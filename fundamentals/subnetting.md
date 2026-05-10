# Subnetting

---

## What is Subnetting

Subnetting is the process of dividing a network into smaller subnetworks.

Main goals:
- Better organization
- Efficient IP usage
- Reduce broadcast traffic

---

## IPv4 Reminder

IPv4 address = 32 bits

Example:
192.168.1.10

Divided into:
- Network portion
- Host portion

---

# Part 1 — Subnetting Basics

## CIDR Notation

CIDR indicates how many bits belong to the network.

Examples:

/24 = 255.255.255.0  
/25 = 255.255.255.128  
/26 = 255.255.255.192  

---

## Why Subnetting

Without subnetting:
- Large broadcast domains
- Wasted IP addresses

With subnetting:
- Smaller networks
- Better performance
- Easier management

---

## Network Address

- First address in subnet
- Identifies the subnet

Example:
192.168.1.0 /24

---

## Broadcast Address

- Last address in subnet
- Used to reach all devices in subnet

Example:
192.168.1.255

---

## Usable Hosts

Addresses between:
- Network address
- Broadcast address

Example:
/24 → usable hosts:
192.168.1.1 → 192.168.1.254

---

## Borrowing Bits

Subnetting works by borrowing bits from the host portion.

More borrowed bits:
- More subnets
- Fewer hosts

Fewer borrowed bits:
- Fewer subnets
- More hosts

---

## Example

Original network:
192.168.1.0 /24

Borrow 1 bit:

New subnet mask:
/25 = 255.255.255.128

Subnets:

1. 192.168.1.0 /25
2. 192.168.1.128 /25

---

## Key Concepts

- Network = first address
- Broadcast = last address
- Hosts = addresses in between

---

## Quick Rules

/24 = 254 hosts  
/25 = 126 hosts  
/26 = 62 hosts  

Each additional subnet bit:
- doubles the number of subnets
- reduces available hosts

---

# Part 2 — Advanced Subnetting

## Subnet Masks

Subnet mask separates:
- Network portion
- Host portion

Examples:

255.255.255.0   = /24
255.255.255.128 = /25
255.255.255.192 = /26
255.255.255.224 = /27

---

## Number of Hosts

Formula:

2^h - 2

Where:
- h = number of host bits

Example:
/26

32 - 26 = 6 host bits

2^6 - 2 = 62 hosts

---

## Number of Subnets

Formula:

2^s

Where:
- s = borrowed subnet bits

Example:

Original:
/24

New:
/26

Borrowed bits:
26 - 24 = 2

2^2 = 4 subnets

---

## Magic Number

Magic Number =
256 - subnet mask octet

Example:
/26

Mask:
255.255.255.192

256 - 192 = 64

Subnet increments:
0, 64, 128, 192

---

## /26 Example

Network:
192.168.1.0 /24

Subnets:

### Subnet 1
- Network: 192.168.1.0
- Hosts: 192.168.1.1 → 192.168.1.62
- Broadcast: 192.168.1.63

### Subnet 2
- Network: 192.168.1.64
- Hosts: 192.168.1.65 → 192.168.1.126
- Broadcast: 192.168.1.127

### Subnet 3
- Network: 192.168.1.128
- Hosts: 192.168.1.129 → 192.168.1.190
- Broadcast: 192.168.1.191

### Subnet 4
- Network: 192.168.1.192
- Hosts: 192.168.1.193 → 192.168.1.254
- Broadcast: 192.168.1.255

---

# Classful Addressing

## Class A

- First octet: 1 - 126
- Default mask: 255.0.0.0
- CIDR: /8

Example:
10.0.0.1

---

## Class B

- First octet: 128 - 191
- Default mask: 255.255.0.0
- CIDR: /16

Example:
172.16.0.1

---

## Class C

- First octet: 192 - 223
- Default mask: 255.255.255.0
- CIDR: /24

Example:
192.168.1.1

---

## Private IP Ranges

### Class A
10.0.0.0 /8

### Class B
172.16.0.0 – 172.31.255.255

### Class C
192.168.0.0 /16

---

## Quick Identification

| Class | First Octet | Default Mask |
|------|-------------|--------------|
| A | 1 - 126 | /8 |
| B | 128 - 191 | /16 |
| C | 192 - 223 | /24 |

---

## Key Idea

Class A:
- Few networks
- Many hosts

Class C:
- Many networks
- Few hosts

---

# Part 3 — Fast Subnetting & VLSM

## Fast Subnetting Method

1. Identify CIDR
2. Find subnet mask
3. Calculate magic number
4. Determine:
   - Network
   - Broadcast
   - Host range

---

## VLSM (Variable Length Subnet Mask)

VLSM allows using different subnet masks in the same network.

Purpose:
- Optimize IP allocation
- Reduce wasted addresses

---

## VLSM Example

Requirements:
- LAN1 → 60 hosts
- LAN2 → 30 hosts
- LAN3 → 10 hosts

Possible allocation:

- LAN1 → /26
- LAN2 → /27
- LAN3 → /28

---

## Quick Host Table

| CIDR | Hosts |
|------|-------|
| /24 | 254 |
| /25 | 126 |
| /26 | 62 |
| /27 | 30 |
| /28 | 14 |
| /29 | 6 |

---

## Important Rules

- Network = first address
- Broadcast = last address
- Hosts = addresses between them

---

## Common Mistakes

- Using network address as host
- Using broadcast address as host
- Wrong subnet mask
- Forgetting the -2 in host calculation

---

## Key Ideas

More subnet bits:
- More networks
- Fewer hosts

Fewer subnet bits:
- Fewer networks
- More hosts

---

## Summary

Subnetting is essential for:
- Routing
- VLANs
- Network design
- Firewalls
- Cybersecurity
- Efficient IP management
