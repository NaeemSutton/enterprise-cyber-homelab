# 🛠️ Kali Linux Setup Notes

This VM is designated as the attacker machine in the lab. It’s connected to the `Ecorp2` (LAN) network and will be used for testing, simulation, and analysis once the environment is fully built.

---

## 📡 Network Configuration

- **Interface**: `Ecorp2 (LAN)`
- **Subnet**: `10.0.3.0/24`
- **Expected IP**: `10.0.3.2` (static or DHCP)
- **Gateway**: `10.0.3.1` (pfSense)

---

## 🔧 Initial Setup Steps

- ✅ Installed latest version of **Kali Linux**
- ✅ Updated packages:
  ```bash
  sudo apt update && sudo apt upgrade -y
