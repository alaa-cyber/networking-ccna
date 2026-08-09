# EtherChannel Configuration Lab

## Objective

Configure and verify different EtherChannel technologies:

- Layer 2 EtherChannel using LACP
- Layer 2 EtherChannel using PAgP
- Layer 3 Static EtherChannel
- Trunking over EtherChannel
- Routing over Layer 3 EtherChannel
- EtherChannel load balancing

---

## Topology

![EtherChannel Lab Topology](topology.png)

Networks:

- ASW1 LAN: 172.16.1.0/24
- ASW2 LAN: 172.16.2.0/24
- DSW1 ↔ DSW2: 10.0.0.0/30

---

# Task 1 - LACP EtherChannel

Configure a Layer 2 EtherChannel between ASW1 and DSW1 using LACP.

Physical interfaces:

ASW1:
- G0/1
- G0/2

DSW1:
- G1/0/3
- G1/0/4

Example configuration:

```cisco
interface range g0/1-2
 channel-group 1 mode active
```

DSW1:

```cisco
interface range g1/0/3-4
 channel-group 1 mode active
```

Configure the Port-Channel as a trunk:

```cisco
interface port-channel 1
 switchport mode trunk
```

Verify:

```cisco
show etherchannel summary
show interfaces trunk
```

---

# Task 2 - PAgP EtherChannel

Configure a Layer 2 EtherChannel between ASW2 and DSW2 using PAgP.

ASW2:

```cisco
interface range g0/1-2
 channel-group 2 mode desirable
```

DSW2:

```cisco
interface range g1/0/3-4
 channel-group 2 mode desirable
```

Configure the Port-Channel as a trunk:

```cisco
interface port-channel 2
 switchport mode trunk
```

Verify:

```cisco
show etherchannel summary
show interfaces trunk
```

---

# Task 3 - Layer 3 Static EtherChannel

Configure a Layer 3 EtherChannel between DSW1 and DSW2.

Physical interfaces:

- DSW1 G1/0/1 and G1/0/2
- DSW2 G1/0/1 and G1/0/2

First convert the physical interfaces to routed ports:

```cisco
interface range g1/0/1-2
 no switchport
 channel-group 3 mode on
```

Then configure the logical Port-Channel.

DSW1:

```cisco
interface port-channel 3
 no switchport
 ip address 10.0.0.1 255.255.255.252
```

DSW2:

```cisco
interface port-channel 3
 no switchport
 ip address 10.0.0.2 255.255.255.252
```

Verify:

```cisco
show etherchannel summary
show ip interface brief
```

---

# Task 4 - Configure Routing

Enable routing on the multilayer switches:

```cisco
ip routing
```

DSW1 needs a route toward:

172.16.2.0/24

```cisco
ip route 172.16.2.0 255.255.255.0 10.0.0.2
```

DSW2 needs a route toward:

172.16.1.0/24

```cisco
ip route 172.16.1.0 255.255.255.0 10.0.0.1
```

Verify:

```cisco
show ip route
```

Test connectivity between both networks:

```cisco
ping <destination-IP>
```

---

# Task 5 - Check EtherChannel Load Balancing

Check the default load-balancing method:

```cisco
show etherchannel load-balance
```

The default method can depend on the switch/platform.

---

# Task 6 - Configure IP Load Balancing

Configure EtherChannel to use both source and destination IP addresses:

```cisco
port-channel load-balance src-dst-ip
```

Verify:

```cisco
show etherchannel load-balance
```

---

# EtherChannel Verification

Important commands:

```cisco
show etherchannel summary
show etherchannel load-balance
show interfaces port-channel
show interfaces trunk
show ip interface brief
show ip route
```

---

# Key Concepts Learned

## LACP

IEEE standard.

Modes:

- active
- passive

At least one side must be active.

---

## PAgP

Cisco proprietary.

Modes:

- desirable
- auto

At least one side must be desirable.

---

## Static EtherChannel

No negotiation protocol.

```cisco
channel-group <number> mode on
```

Both sides must be configured manually.

---

## Layer 2 vs Layer 3 EtherChannel

Layer 2:

```text
Physical Interfaces
        ↓
EtherChannel
        ↓
Port-Channel
        ↓
Trunk
```

Layer 3:

```text
Physical Interfaces
        ↓
no switchport
        ↓
EtherChannel
        ↓
Port-Channel
        ↓
IP Address
```

---

# Quick Comparison

| Type | Protocol | Modes |
|---|---|---|
| LACP | IEEE | active / passive |
| PAgP | Cisco | desirable / auto |
| Static | None | on |

---

# Important Lesson

EtherChannel allows multiple physical links to operate as one logical link.

This provides:

- Higher bandwidth
- Redundancy
- Load balancing
- Simplified STP topology
