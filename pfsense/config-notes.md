# 🔧 pfSense Configuration Notes

## 🌐 Interface Mapping

| Interface | Label     | Subnet       | Notes                        |
|-----------|-----------|--------------|------------------------------|
| `opt1`    | ECorp     | 10.0.1.0/24  | Internal network (Windows VMs + Metasploitable) |
| `LAN`     | ECorp2    | 10.0.3.0/24  | Attacker network (Kali Linux) |

---

## 📄 Firewall Rules Summary

### 🔷 ECorp (opt1)

| # | Action | Source        | Destination  | Description                                 |
|--:|--------|----------------|---------------|---------------------------------------------|
| 1 | ✅ Allow | ECorp subnets | ECorp address | Allows traffic within internal subnet       |
| 2 | ✅ Allow | ECorp subnets | 10.0.3.2      | Allows traffic to Kali Linux                |
| 3 | ✅ Allow | ECorp subnets | !RFC1918       | Allows internet traffic (non-private IPs)   |
| 4 | ❌ Block | ECorp subnets | *             | Blocks all other traffic                    |

> 📌 These rules prioritize internal comms, allow limited external reach, and enforce a default deny policy.

---

### 🔷 ECorp2 (LAN)

| # | Action | Source          | Destination     | Description                                |
|--:|--------|------------------|------------------|--------------------------------------------|
| 1 | ✅ Allow | *               | ECorp2 Address   | Anti-lockout rule (443/80)                 |
| 2 | ❌ Block | ECorp2 subnets  | WAN subnets      | Prevents traffic to WAN from attacker LAN  |
| 3 | ✅ Allow | ECorp2 subnets  | *                | Default allow LAN (IPv4)                   |
| 4 | ✅ Allow | ECorp2 subnets  | *                | Default allow LAN (IPv6)                   |

> 📌 These rules allow full outbound traffic from Kali and protect WAN from direct attacker access.

---

## 🔐 Security Notes

- **Anti-lockout rule** is enabled on ECorp2 to avoid admin lockout.
- Last rule on ECorp blocks all other traffic for strict segmentation.
- Communication between attacker and victim subnets is controlled by explicit allow to Kali’s IP.

---

## 🧠 Lessons Learned

- pfSense rule order matters — top rules take precedence.
- Use explicit IPs for attacker machines to tightly control access.
- Anti-lockout rule is critical when locking down subnets.

---

