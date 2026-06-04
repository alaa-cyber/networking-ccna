# VLSM and Static Routing Lab

## Objective

Subnet the network `192.168.5.0/24` to provide enough addresses for:

- LAN2: 64 hosts
- LAN1: 45 hosts
- LAN3: 14 hosts
- LAN4: 9 hosts
- Point-to-point link between R1 and R2

Then configure static routes so all PCs can ping each other.

---

## VLSM Addressing Plan

| Segment | Hosts Needed | Subnet | Mask | Usable Range | Broadcast |
|---|---:|---|---|---|---|
| LAN2 | 64 | 192.168.5.0/25 | 255.255.255.128 | 192.168.5.1 - 192.168.5.126 | 192.168.5.127 |
| LAN1 | 45 | 192.168.5.128/26 | 255.255.255.192 | 192.168.5.129 - 192.168.5.190 | 192.168.5.191 |
| LAN3 | 14 | 192.168.5.192/28 | 255.255.255.240 | 192.168.5.193 - 192.168.5.206 | 192.168.5.207 |
| LAN4 | 9 | 192.168.5.208/28 | 255.255.255.240 | 192.168.5.209 - 192.168.5.222 | 192.168.5.223 |
| R1-R2 | 2 | 192.168.5.224/30 | 255.255.255.252 | 192.168.5.225 - 192.168.5.226 | 192.168.5.227 |

---

## IP Assignment

### LAN1
- PC1: 192.168.5.129
- R1 G0/0: 192.168.5.190

### LAN2
- PC2: 192.168.5.1
- R1 G0/1: 192.168.5.126

### LAN3
- PC3: 192.168.5.193
- R2 G0/0: 192.168.5.206

### LAN4
- PC4: 192.168.5.209
- R2 G0/1: 192.168.5.222

### Point-to-Point R1-R2
- R1 G0/0/0: 192.168.5.225
- R2 G0/0/0: 192.168.5.226

---

## R1 Configuration

enable
configure terminal

hostname R1

interface g0/0
ip address 192.168.5.190 255.255.255.192
no shutdown

interface g0/1
ip address 192.168.5.126 255.255.255.128
no shutdown

interface g0/0/0
ip address 192.168.5.225 255.255.255.252
no shutdown

ip route 192.168.5.192 255.255.255.240 192.168.5.226
ip route 192.168.5.208 255.255.255.240 192.168.5.226

end
write memory
---

## R2 Configuration

enable
configure terminal

hostname R2

interface g0/0
ip address 192.168.5.206 255.255.255.240
no shutdown

interface g0/1
ip address 192.168.5.222 255.255.255.240
no shutdown

interface g0/0/0
ip address 192.168.5.226 255.255.255.252
no shutdown

ip route 192.168.5.0 255.255.255.128 192.168.5.225
ip route 192.168.5.128 255.255.255.192 192.168.5.225

end
write memory
