# Static Routing Lab

---

## Topology

- 3 Routers (R1, R2, R3)
- 2 LANs
- Multiple interconnected networks

---

## Networks

### LAN 1
- Network: 192.168.1.0 /24
- PC1: 192.168.1.1
- R1 G0/1: 192.168.1.254

---

### R1 ↔ R2
- Network: 192.168.12.0 /24
- R1 G0/0: 192.168.12.1
- R2 G0/0: 192.168.12.2

---

### R2 ↔ R3
- Network: 192.168.13.0 /24
- R2 G0/1: 192.168.13.2
- R3 G0/0: 192.168.13.3

---

### LAN 2
- Network: 192.168.3.0 /24
- PC2: 192.168.3.1
- R3 G0/1: 192.168.3.254

---

## Objective

Configure static routes so that:

PC1 can ping PC2

---

## Router Configuration

### R1
enable
configure terminal

hostname R1

interface g0/0
ip address 192.168.12.1 255.255.255.0
no shutdown

interface g0/1
ip address 192.168.1.254 255.255.255.0
no shutdown---

### R2
enable
configure terminal

hostname R2

interface g0/0
ip address 192.168.12.2 255.255.255.0
no shutdown

interface g0/1
ip address 192.168.13.2 255.255.255.0
no shutdown---

### R3
enable
configure terminal

hostname R3

interface g0/0
ip address 192.168.13.3 255.255.255.0
no shutdown

interface g0/1
ip address 192.168.3.254 255.255.255.0
no shutdown---

## Static Routes

### R1
ip route 192.168.3.0 255.255.255.0 192.168.12.2---

### R2
ip route 192.168.1.0 255.255.255.0 192.168.12.1
ip route 192.168.3.0 255.255.255.0 192.168.13.3---

### R3
ip route 192.168.1.0 255.255.255.0 192.168.13.2---

## PC Configuration

### PC1
- IP: 192.168.1.1
- Mask: 255.255.255.0
- Gateway: 192.168.1.254

### PC2
- IP: 192.168.3.1
- Mask: 255.255.255.0
- Gateway: 192.168.3.254

---

## Verification
show ip route
show ip interface brief
ping 192.168.3.1---

## Expected Result

- Ping from PC1 to PC2 is successful
- Routing table contains static routes

---

## Key Concepts

- Router needs routes to reach remote networks
- Static routes define the path manually
- Each router must know all remote networks

---

## Troubleshooting

- Verify IP addresses
- Check next-hop correctness
- Ensure interfaces are up
- Check routing table
