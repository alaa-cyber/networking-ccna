# DTP & VTP

## Dynamic Trunking Protocol (DTP)

### Definition

Dynamic Trunking Protocol (DTP) is a Cisco proprietary Layer 2 protocol used to automatically negotiate whether a switch port should operate as an access port or a trunk port.

### DTP Modes

| Mode | Description |
|-------|-------------|
| access | Permanent access port |
| trunk | Permanent trunk port |
| dynamic desirable | Actively requests trunking |
| dynamic auto | Waits for trunk request |
| nonegotiate | Disables DTP negotiation |

---

## Trunk Negotiation

| Port A | Port B | Result |
|---------|---------|--------|
| trunk | trunk | Trunk |
| trunk | dynamic auto | Trunk |
| trunk | desirable | Trunk |
| desirable | desirable | Trunk |
| desirable | auto | Trunk |
| auto | auto | Access |

---

## Configure Trunk

interface g0/1

switchport mode trunk

---

## Configure Access

interface g0/2

switchport mode access

switchport access vlan 10

---

## Disable DTP

interface g0/1

switchport mode trunk

switchport nonegotiate

---

## Verify DTP

show interfaces trunk

show interfaces switchport

---

# VLAN Trunking Protocol (VTP)

## Definition

VTP is a Cisco proprietary protocol used to synchronize VLAN information between switches.

---

## Advantages

- Centralized VLAN management
- Automatic VLAN propagation
- Easier administration

---

## VTP Modes

### Server

- Create VLANs
- Delete VLANs
- Modify VLANs
- Advertise VLAN database

### Client

- Receive VLAN database
- Cannot create VLANs
- Cannot delete VLANs

### Transparent

- Does not synchronize VLAN database
- Can create local VLANs
- Forwards VTP advertisements

---

## VTP Domain

All switches must have:

- Same VTP domain
- Same password (optional)
- Same VTP version

---

## VTP Revision Number

The revision number increases every time the VLAN database changes.

Important:
A switch with a higher revision number can overwrite the VLAN database of the entire network.

---

## Verification Commands

show vtp status

show vlan brief

show interfaces trunk

---

## Best Practices

- Configure access ports manually.
- Disable DTP when unnecessary.
- Use trunk ports only where required.
- Reset VTP revision before adding a switch.
- Prefer VTP Transparent mode in production unless VTP is truly needed.

---

## Comparison

| DTP | VTP |
|------|------|
| Negotiates trunk links | Synchronizes VLAN database |
| Works on interfaces | Works between switches |
| Layer 2 | Layer 2 |
| Cisco proprietary | Cisco proprietary |

---

## Key Points

- DTP creates trunk links.
- VTP distributes VLAN information.
- DTP operates per interface.
- VTP operates for the entire switch.
- DTP and VTP are Cisco proprietary protocols.
