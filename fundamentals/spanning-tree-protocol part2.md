# STP Part 2

---

# STP Timers

STP uses three main timers.

## Hello Timer

- Default: **2 seconds**
- BPDUs are sent every 2 seconds by the Root Bridge.

---

## Forward Delay

- Default: **15 seconds**

Time spent in:

- Listening
- Learning

Total:

Listening (15 s) + Learning (15 s) = **30 seconds**

---

## Max Age

- Default: **20 seconds**

If no BPDU is received before Max Age expires, the switch starts a new STP election.

---

# STP Port States

| State | Learns MAC | Forwards Frames |
|--------|------------|-----------------|
| Blocking | ❌ | ❌ |
| Listening | ❌ | ❌ |
| Learning | ✅ | ❌ |
| Forwarding | ✅ | ✅ |
| Disabled | ❌ | ❌ |

---

# STP BPDU

BPDU = **Bridge Protocol Data Unit**

BPDUs are exchanged between switches to:

- Elect the Root Bridge
- Detect topology changes
- Maintain the spanning tree
- Prevent switching loops

Only the Root Bridge generates Configuration BPDUs.

Other switches forward or update them.

---

# BPDU Information

A BPDU contains:

- Root Bridge ID
- Sender Bridge ID
- Root Path Cost
- Port ID
- Timers
- STP Version

---

# STP Optional Features

## PortFast

Purpose:

Immediately places an access port into the Forwarding state.

Advantages:

- Faster PC startup
- Avoids waiting 30 seconds

Configuration

```cisco
interface fa0/1
spanning-tree portfast
```

---

## BPDU Guard

Purpose:

Disables a PortFast interface if a BPDU is received.

Protection against:

- Rogue switches
- Unauthorized devices

Configuration

```cisco
interface fa0/1
spanning-tree bpduguard enable
```

---

## Root Guard

Purpose:

Prevents another switch from becoming the Root Bridge.

---

## Loop Guard

Purpose:

Protects against Layer 2 loops caused by unidirectional links.

---


# STP Configuration

## Display STP Information

```cisco
show spanning-tree
```

---

## Show Root Bridge

```cisco
show spanning-tree root
```

---

## Configure Root Bridge

Primary Root

```cisco
spanning-tree vlan 1 root primary
```

Secondary Root

```cisco
spanning-tree vlan 1 root secondary
```

---

## Set Bridge Priority

```cisco
spanning-tree vlan 1 priority 4096
```

Default Priority

```text
32768
```

Lowest Bridge ID becomes the Root Bridge.

---

# Verification Commands

```cisco
show spanning-tree

show spanning-tree vlan 1

show spanning-tree root

show spanning-tree interface

show spanning-tree summary
```

---

# Best Practices

- Manually configure the Root Bridge.
- Enable PortFast only on access ports.
- Enable BPDU Guard on all PortFast interfaces.
- Never enable PortFast on trunk ports.
- Monitor STP status regularly.

---

# Quick Summary

## Timers

| Timer | Default |
|--------|----------|
| Hello | 2 s |
| Forward Delay | 15 s |
| Max Age | 20 s |

---

## Port States

Blocking

↓

Listening

↓

Learning

↓

Forwarding

---

## Important Features

- PortFast
- BPDU Guard
- Root Guard
- Loop Guard

---

## Key Commands

```cisco
show spanning-tree
show spanning-tree root
show spanning-tree summary
spanning-tree portfast
spanning-tree bpduguard enable
spanning-tree vlan 1 root primary
```
