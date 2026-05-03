# Static Routing

---

## What is Static Routing

Static routing is manually configuring routes on a router.

---

## Command Syntax
ip route [destination] [mask] [next-hop]---

## Example
ip route 192.168.2.0 255.255.255.0 10.0.0.2This means:
To reach 192.168.2.0 → send to 10.0.0.2

---

## Types of Static Routes

- Next-hop IP
- Exit interface
- Default route

---

## Default Route
ip route 0.0.0.0 0.0.0.0 10.0.0.1Used when destination is unknown.

---

## Verification Commands
show ip route
show running-config---

## Key Idea

Router needs routes to reach remote networks
