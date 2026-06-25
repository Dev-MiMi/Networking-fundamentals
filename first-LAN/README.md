## 1. Project Title & Purpose

**Title:** My First LAN

**Purpose:** To build and verify a basic Local Area Network (LAN) using two workstations connected through a switch. This project establishes foundational knowledge of how devices communicate on the same network.

---

## 2. Network Diagram

```
PC0 (192.168.1.10) ──┐
                      ├── Switch0 (2960-24TT)
PC1 (192.168.1.11) ──┘
```

---

## 3. IP Address Table

| Device | IP | Subnet | Role |
|--------|----|--------|------|
| PC0 | 192.168.1.10 | 255.255.255.0 /24 | Workstation |
| PC1 | 192.168.1.11 | 255.255.255.0 /24 | Workstation |

---

## 4. Device Inventory

| Device | Model | Quantity |
|--------|-------|----------|
| PC | PC-PT | 2 |
| Switch | Cisco 2960-24TT | 1 |
| Cable | Copper Straight-Through | 2 |

---

## 5. Configuration Steps

1. Placed 2 PCs and 1 Switch in Packet Tracer
2. Connected each PC to the switch using Copper Straight-Through cables via FastEthernet0/1 and FastEthernet0/2
3. Assigned static IP `192.168.1.10 /24` to PC0
4. Assigned static IP `192.168.1.11 /24` to PC1

---

## 6. Test Results

- PC0 pinged PC1 (`192.168.1.11`) successfully
- Packets sent: **4** | Received: **4** | Lost: **0** (0% loss)
- ✅ Communication confirmed

---

## 7. Lessons Learned

- A switch connects multiple devices on the same network without any extra configuration
- Devices on the same /24 subnet can communicate directly
- RFC 1918 addresses (`192.168.x.x`) are used for private/local networks
