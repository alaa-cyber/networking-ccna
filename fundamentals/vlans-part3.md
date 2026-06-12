# VLANs (Part 3)

## Native VLAN

### What is a Native VLAN?

On a trunk link, most frames are tagged using IEEE 802.1Q.

However, frames belonging to the Native VLAN are transmitted without a VLAN tag.

---

### Default Native VLAN

By default:

```text
VLAN 1
```

is the Native VLAN on Cisco switches.

---

### Native VLAN Example

Switch 1:

```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 99
```

Switch 2:

```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 99
```

Both sides must use the same Native VLAN.

---

### Native VLAN Mismatch

Example:

SW1:

```bash
switchport trunk native vlan 99
```

SW2:

```bash
switchport trunk native vlan 100
```

Result:

* Connectivity issues
* CDP warnings
* Unexpected traffic behavior

---

### Best Practice

Avoid using VLAN 1 as the Native VLAN.

Use an unused VLAN such as:

```text
VLAN 99
```

or

```text
VLAN 999
```

---

## Layer 3 Switch

### What is a Layer 3 Switch?

A Layer 3 Switch combines:

* Layer 2 Switching
* Layer 3 Routing

in the same device.

---

### Layer 2 Switch

Works with:

```text
MAC Addresses
```

Cannot route traffic between VLANs.

---

### Layer 3 Switch

Works with:

```text
MAC Addresses
IP Addresses
```

Can route traffic between VLANs.

---

## Inter-VLAN Routing

Without routing:

* VLAN 10 cannot reach VLAN 20
* VLAN 20 cannot reach VLAN 30

Because each VLAN is a separate broadcast domain.

---

### Solution

Use:

* Router-on-a-Stick
  OR
* Layer 3 Switch

---

## Router-on-a-Stick vs Layer 3 Switch

| Feature        | Router-on-a-Stick | Layer 3 Switch |
| -------------- | ----------------- | -------------- |
| Routing Device | Router            | Switch         |
| Performance    | Lower             | Higher         |
| Trunk Needed   | Yes               | No             |
| Scalability    | Limited           | Better         |

---

## Switch Virtual Interface (SVI)

SVI = Virtual Interface associated with a VLAN.

Example:

```bash
interface vlan 10
ip address 10.0.0.62 255.255.255.192
no shutdown
```

---

## Enable Routing on Layer 3 Switch

```bash
ip routing
```

This command enables Layer 3 routing functionality.

---

## Example Configuration

### VLAN Creation

```bash
vlan 10
name Engineering

vlan 20
name HR
```

---

### SVI Configuration

```bash
interface vlan 10
ip address 10.0.0.62 255.255.255.192
no shutdown

interface vlan 20
ip address 10.0.0.126 255.255.255.192
no shutdown
```

---

### Enable Routing

```bash
ip routing
```

---

## Verification Commands

```bash
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
```

---

## Key Concepts

### Native VLAN

* Untagged traffic
* Trunk links only
* Same on both sides

---

### SVI

* Virtual Layer 3 interface
* Default gateway for hosts

---

### Layer 3 Switch

* Performs switching and routing
* Supports inter-VLAN communication

---

## Summary

* Native VLAN traffic is untagged.
* Native VLAN should match on both trunk sides.
* Layer 3 switches can route between VLANs.
* SVI provides gateway functionality.
* `ip routing` enables Layer 3 routing.

---

## Key Idea

Layer 2 Switch:

* Switching only

Layer 3 Switch:

* Switching + Routing

```
```
