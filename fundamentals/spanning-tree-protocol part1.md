# Spanning Tree Protocol (STP)

---

# What is STP?

Spanning Tree Protocol (STP) is a Layer 2 protocol that prevents switching loops in Ethernet networks.

It creates a loop-free logical topology while keeping redundant links available for failover.

IEEE Standard:

802.1D

---

# Why is STP Needed?

Redundant links improve network availability.

However, redundant Layer 2 links create switching loops.

Without STP, switches continuously forward Ethernet frames, causing network instability.

---

# Problems Caused by Switching Loops

## Broadcast Storm

Broadcast frames circulate indefinitely.

Result:

- High CPU usage
- Congested links
- Network outage

---

## MAC Address Table Instability

A switch continuously learns the same MAC address from different interfaces.

Result:

- Incorrect forwarding
- Unstable MAC table

---

## Multiple Frame Copies

The same Ethernet frame arrives multiple times.

Result:

- Duplicate packets
- Network congestion

---

# STP Operation

STP blocks redundant links while keeping one active path.

If the active path fails, STP activates the blocked link automatically.

---

# Root Bridge

The Root Bridge is the central switch in the spanning tree.

All path calculations are based on the Root Bridge.

Only one Root Bridge exists per VLAN.

---

# Bridge ID (BID)

Each switch has a Bridge ID composed of:

- Bridge Priority
- MAC Address

Lowest Bridge ID becomes the Root Bridge.

---

# Root Port

Each non-root switch selects one Root Port.

Characteristics:

- Best path to the Root Bridge
- Lowest path cost

Each switch has only one Root Port.

---

# Designated Port

Each network segment elects one Designated Port.

Responsibilities:

- Forward traffic
- Connect the segment to the Root Bridge

---

# Blocked Port

Redundant ports are placed in the Blocking State.

Purpose:

Prevent Layer 2 loops.

---

# Port States (IEEE 802.1D)

Blocking

- Does not forward frames
- Does not learn MAC addresses

Listening

- Exchanges BPDU frames
- Does not learn MAC addresses

Learning

- Learns MAC addresses
- Does not forward frames

Forwarding

- Learns MAC addresses
- Forwards traffic

Disabled

- Administratively shut down

---

# BPDU

Bridge Protocol Data Unit

BPDUs are exchanged between switches to:

- Elect the Root Bridge
- Detect topology changes
- Maintain the spanning tree

---

# Path Cost

STP selects the path with the lowest total cost.

Typical costs:

10 Mbps → 100

100 Mbps → 19

1 Gbps → 4

10 Gbps → 2

---

# STP Convergence

When a topology changes:

- STP recalculates paths
- Selects new forwarding ports
- Blocks redundant links again

---

# Verification Commands

```cisco
show spanning-tree

show spanning-tree vlan 10

show spanning-tree root

show spanning-tree interface
```

---

# Key Concepts

- Prevent Layer 2 loops
- Prevent broadcast storms
- Elect one Root Bridge
- Select one Root Port
- Elect one Designated Port
- Block redundant links

---

# Common Problems

- Wrong Root Bridge
- Broadcast storms
- MAC table instability
- Slow convergence

---

# Best Practices

- Configure the Root Bridge manually.
- Use Rapid STP when possible.
- Monitor BPDU traffic.
- Avoid unnecessary Layer 2 loops.

---

# Summary

STP ensures:

✔ Loop-free topology

✔ Redundant links

✔ Automatic failover

✔ Stable Layer 2 switching
