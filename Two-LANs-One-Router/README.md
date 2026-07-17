# Two LANs, One Router

## 1. Project Title & Purpose

**Title:** Two LANs, One Router

**Purpose:** To connect two separate networks using a router and verify that devices on different networks can communicate with each other.

## 2. Network Diagram

```
PC0 (192.168.1.10) ──┐                    ┌── PC2 (192.168.2.10)
                      Switch0 ── Router0 ── Switch1
PC1 (192.168.1.11) ──┘                    └── PC3 (192.168.2.11)

LAN A - 192.168.1.0/24        LAN B - 192.168.2.0/24
```

## 3. IP Address Table

| Device | IP | Subnet | Gateway | Role |
|---|---|---|---|---|
| PC0 | 192.168.1.10 | /24 | 192.168.1.1 | Workstation |
| PC1 | 192.168.1.11 | /24 | 192.168.1.1 | Workstation |
| PC2 | 192.168.2.10 | /24 | 192.168.2.1 | Workstation |
| PC3 | 192.168.2.11 | /24 | 192.168.2.1 | Workstation |
| Router0 (LAN A) | 192.168.1.1 | /24 | — | Gateway |
| Router0 (LAN B) | 192.168.2.1 | /24 | — | Gateway |

## 4. Device Inventory

| Device | Model | Quantity |
|---|---|---|
| PC | PC-PT | 4 |
| Switch | Cisco 2960-24TT | 2 |
| Router | PT-R8200 | 1 |
| Cable | Copper Straight-Through | 6 |

## 5. Configuration Steps

1. Placed 4 PCs, 2 switches and 1 router on the canvas
2. Connected PC0 and PC1 to Switch0 using Copper Straight-Through cables
3. Connected PC2 and PC3 to Switch1 using Copper Straight-Through cables
4. Connected Switch0 to Router0 and Switch1 to Router0
5. Configured Router0 LAN A interface with IP 192.168.1.1 /24 via CLI
6. Configured Router0 LAN B interface with IP 192.168.2.1 /24 via CLI
7. Assigned static IPs and default gateways to all four PCs
8. Labeled networks "LAN A - 192.168.1.0/24" and "LAN B - 192.168.2.0/24"

## 6. Test Results

| Test | Result |
|---|---|
| PC0 pinged PC1 (192.168.1.11) | ✅ 4/4 packets, 0% loss |
| PC0 pinged PC2 (192.168.2.10) | ✅ 3/4 packets, 25% loss (normal ARP behaviour on first ping) |
| PC0 pinged PC3 (192.168.2.11) | ✅ 3/4 packets, 25% loss (normal ARP behaviour on first ping) |

## 7. Lessons Learned

- A router is required to connect two different networks
- Each router interface acts as the default gateway for its connected network
- The default gateway must share the same network IP as the devices it serves
- First ping packet loss is normal in Packet Tracer due to ARP resolution
- Devices on different subnets cannot communicate without a router
