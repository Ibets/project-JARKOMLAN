# OSPF Single-Area and Multi-Area Routing Lab

This repository contains the configurations and setup for an OSPF (Open Shortest Path First) routing lab experiment. The lab demonstrates the implementation of intra-domain routing using both single-area and multi-area OSPF configurations.

---

## Overview

This project is designed to simulate and analyze the behavior of OSPF in a controlled environment. The experiment uses:

- **Environment:** VirtualBox Ubuntu 22.04 with Mininet and `net101` repository.
- **Routing Software:** FRR (Free Range Routing) version 8.5.4.

### Key Features

1. **Single-Area OSPF Configuration**: All routers operate in a single OSPF area (Area 0).
2. **Multi-Area OSPF Configuration**: Routers are segmented into multiple OSPF areas for scalability and structure.
3. **Network Simulation:** Mininet is used to simulate the network topology.
4. **Routing Verification:** Validate routing with commands like `ping`, `show running-config`, and `sh ip ospf database`.

---

## Topology and Configuration

![Topology](https://github.com/Ibets/project-JARKOMLAN/blob/main/OSPF/images/Picture1.png)

### Single-Area OSPF

All routers are configured to operate within Area 0. Below is an example configuration for a router:

```bash
router ospf
 ospf router-id 1.1.1.1
 network 10.11.1.0/24 area 0
 network 172.16.1.0/24 area 0
exit
```

### Multi-Area OSPF

The network is divided into multiple OSPF areas (Area 1, Area 2, Area 3, etc.) to optimize routing and scalability. Example configuration for a router:

```bash
router ospf
 ospf router-id 1.1.1.1
 network 10.11.1.0/24 area 1
 network 172.16.1.0/24 area 1
exit
```

---

## Steps to Run the Lab

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Ibets/project-JARKOMLAN
   ```
2. **Start the Topology**
   Run the following command to initialize the topology:
   ```bash
   sudo python3 ospf-lab.py
   ```
3. **Access Routers**
   Use the provided script to connect to each router:
   ```bash
   ./connect.sh <router-name> vtysh
   ```
4. **Apply Configuration**
   Enter the configuration mode and paste the appropriate router configuration.

5. **Verify Configuration**
   Use the following commands to ensure proper setup:
   ```bash
   show running-config
   ping <destination>
   sh ip ospf database
   ```

---

## Testing and Results

### Ping Tests
Verify connectivity between clients:

- **Ping C1_1 to C3_1**
- **Ping C1_2 to C2_1**
- **Ping C1_2 to C3_2**

### OSPF Database
Compare OSPF databases using the command:
```bash
sh ip ospf database
```
Observe differences in:

- **Router Link States**
- **Net Link States**
- **Summary Link States**

---

## Observations

### Single-Area vs. Multi-Area

1. **Scalability**: Multi-area OSPF provides better scalability by segmenting the network into smaller areas.
2. **Routing Table Size**: Multi-area OSPF reduces the size of routing tables and database entries within an area.
3. **Performance**: Reduces CPU and memory usage on routers in large networks.

---

## Conclusion

This lab highlights the practical implementation and benefits of OSPF routing in both single-area and multi-area setups. Multi-area OSPF demonstrates its scalability and efficiency in managing larger networks, making it a preferred choice for enterprise-level applications.

---

## References

- [FRR Documentation](https://frrouting.org/)
- [OSPF Routing Protocol Overview](https://www.cisco.com/)
- [Mininet](http://mininet.org/)

---

Feel free to contribute or raise issues in this repository!
