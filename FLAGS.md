# Flags and submission evidence — 26/26 completed, 8 exact CTF flag strings preserved

> **Result ≠ retained artifact.** The event completion screenshots show that the participant submitted **26/26** answers across **20/20** scenarios. The original `HTB{...}` strings for eight scenarios are recoverable from the accessible chat. The other completed submissions cannot be safely fabricated from instance guesses. **Stolen Variables** has seven non-standard answer prompts, not seven necessarily `HTB{...}` strings.

| Submission number | Scenario | Source-grounded flag / answer | State |
|---:|---|---|---|
| 01 | FrontDesk | `HTB{N3v3r_Trust_Cl13nt_C00k13s}` | **A — previously reported successful solve** |
| 02 | Open Invitation | NOT RECOVERED | Completion shown only |
| 03 | Checkout | NOT RECOVERED | Payment webhook behavior investigated |
| 04 | DNS Dossier | NOT RECOVERED | Command injection investigated |
| 05 | SR Network | `HTB{f0rg3_s1gn4l_k3y_0v3rl0ad_y3y_ff86f06f753f5d7958e518a37bba20be}` | **B — prior solved flag; full trigger request missing** |
| 06 | Ghost Fleet | NOT RECOVERED | Completed in Web list |
| 07 | Nebula Network | NOT RECOVERED | Completed per final scoreboard |
| 08 | Quantum Market | `HTB{15_th1s_1nfin1t3_m0n3y_gl1tch??_391470769f7bb0c329b5584ca590b959}` | **A — logged** |
| 09 | Based0x | `HTB{enc0d1ng_1s_n0t_th3_s4m3_4s_encrypt10n}` | **B — prior completed solve** |
| 10 | Me is Mey | `HTB{sh4256_bu7_w17h_4_7w157_83f023_c4n_c4u5e_c011i51on5}` | **B — prior completed solve** |
| 11 | The Gazorpazorps | NOT RECOVERED | CBC bit-flipping hint |
| 12 | Stolen Variables Q1: Amplify app ID | Candidate `d209nq8eaf2s88` | Unverified submission |
| 13 | Stolen Variables Q2: exposed IAM user | Candidate `niis-amplify-deployer` | Unverified submission |
| 14 | Stolen Variables Q3: key in `config.js` | Candidate `AKIA453N4QOMFX23RUOL` | Unverified submission |
| 15 | Stolen Variables Q4: attacker's first source IP | NOT ESTABLISHED | Sample IP not necessarily earliest attacker |
| 16 | Stolen Variables Q5: first-use UTC timestamp | NOT ESTABLISHED | Must sort all events |
| 17 | Stolen Variables Q6: first AWS API | NOT ESTABLISHED | Sample actions `ListTables`, `Scan` |
| 18 | Stolen Variables Q7: DynamoDB table | Candidate `niis-identity-records` | Unverified submission |
| 19 | Leaked | `HTB{wh0_l34k3d_th3_cr3ds!!!!?}` | **B — prior completed solve; memory process/C2 evidence** |
| 20 | Re-Cars AI | NOT RECOVERED | Hint only |
| 21 | Cosmic Crisis | NOT RECOVERED | Name only |
| 22 | Stock Signals | NOT RECOVERED | Hint only |
| 23 | Neon Registry | NOT RECOVERED | MCP/PDFMiner research |
| 24 | Yokado Tickets | `HTB{1nd1r3c7-4cc355-byp4553d-tr4v3rs3d}` | **A — tool output** |
| 25 | Shard Council | `HTB{1nf1ltr4t3d_m4n1pul4t3d_r4153d_4_r3b3l10n}` | **A/B — webhook screenshot** |
| 26 | Logics & Business | NOT RECOVERED | Source and patch review |

### Verification notes

- **SR Network:** earlier solved flag captured in prior CTF exchange; documented password-reset `identifier` / 15-star-token behavior; successful final request absent.
- **Based0x / Me is Mey:** exact flags retained in earlier solve notes; starting ciphertext and collision bytes not retained.
- **Leaked:** recorded Linux memory forensic flag plus suspicious PID 1521 and C2 `77.74.198.52:4444`; raw dump not attached.
- **FrontDesk:** Base64-encoded unsigned JSON `{"user":"guest"}` was altered to `{"user":"admin"}` to access `/admin`; exact flag retained in the earlier solve.
- **Quantum Market:** `POST /api/market/purchase` returned `Item purchased successfully`, then `/api/market/my-items` returned the exact flag in `content`.
- **Yokado Tickets:** the `read_kb` response returned the exact flag after `....//....//flag.txt`.
- **Shard Council:** webhook.site `key` query parameter contained the flag; use original clipboard to confirm visually ambiguous `1` vs lowercase `l` if submitting to a new instance.
- **Stolen Variables:** four candidate values are *evidence-derived investigative findings*, not claimed submitted answers.
- **Instance suffixes may rotate**; do not submit a historical flag on a new instance unless the challenge explicitly reuses it.

**Publishing caution:** Release literal challenge flags only after the event organizer permits spoiler write-ups. For a spoiler-free portfolio, redact flag bodies and keep local proof privately.
