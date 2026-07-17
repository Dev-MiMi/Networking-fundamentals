# Full Company Network

---

## 1. Project Title & Purpose

**Title:** Full Company Network

**Purpose:** To design and build a complete company network with five isolated segments — Workstations, DMZ, Admin, IP Phones, and Printers — all connected through a single router, mirroring a real-world secure network architecture.

---

## 2. Network Diagram

```
Laptop0 (Wi-Fi)
    |
AccessPoint0
    |
PC0, PC1, PC2 ── Switch0 ──┐
                            │
Admin-PC ── Switch2 ────────┤
                            │
IP Phone0, Phone1 ── Switch3┤── Router16 (PT8200)
                            │
Printer0, Printer1 ── Switch4┤
                            │
Web Server, DNS ── Switch1 ──┘
```

| Segment | Subnet |
|---------|--------|
| Workstations | 192.168.1.0/24 |
| DMZ | 192.168.2.0/24 |
| Admin | 192.168.3.0/24 |
| IP Phones | 192.168.4.0/24 |
| Printers | 192.168.5.0/24 |

---

## 3. IP Address Table

| Device | IP | Subnet | Gateway | Role |
|--------|----|--------|---------|------|
| PC0 | 192.168.1.10 | /24 | 192.168.1.1 | Workstation |
| PC1 | 192.168.1.11 | /24 | 192.168.1.1 | Workstation |
| PC2 | 192.168.1.12 | /24 | 192.168.1.1 | Workstation |
| Laptop0 | 192.168.1.13 | /24 | 192.168.1.1 | Wireless Workstation |
| Web Server | 192.168.2.10 | /24 | 192.168.2.1 | Web Server (DMZ) |
| DNS Server | 192.168.2.20 | /24 | 192.168.2.1 | DNS Server (DMZ) |
| Admin-PC | 192.168.3.10 | /24 | 192.168.3.1 | Admin Workstation |
| IP Phone0 | DHCP | /24 | 192.168.4.1 | IP Phone |
| IP Phone1 | DHCP | /24 | 192.168.4.1 | IP Phone |
| Printer0 | 192.168.5.10 | /24 | 192.168.5.1 | Printer |
| Printer1 | 192.168.5.11 | /24 | 192.168.5.1 | Printer |
| Router16 (Workstations) | 192.168.1.1 | /24 | — | Gateway |
| Router16 (DMZ) | 192.168.2.1 | /24 | — | Gateway |
| Router16 (Admin) | 192.168.3.1 | /24 | — | Gateway |
| Router16 (IP Phones) | 192.168.4.1 | /24 | — | Gateway |
| Router16 (Printers) | 192.168.5.1 | /24 | — | Gateway |

---

## 4. Device Inventory

| Device | Model | Quantity |
|--------|-------|----------|
| PC | PC-PT | 4 |
| Laptop | Laptop-PT | 1 |
| IP Phone | Cisco 7960 | 2 |
| Printer | Printer-PT | 2 |
| Server | Server-PT | 2 |
| Switch | Cisco 2960-24TT | 5 |
| Router | PT8200 | 1 |
| Access Point | AccessPoint-PT | 1 |
| Cable | Copper Straight-Through | 12 |

---

## 5. Configuration Steps

1. Placed all devices on canvas and organized into 5 network segments
2. Connected all devices to their respective switches using Copper Straight-Through cables
3. Added NIM-ES2-4 module to Router16 to provide extra interfaces
4. Configured standard router interfaces for Workstations and DMZ:

```bash
Router(config)# ip routing

Router(config)# interface GigabitEthernet0/1/0
Router(config-if)# switchport access vlan 30

Router(config)# interface vlan 30
Router(config-if)# ip address 192.168.3.1 255.255.255.0
Router(config-if)# no shutdown

Router(config)# interface GigabitEthernet0/1/1
Router(config-if)# switchport access vlan 40

Router(config)# interface vlan 40
Router(config-if)# ip address 192.168.4.1 255.255.255.0
Router(config-if)# no shutdown

Router(config)# interface GigabitEthernet0/1/2
Router(config-if)# switchport access vlan 50

Router(config)# interface vlan 50
Router(config-if)# ip address 192.168.5.1 255.255.255.0
Router(config-if)# no shutdown
```

5. Fixed VLAN mismatch on NIM-connected switches:

```bash
Switch(config)# interface range FastEthernet0/1-24
Switch(config-if-range)# switchport access vlan [30/40/50]
```

6. Swapped Laptop0 wired module for wireless module (PT-LAPTOP-NM-1W)
7. Connected Laptop0 wirelessly to AccessPoint0
8. Configured DNS server with record mapping `myserver.com` to `192.168.2.10`

---

## 6. Test Results

| Test | Result |
|------|--------|
| Admin-PC → PC1 (192.168.1.11) | ✅ 4/4 packets, 0% loss |
| Admin-PC → Web Server (192.168.2.20) | ✅ 4/4 packets, 0% loss |
| Admin-PC → Admin-PC (192.168.3.10) | ✅ 4/4 packets, 0% loss |
| Admin-PC → IP Phones (192.168.4.10) | ❌ 100% loss — DHCP limitation |
| Admin-PC → Printer0 (192.168.5.10) | ✅ 3/4 packets, 25% loss (ARP) |
| Admin-PC → http://myserver.com | ✅ Page loaded successfully |
| Laptop0 → http://myserver.com (wireless) | ✅ Page loaded successfully |

---

## 7. Lessons Learned

- A single router can connect multiple networks using both standard interfaces and NIM modules
- NIM-ES2-4 ports are Layer 2 only — routing requires VLAN + SVI configuration
- Native VLAN mismatches between router NIM ports and switches must be resolved by matching VLANs on switch ports
- `no ip domain-lookup` prevents the router from freezing on mistyped commands
- IP Phones in Packet Tracer use DHCP only — no static IP option exists
- The 7960 IP Phone model has known limitations with DHCP through the router NIM-based VLAN setups in Packet Tracer
- Wireless devices require a physical module swap before connecting to an access point
- Separating network segments improves security — each segment is isolated but reachable through the router
- This topology directly implements Section 1's recommendation of five separate company networks
