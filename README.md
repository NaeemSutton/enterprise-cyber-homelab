# 🧪 enterprise-cyber-homelab

This homelab simulates a small enterprise network using VirtualBox VMs. It includes attacker and victim machines, a firewall, Active Directory (on Windows Server 2022), and centralized logging with Splunk—designed for hands-on blue team and purple team practice.

---

## 🛠️ Lab Components

| VM Name           | Role                                    | Notes                                 |
|------------------|-----------------------------------------|----------------------------------------|
| **pfSense**       | Firewall/router                         | Interfaces LAN/WAN for segmentation    |
| **Kali Linux**    | Attacker machine                        | Used for recon, exploit, post-exploit |
| **metasploitable_2** | Vulnerable Linux target               | Used for red team testing              |
| **Win10-1**       | Domain-joined endpoint (client)         | Has Splunk UF, Sysmon, logging         |
| **Win10-2**       | Extra endpoint or victim (optional)     | Can be used for lateral movement       |
| **AD_ 2022**      | Domain Controller (Windows Server 2022) | Hosts `ecorp.local` domain             |
| **Nessus**        | Vulnerability scanner                   | Optional; not currently running        |

---

## 🧱 Network Architecture

![Homelab Diagram](architecture/homelab-diagram.png)

- `10.0.3.0/24` — Attacker LAN (Kali Linux)
- `10.0.1.0/24` — Internal LAN (Windows, Metasploitable, AD)
- pfSense bridges traffic between networks with firewall rules

---

## 🔐 Active Directory Setup

- Domain: `ecorp.local`
- Domain Controller: Windows Server 2022 (`AD_ 2022`)
- Domain-joined client: `Win10-1`
- Custom domain users:
  - One on `Win10-1`
  - One on `Win10-2`

---

## 🔎 Logging & Detection

- **Sysmon**: Logs process creation, network connections, etc.
- **Splunk UF**: Installed on `Win10-1`
- **Splunk Web**: Accessed locally for event log analysis
- Collected logs:
  - Sysmon logs
  - PowerShell activity
  - Windows Security log (logon events, failures, etc.)

---

## 🎯 Simulated Attacks

- Recon: `nmap`, `netdiscover`, enum scripts
- Exploits: Metasploit against `metasploitable_2`
- PowerShell attacks: encoded payloads, `Invoke-Mimikatz`
- Credential access: Mimikatz, Pass-the-Hash
- Lateral movement: SMB, RDP, PsExec between Windows VMs

---

## 📂 Repo Structure

```bash
enterprise-cyber-homelab/
├── architecture/
│   └── homelab-diagram.png
├── pfSense/
│   └── config-notes.md
├── vms/
│   ├── kali/
│   │   └── attack-scripts.md
│   ├── metasploitable2/
│   │   └── usage-notes.md
│   ├── win10-1/
│   │   ├── sysmon-config.xml
│   │   ├── splunk-setup.md
│   │   └── domain-join-steps.md
│   ├── win10-2/
│   │   └── usage-notes.md
│   └── ad-2022/
│       └── domain-controller-setup.md
├── detections/
│   ├── test-alerts.md
│   └── rule-tuning-notes.md
├── logs/
│   └── attack-simulation-notes.md
└── screenshots/
    └── alerts-pcap-firewall.png
