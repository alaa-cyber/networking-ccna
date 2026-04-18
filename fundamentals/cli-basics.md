# CLI Basics (Cisco)

## What is CLI
CLI (Command Line Interface) is used to configure and manage network devices.

---

## Modes

### User EXEC
- Prompt: >
- Limited access

### Privileged EXEC
- Prompt: #
- Full access
- Command:
enable

### Global Configuration
- Prompt: (config)#
- Used to configure device

---

## Basic Commands

enable
configure terminal
hostname Router1
exit

---

## Navigation

- Tab → auto-complete
- ? → help
- Arrow keys → history

---
## Password Security

### enable password vs enable secret

enable password
- Stored in plain text (not secure)

enable secret
- Stored as a hash (encrypted)
- More secure
- Recommended

---

### Password Encryption

service password-encryption

- Encrypts all passwords in configuration
- Prevents passwords from being visible in plain text
- Uses weak encryption (Type 7), but better than nothing

---

### Best Practice

- Always use: enable secret
- Avoid: enable password
- Enable password encryption
- Use strong passwords
## Key Idea
CLI is essential to configure routers and switches.

