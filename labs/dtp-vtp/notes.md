# DTP & VTP Lab

---

# Objective

Configure a switched network using:

- VLANs
- Trunk links
- DTP
- VTP

Verify VLAN propagation between switches.

---

# Topology

Three Cisco Catalyst 2960 switches

- SW1
- SW2
- SW3

Connected with Gigabit Ethernet trunk links.

---

# VLANs

| VLAN | Network | Devices |
|------|----------------|----------------|
|10|10.0.0.0/26|PC1 PC2|
|20|10.0.0.64/26|PC8 PC9|
|30|10.0.0.128/26|PC6 PC7|
|40|10.0.0.192/26|PC3 PC4|

---

# VTP Configuration

## SW1

Mode

```cisco
vtp mode server
```

Domain

```cisco
vtp domain CCNA
```

Create VLANs

```cisco
vlan 10
name VLAN10

vlan 20
name VLAN20

vlan 30
name VLAN30
```

---

## SW2

```cisco
vtp mode transparent
```

Create VLAN40

```cisco
vlan 40
name VLAN40
```

Expected Result

- VLAN40 exists only on SW2.
- It is NOT propagated to SW1 or SW3.

---

## SW3

```cisco
vtp mode client
```

Attempt to create VLAN50

Result

Client mode cannot create VLANs.

---

# Trunk Configuration

Interfaces

SW1 G0/1

SW2 G0/1

SW2 G0/2

SW3 G0/1

```cisco
interface g0/1
switchport mode trunk
switchport nonegotiate
```

Repeat for all trunk interfaces.

---

# Access Ports

SW1

```cisco
interface range fa0/1-3

switchport mode access
```

SW2

```cisco
interface range fa0/1-2

switchport mode access
```

SW3

```cisco
interface range fa0/1-4

switchport mode access
```

---

# VLAN Assignment

SW1

```cisco
interface fa0/1
switchport access vlan 10

interface fa0/2
switchport access vlan 10

interface fa0/3
switchport access vlan 20
```

SW2

```cisco
interface fa0/1
switchport access vlan 40

interface fa0/2
switchport access vlan 40
```

SW3

```cisco
interface fa0/1
switchport access vlan 10

interface fa0/2
switchport access vlan 30

interface fa0/3
switchport access vlan 30

interface fa0/4
switchport access vlan 20
```

---

# DTP

Trunk links

```cisco
switchport mode trunk
switchport nonegotiate
```

Access links

```cisco
switchport mode access
```

DTP should be disabled on trunk interfaces.

---

# Verification

```cisco
show vlan brief

show interfaces trunk

show interfaces switchport

show vtp status

show running-config
```

---

# Expected Results

✅ VLAN10

Visible on

- SW1
- SW2
- SW3

---

✅ VLAN20

Visible on

- SW1
- SW2
- SW3

---

✅ VLAN30

Visible on

- SW1
- SW2
- SW3

---

✅ VLAN40

Visible ONLY on SW2.

---

✅ VLAN50

Cannot be created on SW3 because it is a VTP Client.

---

# Key Concepts Learned

- VLAN creation
- Access ports
- Trunk ports
- DTP negotiation
- Disabling DTP
- VTP Server
- VTP Client
- VTP Transparent
- VLAN propagation
- VTP domain
