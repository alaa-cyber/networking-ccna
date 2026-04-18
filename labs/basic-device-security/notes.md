# Basic Device Security Lab

## Topology
- 1 Router (R1)
- 1 Switch (SW1)
- 3 PCs

---

## Objective
Configure basic security on Router and Switch:
- Hostname
- Enable password
- Password encryption
- Save configuration

---

## Router Configuration (R1)
enable
configure terminal

hostname R1

enable password cisco
enable secret class

service password-encryption

exit

write memory

---

## Switch Configuration (SW1)
enable
configure terminal

hostname SW1

enable password cisco
enable secret class

service password-encryption

exit
write memory

---

## Explanation

- hostname → change device name
- enable password → basic access (not secure)
- enable secret → encrypted password (recommended)
- service password-encryption → hides passwords in config
- write memory → saves configuration

---

## Key Notes

- Always use "enable secret" instead of "enable password"
- Encryption type 7 is weak but better than plain text
- Saving configuration is mandatory to keep changes

---
