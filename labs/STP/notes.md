# Spanning Tree Protocol (STP) Lab

---

# Objective

Practice STP configuration by:

- Identifying the Root Bridge
- Verifying STP port roles
- Configuring Primary and Secondary Root Bridges
- Modifying STP Cost
- Modifying Port Priority
- Configuring PortFast
- Configuring BPDU Guard

---

# Topology

Switches

- SW1
- SW2
- SW3
- SW4

VLANs

- VLAN1
- VLAN2

Hosts

- PC1 (VLAN1)
- PC2 (VLAN2)

---

# Task 1

Determine the current STP topology.

Commands

```cisco
show spanning-tree

show spanning-tree vlan 1

show spanning-tree vlan 2

show spanning-tree root
```

Verify

- Root Bridge
- Root Port
- Designated Ports
- Alternate/Blocking Ports

---

# Task 2

Configure Root Bridges.

SW1

Primary Root for VLAN1

```cisco
spanning-tree vlan 1 root primary
```

Secondary Root for VLAN2

```cisco
spanning-tree vlan 2 root secondary
```

---

SW2

Primary Root for VLAN2

```cisco
spanning-tree vlan 2 root primary
```

Secondary Root for VLAN1

```cisco
spanning-tree vlan 1 root secondary
```

Verify

```cisco
show spanning-tree root
```

---

# Task 3

Modify STP Cost.

Increase VLAN1 cost on SW4 interface F0/2.

```cisco
interface f0/2

spanning-tree vlan 1 cost 100
```

Verify

```cisco
show spanning-tree
```

Expected Result

SW4 may select another Root Port if a lower-cost path exists.

---

# Task 4

Modify Port Priority.

Increase the priority of SW1 interface F0/1.

```cisco
interface f0/1

spanning-tree vlan 1 port-priority 240
```

Verify

```cisco
show spanning-tree
```

Expected Result

STP may elect another Designated Port if a better Port ID becomes available.

---

# Task 5

Configure PortFast.

SW3

```cisco
interface f0/3

spanning-tree portfast
```

SW4

```cisco
interface f0/3

spanning-tree portfast
```

---

# Task 6

Configure BPDU Guard.

SW3

```cisco
interface f0/3

spanning-tree bpduguard enable
```

SW4

```cisco
interface f0/3

spanning-tree bpduguard enable
```

---

# Verification Commands

```cisco
show spanning-tree

show spanning-tree root

show spanning-tree summary

show spanning-tree interface

show spanning-tree vlan 1

show spanning-tree vlan 2

show running-config
```

---

# Key Concepts Learned

- Root Bridge Election
- Root Primary
- Root Secondary
- Root Port
- Designated Port
- Alternate Port
- STP Cost
- Port Priority
- PortFast
- BPDU Guard
- STP Verification
- STP Convergence

---

# Important Notes

## STP Cost

Lower Cost

↓

Preferred Path

Higher Cost

↓

Less Preferred Path

---

## Port Priority

Lower Priority Value

↓

Preferred Port

---

## Root Bridge

Lowest Bridge ID wins.

Bridge ID =

Priority + MAC Address

---

## PortFast

Used only on access ports connected to end devices.

Never enable PortFast on trunk ports.

---

## BPDU Guard

Protects PortFast interfaces.

If a BPDU is received,

↓

The interface enters Err-Disabled state.


