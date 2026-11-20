
# CCNA  – OSPF

## 1. Introduction to OSPF

OSPF stands for Open Shortest Path First.

OSPF is a dynamic routing protocol used to exchange routing information between routers.

### Main Characteristics

- Interior Gateway Protocol (IGP)
- Link-State Routing Protocol
- Open Standard
- Uses the Shortest Path First (SPF) algorithm
- Uses cost as its routing metric
- Supports classless routing (CIDR/VLSM)
- Supports hierarchical network design using areas
- Administrative Distance: 110 (Cisco)

OSPFv2 is primarily used for IPv4 routing.
OSPFv3 supports IPv6 and can also support IPv4 through extensions.

---

## 2. Distance Vector vs Link-State

| Feature | Distance Vector | Link-State |
|---|---|---|
| Examples | RIP, EIGRP (advanced distance vector) | OSPF, IS-IS |
| Network knowledge | Routes learned from neighbors | Link-state topology information |
| Algorithm | Protocol-dependent | SPF (Dijkstra) |
| Updates | Protocol-dependent | LSAs exchanged and flooded |
| Metric | Protocol-dependent | OSPF cost |

OSPF routers build a Link-State Database (LSDB) and use the SPF algorithm to calculate the best routes.

---

## 3. OSPF Areas

OSPF uses areas to organize networks.

### Backbone Area

Area 0 is the OSPF backbone area.

In a normal multi-area OSPF design, non-backbone areas must connect logically to Area 0.

### Single-Area OSPF

All OSPF routers belong to one area, commonly Area 0.

### Multi-Area OSPF

Routers are organized into multiple areas to improve scalability.

### Router Types

- Internal Router: All OSPF interfaces belong to one area.
- Backbone Router: Has an interface in Area 0.
- ABR: Area Border Router, connects multiple areas.
- ASBR: Autonomous System Boundary Router, redistributes routes from another routing domain.

---

## 4. OSPF Router ID

The Router ID (RID) is a 32-bit identifier written in dotted-decimal notation.

Example:

1.1.1.1

### Router ID Selection (Cisco IOS)

1. Manually configured OSPF Router ID
2. Highest IPv4 address on an active loopback interface
3. Highest IPv4 address on an active physical interface

Example:

```cisco
router ospf 1
 router-id 1.1.1.1
```

Note: A router ID change may require restarting the OSPF process to take effect.

---

## 5. OSPF Cost

OSPF selects routes based on the total cost of the path.

Cisco's traditional default calculation:

Cost = Reference Bandwidth / Interface Bandwidth

Default reference bandwidth: 100 Mbps.

### Examples

| Interface | Bandwidth | Default Cost |
|---|---|---|
| Ethernet | 10 Mbps | 10 |
| FastEthernet | 100 Mbps | 1 |
| GigabitEthernet | 1000 Mbps | 1 |
| 10 GigabitEthernet | 10000 Mbps | 1 |

With the traditional default reference bandwidth, FastEthernet and faster interfaces can have the same cost.

### Change Reference Bandwidth

```cisco
router ospf 1
 auto-cost reference-bandwidth 100000
```

The value is expressed in Mbps.

Configure a consistent reference bandwidth on all OSPF routers.

### Manual Interface Cost

```cisco
interface g0/0
 ip ospf cost 10
```

---

## 6. OSPF Neighbor Relationships

OSPF routers discover neighbors using Hello packets.

Important requirements for adjacency include:

- Compatible area IDs
- Compatible Hello and Dead timers
- Compatible authentication settings
- Compatible area parameters
- Appropriate IP addressing and network connectivity

Some requirements depend on the OSPF network type.

### Default Hello and Dead Timers

On common broadcast and point-to-point OSPF networks:

Hello Interval: 10 seconds

Dead Interval: 40 seconds

These defaults are not universal for every OSPF network type.

---

## 7. OSPF Packet Types

| Type | Name | Purpose |
|---|---|---|
| 1 | Hello | Discover and maintain neighbors |
| 2 | Database Description (DBD) | Summarize LSDB contents |
| 3 | Link-State Request (LSR) | Request LSAs |
| 4 | Link-State Update (LSU) | Send LSAs |
| 5 | Link-State Acknowledgment (LSAck) | Acknowledge LSAs |

OSPF uses IP Protocol Number 89.

OSPFv2 multicast addresses:

224.0.0.5 – AllSPFRouters

224.0.0.6 – AllDRouters

---

## 8. Basic OSPF Configuration

### Enable OSPF

```cisco
enable
configure terminal
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
```

Explanation:

`router ospf 1`

Creates or enters OSPF process 1.

The process ID is locally significant and does not need to match on neighboring routers.

`network 192.168.1.0 0.0.0.255 area 0`

Enables OSPF on matching interfaces and assigns them to Area 0.

### Alternative Interface Configuration

```cisco
interface g0/0
 ip ospf 1 area 0
```

This enables OSPF directly on the interface.

---

## 9. OSPF Verification Commands

```cisco
show ip protocols
show ip ospf
show ip ospf interface brief
show ip ospf neighbor
show ip ospf database
show ip route ospf
show ip route
```

### Important Route Codes

O – OSPF intra-area route

O IA – OSPF inter-area route

O E1 – OSPF external type 1

O E2 – OSPF external type 2

---

## 10. Key Concepts to Remember

- OSPF = Open Shortest Path First
- OSPF is a Link-State IGP
- SPF algorithm = Dijkstra
- Administrative Distance = 110
- Metric = Cost
- Backbone Area = Area 0
- OSPF IP Protocol Number = 89
- Router ID = Unique 32-bit identifier
- Hello packets = Neighbor discovery
- LSDB = Link-State Database
- LSA = Link-State Advertisement
- ABR = Area Border Router
- ASBR = Autonomous System Boundary Router

---

## 11. CCNA Review Questions

1. What type of routing protocol is OSPF?
2. Which algorithm does OSPF use?
3. What is the administrative distance of OSPF?
4. What is the purpose of Area 0?
5. How does Cisco IOS select the OSPF Router ID?
6. What is the difference between an ABR and an ASBR?
7. What is the default OSPF reference bandwidth?
8. What are the five OSPF packet types?
9. What is the difference between O and O IA routes?
10. What command displays OSPF neighbors?

---

## 12. Conclusion

OSPF is a scalable link-state routing protocol.

It uses LSAs to build a topology database and calculates shortest paths using the SPF algorithm.

Understanding OSPF areas, router IDs, costs, and neighbor relationships is essential for CCNA and network troubleshooting.
