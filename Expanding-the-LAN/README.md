# Expanding the LAN

## 1. Project Title & Purpose

**Title:** Expanding the LAN

**Purpose:** To expand an existing LAN by adding more workstations to the same switch and verify that all devices can communicate with each other on the same network.

## 2. Network Diagram

```
PC0 (192.168.1.10) ──┐
PC1 (192.168.1.11) ──┤
                      Switch0 (2960-24TT)
PC2 (192.168.1.12) ──┤
PC3 (192.168.1.13) ──┘
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
| Switch | Cisco 2960-24TT | 1 |
| Cable | Copper Straight-Through | 4 |

## 5. Configuration Steps

1. Opened Project 1 topology in Packet Tracer
2. Added PC2 and PC3 to the canvas
3. Connected PC2 and PC3 to Switch0 using Copper Straight-Through cables
4. Assigned static IP 192.168.1.12 /24 to PC2
5. Assigned static IP 192.168.1.13 /24 to PC3

## 6. Test Results

| Test | Result |
|---|---|
| PC1 pinged PC0 (192.168.1.10) | ✅ 4/4 packets, 0% loss |
| PC1 pinged PC3 (192.168.1.13) | ✅ 4/4 packets, 0% loss |
| PC1 pinged PC2 (192.168.1.12) | ✅ 4/4 packets, 0% loss |

## 7. Lessons Learned

- A single switch can connect multiple devices on the same LAN without extra configuration
- All devices sharing the same /24 subnet can communicate freely — this is what Section 1 calls a flat network
- Adding more devices to a LAN requires no changes to existing device configurations
