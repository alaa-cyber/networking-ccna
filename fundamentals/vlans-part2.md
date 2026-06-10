# VLANs (Part 2) - Trunking

## What is a Trunk Port?

A trunk port is a switch port that carries traffic from multiple VLANs.

Unlike an access port, which belongs to a single VLAN, a trunk can transport traffic from several VLANs simultaneously.

---

## Why Do We Need Trunks?

Imagine:

* VLAN 10 devices connected to SW1
* VLAN 10 devices connected to SW2

If the link between SW1 and SW2 is configured as an access port:

* Only one VLAN can pass

If the link is configured as a trunk:

* VLAN 10
* VLAN 20
* VLAN 30

can all pass through the same physical link.

---

## Access Port vs Trunk Port

| Feature          | Access Port   | Trunk Port        |
| ---------------- | ------------- | ----------------- |
| VLANs            | One VLAN      | Multiple VLANs    |
| Connected To     | PCs, Printers | Switches, Routers |
| Tagging          | No            | Yes               |
| Broadcast Domain | One VLAN      | Multiple VLANs    |

---

## VLAN Tagging

When a frame crosses a trunk link, the switch adds a VLAN tag.

The tag identifies which VLAN the frame belongs to.

Example:

* VLAN 10 frame → tagged VLAN 10
* VLAN 20 frame → tagged VLAN 20
* VLAN 30 frame → tagged VLAN 30

This process is called VLAN tagging.

---

## IEEE 802.1Q

802.1Q is the standard used for VLAN tagging.

It inserts a 4-byte field inside the Ethernet frame.

Information added:

* VLAN ID
* Priority information

---

## Native VLAN

The Native VLAN is special.

Frames belonging to the Native VLAN are sent without a tag.

Default Native VLAN:

VLAN 1

---

## Trunk Configuration

### Configure a Trunk Port

```bash
enable
configure terminal

interface g0/1
switchport mode trunk
```

---

## Change Native VLAN

```bash
interface g0/1
switchport trunk native vlan 99
```

---

## Allow Specific VLANs

```bash
interface g0/1
switchport trunk allowed vlan 10,20,30
```

Only these VLANs can pass through the trunk.

---

## Verification Commands

```bash
show interfaces trunk
show vlan brief
show running-config
```

---

## Important Concepts

### VLAN ID

Unique identifier of a VLAN.

Examples:

* VLAN 10
* VLAN 20
* VLAN 30

---

### Tagged Frame

Frame contains VLAN information.

Used on trunk links.

---

### Untagged Frame

Frame without VLAN tag.

Usually belongs to the Native VLAN.

---

## Common Problems

### Native VLAN Mismatch

Different Native VLANs on both sides of a trunk.

Can cause connectivity issues.

---

### VLAN Not Allowed

A VLAN is not included in:

```bash
switchport trunk allowed vlan
```

Traffic will not pass.

---

### Trunk Not Configured

Port remains in access mode.

Inter-switch VLAN traffic fails.

---

## Key Idea

Access Port:

* One VLAN

Trunk Port:

* Multiple VLANs

---

## Summary

* Trunk links transport multiple VLANs.
* VLAN tagging uses IEEE 802.1Q.
* Native VLAN traffic is untagged.
* Trunks are commonly used between switches and routers.
* `show interfaces trunk` is the main verification command.

```
```
