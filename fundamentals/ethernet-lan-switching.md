# Ethernet LAN Switching

## What is a Switch

A switch is a Layer 2 device that connects devices inside a LAN.

It uses MAC addresses to forward frames.

---

## MAC Address

- Unique identifier for each device
- 48 bits (12 hexadecimal digits)
- Example: 00:1A:2B:3C:4D:5E

---

## Ethernet Frame

An Ethernet frame contains:

1. Preamble
2. SFD (Start Frame Delimiter)
3. Destination MAC
4. Source MAC
5. Type / Length
6. Data (Payload)
7. FCS (Frame Check Sequence)

---

## How a Switch Works

### 1. Learning
- Switch learns MAC addresses
- Stores them in MAC address table

### 2. Forwarding
- Sends frame to correct port if MAC known

### 3. Flooding
- If destination unknown → send to all ports

---

## MAC Address Table

Switch keeps a table:

MAC → Port

Example:
PC1 → Fa0/1  
PC2 → Fa0/2  

---

## Key Idea

Switch = MAC-based forwarding device

---

## Important Concepts

- Unicast → one device
- Broadcast → all devices
- Unknown unicast → flooding

---

## Summary

- Switch works at Layer 2
- Uses MAC addresses
- Learns and forwards traffic intelligently
