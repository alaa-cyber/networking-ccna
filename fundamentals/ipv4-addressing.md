# IPv4 Addressing

---

## What is an IP Address

An IPv4 address is a 32-bit number used to identify a device in a network.

Example:
192.168.1.10

---

## Structure

IPv4 address = 4 octets (8 bits each)

Example:
192.168.1.10
= 11000000.10101000.00000001.00001010

---

## Network vs Host

An IP address is divided into:

- Network part
- Host part

---

## Subnet Mask

Defines which part is network and which part is host.

Example:
255.255.255.0

---

## Example

IP: 192.168.1.10  
Mask: 255.255.255.0

Network: 192.168.1.0  
Broadcast: 192.168.1.255  

Host range:
192.168.1.1 → 192.168.1.254

---

## Key Terms

- Network Address → first IP
- Broadcast Address → last IP
- Host → device in network

---

## Private IP Ranges

- 10.0.0.0 /8
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 /16

---

## Key Idea

IP = identity of device  
Subnet mask = defines network size
