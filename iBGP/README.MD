# iBGP

This project demonstrates the configuration of **Border Gateway Protocol (BGP)** in a network topology with multiple Autonomous Systems (ASNs). It also includes traffic engineering using import and export policies to control route preferences and traffic flow.

---

## **Network Topology Overview**

- **Routers and ASNs:**
  - **R1:** ASN 100
  - **R2:** ASN 200
  - **R3:** ASN 300

- **Routing Protocols:**
  - **OSPF** for internal routing.
  - **BGP** for inter-AS communication.

- **Route Advertisement:**
  - Each router advertises its local networks through BGP.

---

## **Scenarios and Configurations**

### **Scenario 1: Traffic Engineering**

#### Objective:
Direct traffic from R3 to R1 via R2 and vice versa.

1. **Import Policy - Local Preference**
   
   Configure R3 to prefer routes via R2.
   
   ```
   neighbor 10.10.2.1 route-map AVOID_R1 in
   neighbor 10.10.3.2 route-map PREFER_R2 in

   route-map PREFER_R2 permit 10
   set local-preference 200

   route-map AVOID_R1 permit 10
   set local-preference 100
   ```

   **Result:**
   - Traffic from R3 to R1 is routed through R2.
   - The BGP routing table reflects the higher local preference for routes via R2.

2. **Export Policy - AS-Path Prepending**

   Configure R3 to make R2 the preferred path for traffic from R1.

   ```
   neighbor 10.10.2.1 route-map PREPEND_R1 out

   route-map PREPEND_R1 permit 10
   set as-path prepend 300 300 300 300
   ```

   **Result:**
   - Traffic from R1 to R3 is also routed through R2.
   - AS-path length manipulation ensures R2 is the preferred path.

---

### **Scenario 2: Prefix Filtering**

#### Objective:
Control the prefixes imported and exported by each router.

1. **Import Policy: Prefix Filtering**

   On R1, accept only `/23` prefixes from neighbors.

   ```
   ip prefix-list ACCEPT_ONLY_23 seq 10 permit 10.0.0.0/23
   route-map IMPORT_POLICY permit 10
   match ip address prefix-list ACCEPT_ONLY_23

   neighbor 10.10.1.2 route-map IMPORT_POLICY in
   ```

   **Result:**
   - Only prefixes with `/23` subnet masks are accepted.

2. **Export Policy: Prefix Filtering**

   On R1, advertise only its local prefixes.

   ```
   ip prefix-list EXPORT_OWN_PREFIX seq 10 permit 10.11.1.0/23
   ip prefix-list EXPORT_OWN_PREFIX seq 20 permit 10.11.1.0/24

   route-map EXPORT_POLICY permit 10
   match ip address prefix-list EXPORT_OWN_PREFIX

   neighbor 10.10.1.2 route-map EXPORT_POLICY out
   ```

   **Result:**
   - R1 advertises only its own prefixes and does not act as a transit router.

---

## **Testing and Verification**

1. **Ping and Traceroute:**
   - Validate connectivity between hosts.
   - Use `traceroute` to confirm traffic paths.

2. **BGP Routing Table:**
   - Run `show ip bgp` to check the BGP routing table and confirm policy application.

3. **Configuration Check:**
   - Use `show running-config` to verify the applied configurations.

---

## **Key Commands Summary**

- **BGP Neighbor Configuration:**
  ```
  neighbor <neighbor_ip> remote-as <asn>
  neighbor <neighbor_ip> route-map <map_name> in|out
  ```

- **Route Map Configuration:**
  ```
  route-map <map_name> permit|deny <sequence_number>
  set local-preference <value>
  set as-path prepend <asn> <asn> <asn>
  match ip address prefix-list <prefix_list_name>
  ```

- **Prefix List Configuration:**
  ```
  ip prefix-list <name> seq <seq_number> permit|deny <prefix>
  ```

---

## **Conclusion**

This configuration demonstrates effective traffic engineering and route control using BGP policies. By manipulating **local preference**, **AS-path prepending**, and **prefix filtering**, traffic flow can be optimized, and network behavior can be fine-tuned to meet specific requirements.

---

Feel free to contribute or report issues related to this project!
