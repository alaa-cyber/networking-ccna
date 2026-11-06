
# Dynamic Routing – CCNA Day 24

## 1. Introduction

Dynamic Routing allows routers to automatically learn and update routes by exchanging routing information with other routers.

Unlike static routing, dynamic routing protocols can adapt to network topology changes.

### Why use Dynamic Routing?

- Automatic route discovery
- Automatic adaptation to network changes
- Better scalability
- Reduced manual configuration
- Redundant paths and failover

---

## 2. Static Routing vs Dynamic Routing

| Static Routing | Dynamic Routing |
|---|---|
| Routes manually configured | Routes learned automatically |
| No routing protocol exchanges | Routers exchange routing information |
| Limited scalability | Better scalability |
| Manual updates after changes | Automatic route recalculation |
| Low protocol overhead | Uses CPU, memory and bandwidth |

**Important:** Static routing is still useful for small networks, default routes and predictable paths.

---

## 3. Types of Dynamic Routing Protocols

Dynamic routing protocols are divided into two major categories:

### IGP – Interior Gateway Protocol

Used to exchange routing information within one Autonomous System (AS).

Examples:

- RIP
- EIGRP
- OSPF
- IS-IS

### EGP – Exterior Gateway Protocol

Used to exchange routing information between Autonomous Systems.

Example:

- BGP (Border Gateway Protocol)

An Autonomous System is a group of networks managed under a common routing policy.

---

## 4. IGP Categories

### Distance Vector

Routers exchange routing information with their neighbors.

Examples:

- RIP
- EIGRP (Advanced Distance Vector)

Characteristics:

- Uses routing information received from neighbors
- Does not require a complete link-state topology database
- Uses metrics to select routes

### Link State

Routers build a topology database of their routing area.

Examples:

- OSPF
- IS-IS

Characteristics:

- Exchanges link-state information
- Builds a Link-State Database (LSDB)
- Calculates shortest paths using SPF (Dijkstra)
- Supports scalable network designs

---

## 5. Dynamic Routing Protocol Comparison

| Protocol | Category | Main Metric |
|---|---|---|
| RIP | Distance Vector | Hop Count |
| EIGRP | Advanced Distance Vector | Bandwidth and Delay |
| OSPF | Link State | Cost |
| IS-IS | Link State | Cost |
| BGP | Path Vector | Path Attributes |

### RIP

- Maximum usable hop count: 15
- 16 hops means unreachable
- Uses hop count as its metric

### EIGRP

- Uses the DUAL algorithm
- Uses bandwidth and delay by default
- Supports rapid convergence

### OSPF

- Open-standard IGP
- Uses the SPF algorithm
- Uses interface costs
- Supports areas

### BGP

- Exterior routing protocol
- Uses path attributes and routing policies
- Commonly used for Internet interdomain routing

---

## 6. Routing Metrics

A metric is a value used by a routing protocol to compare different paths.

Examples:

- Hop Count
- Bandwidth
- Delay
- Cost

Within the same routing protocol, the route with the best metric is generally preferred.

**Note:** Metrics from different routing protocols are not directly comparable.

---

## 7. Administrative Distance (AD)

Administrative Distance indicates how trustworthy a route source is to a Cisco router.

Lower AD = More preferred route source.

| Route Source | Default Cisco AD |
|---|---:|
| Connected | 0 |
| Static | 1 |
| EIGRP Summary | 5 |
| External BGP | 20 |
| Internal EIGRP | 90 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| External EIGRP | 170 |
| Internal BGP | 200 |

### Important Difference

Administrative Distance:

Used to choose between routes learned from different sources.

Metric:

Used to select the best route within a routing protocol.

---

## 8. Route Selection Process

When multiple routes exist, a Cisco router generally:

1. Prefers the longest matching prefix for forwarding packets.
2. Uses Administrative Distance to select between competing route sources for the same prefix.
3. Uses routing protocol metrics to compare routes learned through the same protocol.
4. May install equal-cost routes for load balancing.

### Example

For the same destination prefix:

- OSPF route: AD 110
- RIP route: AD 120

The OSPF route is preferred because it has the lower AD.

---

## 9. Dynamic Routing and Convergence

Convergence is the process through which routers update their routing information after a topology change.

Example:

1. A network link fails.
2. The routing protocol detects the failure.
3. Routers exchange updated information.
4. New best paths are calculated.
5. Routing tables are updated.

Convergence speed depends on the routing protocol, topology and configuration.

---

## 10. Useful Cisco Commands

Display the routing table:

```cisco
show ip route
```

Display the routing protocols:

```cisco
show ip protocols
```

Display interface IP addresses:

```cisco
show ip interface brief
```

Display routing table entries learned through OSPF:

```cisco
show ip route ospf
```

Display routing table entries learned through EIGRP:

```cisco
show ip route eigrp
```

---

## 11. Routing Table Codes

| Code | Meaning |
|---|---|
| C | Connected |
| L | Local |
| S | Static |
| R | RIP |
| D | EIGRP |
| O | OSPF |
| B | BGP |

Example:

```text
O 192.168.10.0/24 [110/20] via 10.0.0.2
```

Explanation:

- O = OSPF
- 192.168.10.0/24 = Destination network
- 110 = Administrative Distance
- 20 = OSPF Metric
- 10.0.0.2 = Next-hop address

---

## 12. Key Concepts to Remember

- Dynamic Routing
- Static vs Dynamic Routing
- IGP vs EGP
- Autonomous System
- Distance Vector
- Link State
- Path Vector
- RIP
- EIGRP
- OSPF
- IS-IS
- BGP
- Routing Metrics
- Administrative Distance
- Longest Prefix Match
- Convergence
- Routing Table
