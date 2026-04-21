# Ethernet Switching Analysis Lab

## Objective
Analyze how frames move in a switched network.

---

## What I observed

- Switch learns MAC addresses
- Broadcast traffic is flooded
- Unicast traffic is forwarded correctly

---

## ARP Behavior

- ARP request is broadcast
- All devices receive it
- Only the target replies

---

## ICMP Behavior

- ping uses ICMP
- successful ping = connectivity working

---

## Key Takeaways

- First communication = flooding (ARP)
- Next communication = direct (MAC learned)
