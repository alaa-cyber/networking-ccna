# VLANs (Part 1)

## What is a VLAN?

A VLAN (Virtual Local Area Network) is a logical segmentation of a switch.

It allows us to divide one physical switch into multiple logical networks.

---

## Why VLANs?

Without VLANs:
- All devices are in the same broadcast domain
- Broadcast traffic is sent to all devices
- Less security
- Poor network organization

With VLANs:
- Devices are separated logically
- Broadcast domains are reduced
- Security is improved
- Network management becomes easier

---

## Broadcast Domain

A broadcast domain is a group of devices that receive broadcast traffic from each other.

By default, all ports on a switch are in the same broadcast domain.

VLANs create separate broadcast domains.

---

## Default VLAN

On Cisco switches:

- VLAN 1 is the default VLAN
- All switch ports belong to VLAN 1 by default
- VLAN 1 exists automatically
- VLAN 1 cannot be deleted

---

## VLAN Example

Example:

- VLAN 10 → HR Department
- VLAN 20 → IT Department
- VLAN 30 → Finance Department

Devices in different VLANs cannot communicate directly without a router or Layer 3 switch.

---

## Access Port

An access port belongs to only one VLAN.

Example:

interface f0/1
switchport mode access
switchport access vlan 10
