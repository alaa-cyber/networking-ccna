# EtherChannel

---

# What is EtherChannel?

EtherChannel is a Layer 2 (or Layer 3) technology that combines multiple physical Ethernet links into a single logical interface called a Port-Channel.

Instead of using one cable between two switches, multiple links work together as one connection.

---

# Why Use EtherChannel?

Advantages:

- Increased bandwidth
- Link redundancy
- Load balancing
- Simplified management
- Faster convergence with STP

---

# Example

Without EtherChannel

SW1 ---- 1 Gbps ---- SW2

Bandwidth = 1 Gbps

---

With EtherChannel

SW1 == 4 × 1 Gbps == SW2

Logical bandwidth = 4 Gbps

If one cable fails:

Remaining links continue carrying traffic.

---

# Requirements

All physical interfaces must have:

- Same speed
- Same duplex
- Same VLAN configuration
- Same trunk or access mode
- Same native VLAN (if trunk)
- Same allowed VLANs

---

# Port-Channel

Logical interface created from multiple physical interfaces.

Example

Port-Channel1

contains

- Fa0/1
- Fa0/2
- Fa0/3
- Fa0/4

---

# EtherChannel Protocols

## PAgP

Port Aggregation Protocol

Cisco proprietary

Modes:

- desirable
- auto

---

## LACP

Link Aggregation Control Protocol

IEEE 802.3ad (802.1AX)

Works between different vendors.

Modes:

- active
- passive

---

## Static EtherChannel

No negotiation.

Configured manually.

Mode:

```cisco
on
```

---

# PAgP Modes

| Mode | Description |
|------|-------------|
| desirable | Actively negotiates |
| auto | Waits for negotiation |

Negotiation

| Side A | Side B | Result |
|---------|---------|--------|
| desirable | desirable | Success |
| desirable | auto | Success |
| auto | auto | Fail |

---

# LACP Modes

| Mode | Description |
|------|-------------|
| active | Starts negotiation |
| passive | Waits for negotiation |

Negotiation

| Side A | Side B | Result |
|---------|---------|--------|
| active | active | Success |
| active | passive | Success |
| passive | passive | Fail |

---

# Configure Static EtherChannel

```cisco
interface range g0/1-2

channel-group 1 mode on

exit

interface port-channel1

switchport mode trunk
```

---

# Configure PAgP

```cisco
interface range g0/1-2

channel-group 1 mode desirable
```

---

# Configure LACP

```cisco
interface range g0/1-2

channel-group 1 mode active
```

---

# Verification Commands

```cisco
show etherchannel summary

show etherchannel port-channel

show interfaces port-channel

show interfaces trunk

show running-config
```

---

# Load Balancing

EtherChannel does not split one packet across links.

Instead, traffic is distributed using a hash based on:

- Source MAC
- Destination MAC
- Source IP
- Destination IP
- TCP/UDP ports

Each flow follows one physical link.

---

# STP and EtherChannel

STP sees the Port-Channel as one logical link.

Benefits:

- No blocked links inside the EtherChannel
- Faster convergence
- Better bandwidth utilization

---

# Best Practices

- Prefer LACP over PAgP.
- Configure identical settings on all member interfaces.
- Verify Port-Channel status after configuration.
- Use Port-Channels between switches whenever redundancy is required.

---

# Comparison

| Static | PAgP | LACP |
|---------|------|------|
| Manual | Cisco Proprietary | IEEE Standard |
| No negotiation | Negotiation | Negotiation |
| mode on | desirable/auto | active/passive |

---

# Key Commands

```cisco
channel-group 1 mode on

channel-group 1 mode desirable

channel-group 1 mode active

show etherchannel summary

show interfaces port-channel
```

---

# Key Concepts

- EtherChannel
- Port-Channel
- PAgP
- LACP
- Static EtherChannel
- Load Balancing
- Link Redundancy
- Increased Bandwidth
