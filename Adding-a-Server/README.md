# Adding a Server

## 1. Project Title & Purpose

**Title:** Adding a Server

**Purpose:** To add a web server to an existing two-LAN network and verify that a client on a different network can access the server's webpage through a router.

## 2. Network Diagram

```
PC0 (192.168.1.10) ──┐                    ┌── PC2 (192.168.2.10)
                      Switch0 ── Router0 ── Switch1── PC3 (192.168.2.11)
PC1 (192.168.1.11) ──┘                    └── Server0 (192.168.2.20)

LAN A - 192.168.1.0/24        LAN B - 192.168.2.0/24
```

## 3. IP Address Table

| Device | IP | Subnet | Gateway | Role |
|---|---|---|---|---|
| PC0 | 192.168.1.10 | /24 | 192.168.1.1 | Workstation |
| PC1 | 192.168.1.11 | /24 | 192.168.1.1 | Workstation |
| PC2 | 192.168.2.10 | /24 | 192.168.2.1 | Workstation |
| PC3 | 192.168.2.11 | /24 | 192.168.2.1 | Workstation |
| Server0 | 192.168.2.20 | /24 | 192.168.2.1 | Web Server |
| Router0 (LAN A) | 192.168.1.1 | /24 | — | Gateway |
| Router0 (LAN B) | 192.168.2.1 | /24 | — | Gateway |

## 4. Device Inventory

| Device | Model | Quantity |
|---|---|---|
| PC | PC-PT | 4 |
| Server | Server-PT | 1 |
| Switch | Cisco 2960-24TT | 2 |
| Router | PT-R8200 | 1 |
| Cable | Copper Straight-Through | 7 |

## 5. Configuration Steps

1. Opened Project 4 topology in Packet Tracer
2. Added Server0 to the canvas on LAN B
3. Connected Server0 to Switch1 using a Copper Straight-Through cable
4. Assigned static IP 192.168.2.20 /24 to Server0 with gateway 192.168.2.1
5. Enabled HTTP service on Server0
6. Opened web browser on PC0
7. Typed http://192.168.2.20 in the URL bar and clicked Go

## 6. Test Results

| Test | Result |
|---|---|
| PC0 accessed Server0 webpage via http://192.168.2.20 | ✅ Page loaded successfully |
| Traffic crossed from LAN A through Router0 to LAN B | ✅ Successful |
| Cisco Packet Tracer default webpage displayed | ✅ Displayed correctly |

## 7. Lessons Learned

- A server functions like any other device on a network — it needs an IP, subnet and gateway
- Web traffic travels across different networks through a router just like ping traffic
- A client on LAN A can access a server on LAN B as long as routing is configured correctly
- This setup mirrors how real internet browsing works — a request leaves your network, travels through routers and reaches a web server on a different network
