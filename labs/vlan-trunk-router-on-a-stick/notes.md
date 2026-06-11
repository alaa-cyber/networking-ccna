# VLAN Trunking and Router-on-a-Stick Lab

## Objective

* Configure VLANs
* Configure Access Ports
* Configure Trunk Links
* Configure Native VLAN
* Configure Router-on-a-Stick
* Verify Inter-VLAN Connectivity

---

# Topology

## VLAN 10

Network:
10.0.0.0/26

Devices:

| Device | IP Address |
| ------ | ---------- |
| PC1    | 10.0.0.1   |
| PC2    | 10.0.0.2   |
| PC6    | 10.0.0.3   |
| PC7    | 10.0.0.4   |

Gateway:

10.0.0.62

---

## VLAN 20

Network:
10.0.0.64/26

Devices:

| Device | IP Address |
| ------ | ---------- |
| PC5    | 10.0.0.65  |

Gateway:

10.0.0.126

---

## VLAN 30

Network:
10.0.0.128/26

Devices:

| Device | IP Address |
| ------ | ---------- |
| PC3    | 10.0.0.129 |
| PC4    | 10.0.0.130 |

Gateway:

10.0.0.190

---

# Step 1 - Create VLANs

```bash
enable
configure terminal

vlan 10
name Engineering

vlan 20
name HR

vlan 30
name Sales

vlan 99
name Native
```

---

# Step 2 - Configure Access Ports

## SW1

```bash
interface range f0/1 - 2
switchport mode access
switchport access vlan 10

interface range f0/3 - 4
switchport mode access
switchport access vlan 30
```

## SW2

```bash
interface f0/1
switchport mode access
switchport access vlan 20

interface range f0/2 - 3
switchport mode access
switchport access vlan 10
```

---

# Step 3 - Configure Trunk Between SW1 and SW2

## SW1

```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30
```

## SW2

```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30
```

---

# Step 4 - Configure Trunk Between SW2 and R1

## SW2

```bash
interface g0/2
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30
```

---

# Step 5 - Configure Router-on-a-Stick

## Physical Interface

```bash
interface g0/0
no shutdown
```

---

## VLAN 10

```bash
interface g0/0.10
encapsulation dot1Q 10
ip address 10.0.0.62 255.255.255.192
```

---

## VLAN 20

```bash
interface g0/0.20
encapsulation dot1Q 20
ip address 10.0.0.126 255.255.255.192
```

---

## VLAN 30

```bash
interface g0/0.30
encapsulation dot1Q 30
ip address 10.0.0.190 255.255.255.192
```

---

## Native VLAN

```bash
interface g0/0.99
encapsulation dot1Q 99 native
```

---

# Step 6 - Verification Commands

```bash
show vlan brief
show interfaces trunk
show ip interface brief
show running-config
```

---

# Connectivity Tests

```bash
ping 10.0.0.65
ping 10.0.0.129
ping 10.0.0.3
```

Expected Result:

All PCs should be able to communicate.

---

# Key Concepts Learned

## Access Port

Connects end devices.

One VLAN only.

---

## Trunk Port

Carries multiple VLANs.

Uses 802.1Q tagging.

---

## Native VLAN

Frames are sent untagged.

Default Native VLAN = 1

Best practice:
Use an unused VLAN such as VLAN 99.

---

## Router-on-a-Stick

One physical router interface.

Multiple logical subinterfaces.

One gateway per VLAN.

---

## 802.1Q

Industry standard for VLAN tagging.

Adds VLAN information to Ethernet frames.

---

# Important Commands

```bash
show vlan brief
show interfaces trunk
show ip route
show ip interface brief
```

---

# Summary

This lab demonstrates:

* VLAN creation
* Access Ports
* Trunk Links
* Native VLAN
* 802.1Q Tagging
* Router-on-a-Stick
* Inter-VLAN Routing

---

## Screenshot

topology.png

```
```
