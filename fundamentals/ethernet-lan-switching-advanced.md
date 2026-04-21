# Ethernet LAN Switching (Advanced)

---

## Minimum Frame Size

- Minimum Ethernet frame = 64 bytes
- Minimum payload = 46 bytes

### Why?
To detect collisions in the network

---

## Ethernet Frame Recap

Frame structure:

- Preamble
- SFD
- Destination MAC
- Source MAC
- Type
- Data (payload)
- FCS

---

## ARP (Address Resolution Protocol)

### Role
Maps IP address → MAC address

### Process

1. ARP Request (Broadcast)
   - "Who has 192.168.1.10?"

2. ARP Reply (Unicast)
   - "I am 192.168.1.10"

---

## ICMP (Internet Control Message Protocol)

### Role
Used for diagnostics and error messages

### Example
- ping command
- echo request / reply

---

## Key Difference

- ARP → finds MAC from IP
- ICMP → tests connectivity

---

## Key Idea

Switch works with MAC  
ARP helps find MAC  
ICMP helps test network
