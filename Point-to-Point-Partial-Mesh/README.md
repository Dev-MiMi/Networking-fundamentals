# Point-to-Point & Partial Mesh

## 1. Project Title & Purpose

**Title:** Point-to-Point & Partial Mesh

**Purpose:** To build a partial mesh topology using three routers with point-to-point links and verify that devices on all three separate LANs can communicate through static routing.

## 2. Network Diagram

```
PC0 ── Switch0 ── Router0 ── Router1 ── Switch1 ── PC1
                     |
                  Router2
                     |
                  Switch2
                     |
                    PC2

Point-to-Point Links:
Router0 ↔ Router1 → 10.0.0.0/30
Router0 ↔ Router2 → 10.0.1.0/30
```

## 3. IP Address Table

| Device | Interface | IP | Subnet | Gateway | Role |
|---|---|---|---|---|---|
| PC0 | Fa0 | 192.168.1.10 | /24 | 192.168.1.1 | Workstation |
| PC1 | Fa0 | 192.168.2.10 | /24 | 192.168.2.1 | Workstation |
| PC2 | Fa0 | 192.168.3.10 | /24 | 192.168.3.1 | Workstation |
| Router0 | Gi0/0/0 | 10.0.0.1 | /30 | — | Link to Router1 |
| Router0 | Gi0/0/1 | 10.0.1.1 | /30 | — | Link to Router2 |
| Router0 | Vlan10 | 192.168.1.1 | /24 | — | LAN A Gateway |
| Router1 | Gi0/0/1 | 10.0.0.2 | /30 | — | Link to Router0 |
| Router1 | Gi0/0/0 | 192.168.2.1 | /24 | — | LAN B Gateway |
| Router2 | Gi0/0/1 | 10.0.1.2 | /30 | — | Link to Router0 |
| Router2 | Gi0/0/0 | 192.168.3.1 | /24 | — | LAN C Gateway |

## 4. Device Inventory

| Device | Model | Quantity |
|---|---|---|
| PC | PC-PT | 3 |
| Switch | Cisco 2960-24TT | 3 |
| Router | PT8200 | 3 |
| Cable | Copper Straight-Through | 6 |

## 5. Configuration Steps

1. Placed 3 PCs, 3 switches and 3 routers on canvas
2. Connected each PC to its respective switch
3. Connected each switch to its respective router
4. Connected Router0 to Router1 and Router0 to Router2 for partial mesh
5. Configured LAN interfaces on each router
6. Configured point-to-point /30 links between routers:

```bash
! Router0
Router0(config)# interface GigabitEthernet0/0/0
Router0(config-if)# ip address 10.0.0.1 255.255.255.252
Router0(config-if)# no shutdown

Router0(config)# interface GigabitEthernet0/0/1
Router0(config-if)# ip address 10.0.1.1 255.255.255.252
Router0(config-if)# no shutdown

! Router1
Router1(config)# interface GigabitEthernet0/0/1
Router1(config-if)# ip address 10.0.0.2 255.255.255.252
Router1(config-if)# no shutdown

! Router2
Router2(config)# interface GigabitEthernet0/0/1
Router2(config-if)# ip address 10.0.1.2 255.255.255.252
Router2(config-if)# no shutdown
```

7. Added static routes on all three routers:

```bash
! Router0
Router0(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
Router0(config)# ip route 192.168.3.0 255.255.255.0 10.0.1.2

! Router1
Router1(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1
Router1(config)# ip route 192.168.3.0 255.255.255.0 10.0.0.1

! Router2
Router2(config)# ip route 192.168.1.0 255.255.255.0 10.0.1.1
Router2(config)# ip route 192.168.2.0 255.255.255.0 10.0.1.1
```

8. Assigned static IPs and gateways to all PCs

## 6. Test Results

| Test | Result |
|---|---|
| PC0 → PC1 (192.168.2.10) | ✅ 2/4 packets first run (ARP), 4/4 second run |
| PC0 → PC2 (192.168.3.10) | ✅ 2/4 packets first run (ARP), 4/4 second run |

## 7. Lessons Learned

- Point-to-point router links require dedicated /30 subnets separate from LAN networks
- Using LAN IP ranges on router-to-router links causes IP conflicts and routing chaos
- Static routes must be configured on every router for full end-to-end connectivity
- Each router only automatically knows its directly connected networks — everything else requires static routes
- Router2 reaches PC1's network through Router0 — traffic doesn't always take a direct path
- /30 subnets are industry standard for point-to-point links — only 2 usable IPs needed
- First ping packet loss is normal ARP behaviour — not a configuration error
