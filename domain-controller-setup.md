# 🧱 Domain Controller Setup (Windows Server 2022)

This VM acts as the Domain Controller for the `ecorp.local` domain. It is the backbone of the lab's Active Directory environment and allows testing of user account activity, authentication, and domain-joined machine behavior.

---

## 🖥️ Host Info

- **VM Name**: `AD_ 2022`
- **OS**: Windows Server 2022
- **Role**: Active Directory Domain Services (AD DS)
- **IP Address**: `10.0.1.15`
- **Subnet**: `Ecorp / 10.0.1.0/24`
- **DNS**: Self-hosted (this server handles DNS for domain clients)

---

## 🛠️ Setup Summary

- ✅ Set static IP: `10.0.1.15` with DNS pointing to itself
- ✅ Installed AD DS & DNS roles via Server Manager
- ✅ Promoted to Domain Controller (forest root)
- ✅ Created new domain: `ecorp.local`
- ✅ Set domain functional level to Windows Server 2016+
- ✅ Enabled Windows Firewall and allowed domain-related traffic

---

## 👥 Active Directory Info

### Domain
- `ecorp.local`

### OU Structure (Initial)
- `ECorp Computers`
- `ECorp Users`

### Sample Users
- `win10user1` (used on Win10-1)
- `win10user2` (used on Win10-2)

### Domain-Joined Machines
| Hostname   | IP Address | Notes                    |
|------------|------------|--------------------------|
| `WIN10-1`  | 10.0.1.12   | Primary workstation VM   |
| `WIN10-2`  | 10.0.1.13   | Second endpoint for testing |

---

## 🔒 Security Settings

- Default domain policy is currently applied
- Windows Defender is enabled
- No GPOs created yet — baseline domain environment

---

## 📌 Next Steps

- Create custom GPOs for:
  - Logon auditing
  - PowerShell logging
  - Disabling local admin on endpoints
- Install Splunk Universal Forwarder to ship logs (optional)
- Use this machine to simulate user logons, failed attempts, and AD attacks later

---

## 🧠 Notes

- Always snapshot before major changes like role installs or GPO testing
- DNS must be working properly or domain joins will fail
- Consider enabling account lockout policies after baseline testing
