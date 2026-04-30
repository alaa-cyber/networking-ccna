# Switch Interfaces

---

## What is a Switch Interface

A switch interface (port) is used to connect devices to the switch.

Example:
Fa0/1, Fa0/2, Gi0/1

---

## Interface Types

### Access Port
- Connects end devices (PCs)
- Belongs to one VLAN

---

## Interface Configuration
---

## Speed and Duplex

- Speed: data rate (10/100/1000 Mbps)
- Duplex:
  - Half duplex → one direction
  - Full duplex → both directions

Default:
- Auto negotiation

---

## Interface Status

Interface can be:

- up/up → working
- down → disabled or no cable
- administratively down → shutdown command applied

---

## Commands
show interfaces status
show ip interface brief
show running-config---

## Key Idea

Switch ports connect devices and must be correctly configured.

---

## Summary

- Access port → connects PCs
- Interfaces must be enabled (no shutdown)
- Check status using show commands

