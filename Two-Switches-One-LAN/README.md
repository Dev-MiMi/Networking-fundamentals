# Two Switches, One LAN

## 1. Project Title & Purpose

**Title:** Two Switches, One LAN

**Purpose:** To expand a LAN across two switches and verify that devices on different switches can still communicate on the same network.

## 2. Network Diagram

```
PC0 (192.168.1.10) ──┐                    ┌── PC2 (192.168.1.12)
                      Switch0 ────────── Switch1
PC1 (192.168.1.11) ──┘                    └── PC3 (192.168.1.13)

LAN A - 192.168.1.0/24
```

## 3. IP Address Table

| Device | IP | Subnet | Role |
|---|---|---|---|
| PC0 | 192.168.1.10 | 255.255.255.0 /24 | Workstation |
| PC1 | 192.168.1.11 | 255.255.255.0 /24 | Workstation |
| PC2 | 192.168.1.12 | 255.255.255.0 /24 | Workstation |
| PC3 | 192.168.1.13 | 255.255.255.0 /24 | Workstation |

## 4. Device Inventory

| Device | Model | Quantity |
|---|---|---|
| PC | PC-PT | 4 |
| Switch | Cisco 2960-24TT | 2 |
| Cable | Copper Straight-Through | 6 |

## 5. Configuration Steps

1. Placed 4 PCs and 2 switches on the canvas
2. Connected PC0 and PC1 to Switch0 using Copper Straight-Through cables
3. Connected PC2 and PC3 to Switch1 using Copper Straight-Through cables
4. Connected Switch0 to Switch1 using a Copper Straight-Through cable
5. Assigned static IPs to all four PCs
6. Labeled the network "LAN A - 192.168.1.0/24" using the Drawing Palette

## 6. Test Results

| Test | Result |
|---|---|
| PC0 pinged PC1 (192.168.1.11) | ✅ 4/4 packets, 0% loss, 0ms avg |
| PC0 pinged PC2 (192.168.1.12) | ✅ 4/4 packets, 0% loss, 7ms avg |
| PC0 pinged PC3 (192.168.1.13) | ✅ 4/4 packets, 0% loss, 1ms avg |

## 7. Lessons Learned

- Two switches can be connected together to extend a LAN
- All devices remain on the same /24 subnet regardless of which switch they connect to
- Traffic crossing two switches may experience slightly higher latency than traffic on the same switch
- Copper Straight-Through cable works for switch to switch connections in Packet Tracer
