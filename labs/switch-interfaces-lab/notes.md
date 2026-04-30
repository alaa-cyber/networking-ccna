# Switch Interfaces Configuration Lab

---

## Topology

- 1 Router (R1)
- 2 Switches (SW1, SW2)
- 4 PCs
- Network: 172.16.0.0 /16

---

## Objective

- Configure hostnames
- Assign IP addresses
- Configure speed and duplex manually
- Add interface descriptions
- Disable unused interfaces

---

## IP Addressing

### Router (R1)
- G0/0 → 172.16.255.254 /16

### PCs
- PC1 → 172.16.0.1 /16
- PC2 → 172.16.0.2 /16
- PC3 → 172.16.0.3 /16
- PC4 → 172.16.0.4 /16

Default Gateway (all PCs):
172.16.255.254

---

## Router Configuration
enable
configure terminal

hostname R1

interface g0/0
ip address 172.16.255.254 255.255.0.0
no shutdown
description Connection to SW1---

## Switch Configuration (SW1)
enable
configure terminal

hostname SW1

interface f0/1
description PC1

interface f0/2
description PC2

interface g0/1
description Link to Router
speed 1000
duplex full

interface g0/2
description Link to SW2
speed 1000
duplex full---

## Switch Configuration (SW2)
enable
configure terminal

hostname SW2

interface f0/1
description PC3

interface f0/2
description PC4

interface g0/1
description Link to SW1
speed 1000
duplex full
