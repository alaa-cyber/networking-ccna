# The Life of a Packet

---

## What is "Life of a Packet"

It describes how data moves from one device to another across a network.

---

## Main Steps

1. Application creates data
2. Data is encapsulated
3. Sent through network
4. Decapsulated at destination

---


## Example Scenario

PC1 sends data to PC2 in another network:

---

## Step 1: Check Destination

- PC checks if destination is in same network
- If NOT → send to default gateway

---

## Step 2: ARP Process

- PC sends ARP request:
  "Who has gateway IP?"

- Router replies with MAC address

---

## Step 3: Frame Creation

Frame contains:
- Source MAC (PC)
- Destination MAC (Router)
- IP packet inside

---

## Step 4: Routing

Router receives packet:

- Removes Layer 2 frame
- Checks IP destination
- Looks in routing table
- Forwards to next hop

---

## Step 5: Re-encapsulation

Router creates new frame:

- New Source MAC = router
- New Destination MAC = next device

---

## Step 6: Final Delivery

At destination:

- Frame → Packet → Data
- Delivered to application

---

## Key Concepts

- MAC changes at every hop
- IP stays the same (end-to-end)
- Router makes forwarding decisions
- Switch uses MAC only

---

## Summary

PC → Switch → Router → Router → Switch → PC

---

## Key Idea

Encapsulation → Transmission → Decapsulation
