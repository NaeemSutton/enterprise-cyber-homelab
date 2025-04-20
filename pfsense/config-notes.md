# 🔧 pfSense Configuration Notes

## 🌐 Interface Mapping

| Interface | Label     | Subnet       | Notes                                       |
|-----------|-----------|--------------|---------------------------------------------|
| `opt1`    | ECorp     | 10.0.1.0/24  | Internal network (Windows VMs + Metasploitable) |
| `LAN`     | ECorp2    | 10.0.3.0/24  | Attacker network (Kali Linux)              |
| `WAN`     | WAN       | External     | Simulates internet/WAN                      |

---

## 📄 Firewall Rules Summary

### 🔷 ECorp (opt1)

| # | Action | Source        | Destination  | Description                                 |
|--:|--------|----------------|---------------|---------------------------------------------|
| 1 | ✅ Allow | ECorp subnets | ECorp address | Allows traffic within internal subnet       |
| 2 | ✅ Allow | ECorp subnets | 10.0.3.2      | Allows traffic to Kali Linux                |
| 3 | ✅ Allow | ECorp subnets | !RFC1918       | Allows internet traffic (non-private IPs)   |
| 4 | ❌ Block | ECorp subnets | *             | Blocks all other traffic                    |

---

### 🔷 ECorp2 (LAN)

| # | Action | Source          | Destination     | Description                                |
|--:|--------|------------------|------------------|--------------------------------------------|
| 1 | ✅ Allow | *               | ECorp2 Address   | Anti-lockout rule (443/80)                 |
| 2 | ❌ Block | ECorp2 subnets  | WAN subnets      | Prevents traffic to WAN from attacker LAN  |
| 3 | ✅ Allow | ECorp2 subnets  | *                | Default allow LAN (IPv4)                   |
| 4 | ✅ Allow | ECorp2 subnets  | *                | Default allow LAN (IPv6)                   |

---

### 🌐 WAN

| # | Action | Source                       | Destination | Description             |
|--:|--------|-------------------------------|-------------|-------------------------|
| 1 | ❌ Block | Reserved / Not Assigned by IANA | *           | Block bogon networks    |

> 📌 No pass rules on WAN — inbound traffic is blocked by default for security.

---

## 🔐 Security Notes

- Anti-lockout is enabled on ECorp2 to avoid losing admin access
- Traffic is strictly segmented — attacker access is controlled
- WAN is locked down with bogon filtering and no open inbound rules

---

## 🧠 Lessons Learned

- pfSense rule order is critical — top-to-bottom enforcement
- WAN should default to deny unless absolutely needed
- Use firewall aliases for clarity and future scalability
