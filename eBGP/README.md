# README: eBGP and iBGP Implementation with Mininet

## Project Description
This project aims to build a network topology involving the implementation of **iBGP (Internal BGP)** and **eBGP (External BGP)** protocols on multiple routers connected within a network using Mininet. The topology consists of three Autonomous Systems (**AS**):

- **AS 100**: R11, R12, R13, R14
- **AS 200**: R21, R22, R23, R24
- **AS 300**: R31, R32, R33, R34

Communication between routers within an AS uses **iBGP** and the OSPF routing protocol, while communication between ASes uses **eBGP**.

## Network Topology
1. **eBGP**
   - R14 (AS 100) ⇔ R22 (AS 200)
   - R23 (AS 200) ⇔ R34 (AS 300)
2. **iBGP and OSPF**
   - Used for internal communication within each AS.

## Script Modification
### File Modified: `ospf-lab.py`
- Routers and interfaces were added to create the specified topology.
- iBGP, eBGP, and OSPF configurations were implemented for each router.
- The script can be executed with the following command:
  ```bash
  sudo python3 ospf-lab.py
  ```
- To enter **Privilege exec mode** for each router:
  ```bash
  ./connect.sh <router name> vtysh
  ```

## Routing Configuration
### iBGP and OSPF (Internal)
Below are the configurations for internal routers within each AS:

#### **Sample OSPF Configuration (R11 in AS 100):**
```
router ospf
 network 10.0.1.0/24 area 0
 network 10.0.2.0/24 area 0
```

#### **Sample iBGP Configuration (R11 in AS 100):**
```
router bgp 100
 neighbor 10.0.1.2 remote-as 100
 neighbor 10.0.2.3 remote-as 100
```

### eBGP (Inter-AS)
Below are the eBGP configurations for routers connecting ASes:

#### **R14 (AS 100) ⇔ R22 (AS 200):**
**R14:**
```
router bgp 100
 neighbor 192.168.1.2 remote-as 200
```
**R22:**
```
router bgp 200
 neighbor 192.168.1.1 remote-as 100
```

#### **R23 (AS 200) ⇔ R34 (AS 300):**
**R23:**
```
router bgp 200
 neighbor 192.168.2.2 remote-as 300
```
**R34:**
```
router bgp 300
 neighbor 192.168.2.1 remote-as 200
```

## Testing
### iBGP
Test connectivity between routers within an AS. Below are the test scenarios:

#### **AS 100**
- C11 > R11
- C11 > R12
- R14 > C11
- R14 > R11

#### **AS 200**
- C21 > R21
- C21 > R22
- R24 > C21
- R24 > R21

#### **AS 300**
- C31 > R31
- C31 > R32
- R34 > C31
- R34 > R31

### eBGP
Test connectivity between ASes through border routers:
- R14 (AS 100) ⇔ R22 (AS 200)
- R23 (AS 200) ⇔ R34 (AS 300)

Use the following commands to verify connectivity and routing:
```bash
show ip bgp
show ip ospf neighbor
```

## Conclusion
This project provides in-depth understanding of:
1. Building a network topology using iBGP, eBGP, and OSPF.
2. Implementing internal (iBGP and OSPF) and inter-AS (eBGP) routing.
3. Utilizing Mininet and FRR (Free Range Routing) for network simulation.

While there were challenges in fully implementing eBGP, the project successfully demonstrates how these protocols can be integrated into a complex network.

