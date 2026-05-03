# Routing Fundamentals

---

## What is Routing

Routing is the process of forwarding packets between different networks.

Routers use IP addresses to make decisions.

---

## Routing Table

A router uses a routing table to decide where to send packets.

Each entry contains:
- Destination network
- Next hop
- Interface

---

## Types of Routes

- Directly Connected → networks connected to router interfaces
- Static Routes → manually configured
- Dynamic Routes → learned automatically

---

## Key Concept

If destination is:
- Same network → send directly
- Different network → send to router

---

## Example

Router R1 knows:

192.168.1.0 → directly connected  
192.168.2.0 → via 10.0.0.2  

---

## Key Idea

Routing = decision making based on IP
