# Rapid Spanning Tree Protocol (RSTP)

---

# What is RSTP?

Rapid Spanning Tree Protocol (RSTP) is the evolution of the original Spanning Tree Protocol (STP).

IEEE Standard:

802.1w

RSTP provides much faster convergence than the legacy STP (802.1D).

---

# Why RSTP?

Traditional STP convergence can take 30 to 50 seconds.

RSTP typically converges in less than one second on point-to-point links.

Advantages:

- Faster recovery
- Less network downtime
- Better redundancy
- Better performance

---

# STP vs RSTP

| STP | RSTP |
|------|------|
| IEEE 802.1D | IEEE 802.1w |
| 30–50 s convergence | < 1–6 s convergence |
| 5 port states | 3 operational states |
| Slower topology changes | Rapid topology changes |

---

# RSTP Port Roles

## Root Port (RP)

Best path toward the Root Bridge.

One Root Port per non-root switch.

---

## Designated Port (DP)

Forwards traffic for each LAN segment.

---

## Alternate Port (AP)

Backup path toward the Root Bridge.

Immediately replaces the Root Port if needed.

---

## Backup Port (BP)

Backup for another Designated Port on the same shared segment.

Rarely seen in modern switched networks.

---

# RSTP Port States

| State | Learns MAC | Forwards Frames |
|--------|------------|-----------------|
| Discarding | ❌ | ❌ |
| Learning | ✅ | ❌ |
| Forwarding | ✅ | ✅ |

RSTP combines the STP Blocking, Listening and Disabled states into a single **Discarding** state.

---

# RSTP Link Types

## Edge Port

Connected to an end device.

Equivalent to PortFast.

Immediately enters the Forwarding state.

---

## Point-to-Point Port

Full-duplex connection between switches.

Supports rapid convergence.

---

## Shared Port

Half-duplex link.

Uses legacy STP behavior.

Rarely used today.

---

# Proposal / Agreement Process

RSTP introduces a handshake mechanism.

Instead of waiting for timers:

1. Proposal
2. Agreement
3. Immediate transition to Forwarding

This greatly reduces convergence time.

---

# RSTP BPDU

Unlike STP:

Every switch generates BPDUs every Hello Time (2 seconds).

There is no dependence on only the Root Bridge generating configuration BPDUs.

---

# RSTP Timers

Hello Time

- 2 seconds

RSTP relies less on timers and more on synchronization.

---

# RSTP Configuration

Enable Rapid PVST+

```cisco
spanning-tree mode rapid-pvst
```

Enable MST

```cisco
spanning-tree mode mst
```

---

# Verification Commands

```cisco
show spanning-tree

show spanning-tree summary

show spanning-tree root

show spanning-tree vlan 1
```

---

# Comparison

## STP

- Blocking
- Listening
- Learning
- Forwarding
- Disabled

## RSTP

- Discarding
- Learning
- Forwarding

---

# Advantages of RSTP

- Very fast convergence
- Automatic backup paths
- Less downtime
- Better redundancy
- Improved network stability

---

# Best Practices

- Use Rapid PVST+ on Cisco switches.
- Configure the Root Bridge manually.
- Enable PortFast (Edge Ports) only on access interfaces.
- Enable BPDU Guard on Edge Ports.
- Verify STP topology regularly.

---

# Key Commands

```cisco
spanning-tree mode rapid-pvst

show spanning-tree

show spanning-tree summary

show spanning-tree root
```

---

# Key Concepts

- IEEE 802.1w
- Fast convergence
- Proposal / Agreement
- Alternate Port
- Backup Port
- Edge Port
- Discarding State
