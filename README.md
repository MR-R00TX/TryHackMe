<div align="center">

![SecFest '26 event banner](evidence/event-banner.png)

# 🛡️ Hack The Box — SecFest'26 CTF
### Offensive Security | Web Exploitation | AI/LLM Security | Forensics | Secure Coding

**A reproducible, evidence-led technical research journal**

[![CTF](https://img.shields.io/badge/CTF-SecFest%2726-dc2626?style=for-the-badge)](https://ctf.hackthebox.com/event/3688)
![Result](https://img.shields.io/badge/Submitted-26%2F26-95ef00?style=for-the-badge)
![Scenarios](https://img.shields.io/badge/Scenarios-20%2F20-38bdf8?style=for-the-badge)
![Points](https://img.shields.io/badge/Points-16775-f59e0b?style=for-the-badge)
![Global Rank](https://img.shields.io/badge/Global%20Rank-%236-8b5cf6?style=for-the-badge)

**Player:** [MR-R00TX](https://github.com/MR-R00TX) · **Team:** `hrmunna` · **Event:** SecFest'26, presented by Monzo

</div>

> [!IMPORTANT]
> **Results versus documentation coverage.** The screenshots supplied by the player show **20/20 scenarios, 26/26 flag submissions, 16,775 points, global rank #6**. This repository is an honest reconstruction from *available* terminal transcripts, screenshot evidence and scripts. It does **not** claim that all 26 flag strings or 20 individual exploit transcripts were recovered. Known flags and reproducible commands are provided where evidence exists; unknown submissions are expressly marked **NOT RECOVERED**. The number of scenarios and flags differs because **Stolen Variables accounts for seven submissions**.
>
> **Publication:** Challenge solutions and flags should be shared only when the event organizers permit public write-ups. The documentation was assembled after the player's reported solves; historical targets/ports are illustrative and may be offline.

---

## 🏆 Event outcome

| Metric | Recorded outcome |
|:--|--:|
| Global rank shown | **6th** |
| Total score | **16,775** |
| Flag submissions | **26/26** |
| Scenarios completed | **20/20** |
| Participation | **Solo (`hrmunna`)** |
| Source | Player-provided completion and leaderboard screenshots |

| Leaderboard | Challenge completion |
|:--:|:--:|
| ![Global sixth place](evidence/leaderboard.png) | ![All scenarios solved](evidence/completion.png) |

## 🔍 What this repository demonstrates

Rather than presenting flags without explanation, the write-ups separate **observed behavior**, **hypothesis**, **exploit**, **confirmation** and **defensive remediation**. The most fully reconstructed cases demonstrate:

- **Client-side session trust:** FrontDesk accepted an unsigned Base64 JSON cookie, allowing `guest` to become `admin` and exposing a restricted flag.
- **Business logic failure:** Quantum Market rewarded mass referral registrations without adequate abuse controls, allowing 134 referral bonuses, 1,340 credits and a 1,337-credit blueprint purchase.
- **LLM prompt-injection trust boundary:** Shard Council accepted adversary-controlled external data as an authoritative audit instruction. With three approved identities, council votes authorized changes to an AI tool's description; a Backup Agent then sent its derived shard key to an external webhook.
- **AI-tool file access / path traversal:** Yokado Tickets' `read_kb` file argument reached `flag.txt` through an indirect traversal pattern.
- **MCP path traversal / insecure deserialization hypothesis:** Neon Registry's resource loader read `../app.py` and `../config.py`; a PDFMiner CMap pickle-loading chain was prepared. The provided transcript does not demonstrate the resulting flag for this instance.
- **Webhook integrity validation:** Checkout investigation found a route where omitting a signature header could mark a payment paid. A final flag response was not present in the recovered excerpt.
- **Memory forensics:** Leaked analysis correlated suspicious PID 1521 (`jN8ziHXGE`) with outbound `77.74.198.52:4444` and recovered the prior solved flag.
- **Shell command injection:** DNS Dossier testing recorded a shell-metacharacter payload and command-execution evidence; final flag output needs to be restored.
- **Financial application secure coding:** Logics & Business source and patches expose currency-exchange, loans and authorization logic relevant to secure financial workflows.

## 🗂️ Navigate the complete 20-scenario archive

All **20 official challenge names** have been recovered from the player's category screenshots. A detailed technical solution exists where a successful transcript survives. For the other entries we include verified challenge hints, artifacts and an evidence-restoration path rather than invented exploits.

| Category | Challenges | Recovered detailed evidence |
|:--|:--|:--|
| **Web (8)** | [FrontDesk](challenges/web/frontdesk.md), [Open Invitation](challenges/web/open-invitation.md), [Checkout](challenges/web/checkout.md), [DNS Dossier](challenges/web/dns-dossier.md), [SR Network](challenges/web/sr-network.md), [Ghost Fleet](challenges/web/ghost-fleet.md), [Nebula Network](challenges/web/nebula-network.md), [**Quantum Market**](challenges/web/quantum-market.md) | FrontDesk: **confirmed unsigned cookie bypass and flag**; Quantum Market: **confirmed referral exploit and flag**; SR Network: **prior solved flag and partial API trace**; Checkout/DNS: partial |
| **Crypto (3)** | [Based0x](challenges/crypto/based0x.md), [Me is Mey](challenges/crypto/me-is-mey.md), [The Gazorpazorps](challenges/crypto/the-gazorpazorps.md) | All three original hints; **Based0x and Me is Mey flags recovered**, Gazorpazorps flag missing |
| **Forensics (2)** | [Stolen Variables (7 answers)](challenges/forensics/stolen-variables.md), [Leaked](challenges/forensics/leaked.md) | Seven exact question prompts and AWS/CloudFront investigative candidates; **Leaked flag and Linux memory/network evidence** |
| **AI/ML (6)** | [Re-Cars AI](challenges/ai-ml/re-cars-ai.md), [Cosmic Crisis](challenges/ai-ml/cosmic-crisis.md), [Stock Signals](challenges/ai-ml/stock-signals.md), [Neon Registry](challenges/ai-ml/neon-registry.md), [**Yokado Tickets**](challenges/ai-ml/yokado-tickets.md), [**Shard Council**](challenges/ai-ml/shard-council.md) | Yokado and Shard Council: **confirmed flag**; Neon MCP traversal: confirmed, previous-instance RCE shown |
| **Secure Coding (1)** | [Logics & Business](challenges/secure-coding/logics-and-business.md) | Flask banking code and defensive patch analysis |

Read **[the complete 20-challenge master Markdown](COMPLETE_WRITEUP.md)** for a single-file version. See **[Challenge and flag index](CHALLENGE_INDEX.md)** for all 20 scenario names and all 26 submission slots. The [flag evidence ledger](FLAGS.md) distinguishes actual submitted strings from hypotheses.

## 🧭 Reproduction methodology

```text
Capture challenge context
      ↓
Map inputs, endpoints, trust boundaries, permissions
      ↓
Build hypothesis and a controlled baseline
      ↓
Execute the smallest meaningful proof of concept
      ↓
Observe the response; distinguish success from mere acceptance
      ↓
Recover and confirm the exact flag (when evidence exists)
      ↓
Explain root cause, blast radius and remediation
```

Read [Methodology](METHODOLOGY.md), [Research timeline](RESEARCH_TIMELINE.md), [Reproduction checklist](REPRODUCTION_CHECKLIST.md), [Evidence policy](EVIDENCE.md), [Evidence manifest](EVIDENCE_MANIFEST.md), and [Publication guidance](PUBLICATION.md).

## 🗃️ Directory structure

```text
HTB-SecFest26-Writeups/
├── README.md                      # This landing page
├── CHALLENGE_INDEX.md             # 20 scenario / 26 submission mapping
├── FLAGS.md                       # Verified strings and missing evidence
├── METHODOLOGY.md                 # Repeatable CTF and pentesting process
├── EVIDENCE.md                    # Evidence grading and provenance
├── EVIDENCE_MANIFEST.md           # Screenshot-to-claim matrix
├── PUBLICATION.md                 # Scope and disclosure ethics
├── RESEARCH_TIMELINE.md           # Chronology and failed branches
├── REPRODUCTION_CHECKLIST.md      # Evidence and verification rules
├── COMPLETE_WRITEUP.md            # All 20 chapters as one Markdown file
├── challenges/
│   ├── web/                       # 8 named Web scenarios
│   ├── crypto/                    # 3 named Crypto scenarios
│   ├── ai-ml/                     # Shard Council, Yokado, Neon Registry
│   ├── secure-coding/             # Logics & Business
│   ├── forensics/                 # Stolen Variables / 7-question case
├── scripts/                       # Reproduction helpers / snippets
├── evidence/                      # Original screenshots supplied by player
├── notes/                         # Restoration checklist
└── templates/                     # Evidence-first write-up template
```

## 🛠️ Environment

```bash
# Kali / Debian-based systems
sudo apt update
sudo apt install -y curl jq python3 python3-venv git

# Work only against an explicitly authorized, running CTF instance.
# Ports and session IDs rotate when a container is restarted.
export TARGET='http://CTF_INSTANCE_IP:PORT'
```

Useful skills: Bash scripting, JSON inspection (`jq`), browser DevTools, API fuzzing, JWT inspection, Python proof-of-concept development, HTTP/MCP protocol comprehension, SQL and source-code review, evidence capture and defensive reporting.

## 🧠 Most important lessons

1. **Treat third-party data as data, not system policy.** The Shard Council chain crossed that boundary twice: remote weight files and tool descriptions.
2. **Server-side state changes must be authenticated, authorized and rate-controlled.** Quantum Market credited referrals on registration without sufficient abuse mitigation.
3. **Tool permission isn't equivalent to security.** Restricting agents to a tool allowlist is necessary but not sufficient when descriptions and outputs are controlled by lower-trust actors.
4. **A 200 response does not prove exploitation.** Backups can report success without returning any key or downloadable file; an audit request can be accepted and still rejected later.
5. **High-quality work is auditable.** Distinguishing flags shown in logs from unrecovered flag submissions makes this portfolio stronger, not weaker.

## 📄 For technical reviewers

If you are assessing this project as proof of work, start with the [one-page recruiter brief](RECRUITER_BRIEF.md) and the [full consolidated write-up](COMPLETE_WRITEUP.md). A runnable [repository consistency checker](scripts/check_repository.py) is included.

## 👨‍💻 Author

**Md. Munna** · Offensive Security / Web Application Penetration Testing  
GitHub: [MR-R00TX](https://github.com/MR-R00TX) · LinkedIn: [mdmunna-sec](https://www.linkedin.com/in/mdmunna-sec/)  
Cybersecurity venture: [Security Crown](https://seccrown.com/)

*All actions described here relate to authorized CTF labs. Do not reuse challenge commands on real organizations without written authorization.*
