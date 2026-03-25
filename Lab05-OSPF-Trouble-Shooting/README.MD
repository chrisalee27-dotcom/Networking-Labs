# 🧪 Lab 05 - OSPF Troubleshooting

## 📌 Overview
This lab focuses on troubleshooting common OSPF issues including:
- Missing routes
- Neighbor adjacency problems
- Timer mismatches
- Network type mismatches
- Default route propagation

The goal is to identify, diagnose, and resolve OSPF issues step-by-step using verification commands and logical troubleshooting.

---

## 🗺️ Network Topology

[View Topology](./screenshots/1_topology.png)

---

## ❌ Initial Problem

- Internal network communication is failing

[Ping Failure](./screenshots/0_internal_network_ping_fail.png)

---

## 🔍 Step 1 - Check Routing Table

- Missing routes identified on R1

[Missing Routes](./screenshots/2_r1_missing_routes.png)

---

## 🔍 Step 2 - Verify OSPF Configuration

- Check OSPF process on R2 and R4

[R2 OSPF Config](./screenshots/10_r2_sh_ip_ospf.png)  
[R4 OSPF Config](./screenshots/11_r4_sh_ip_ospf.png)

---

## 🔍 Step 3 - Check Neighbor Adjacency

- Adjacency issues detected between routers

[Neighbor Issue](./screenshots/3_r4_neighbor_adjacency_missing_routes.png)  
[R5 Neighbors](./screenshots/14_r5_neighbors.png)

---

## 🔍 Step 4 - Verify Network Type

- Mismatch between broadcast and point-to-point discovered

[Broadcast Network](./screenshots/4_r4_network_broadcast.png)  
[Point-to-Point Network](./screenshots/5_r3_network_pp.png)

---

## 🛠️ Step 5 - Fix Network Type Mismatch

- Removed incorrect configuration

[Remove Point-to-Point](./screenshots/6_r3_remove_pp.png)

---

## 🔍 Step 6 - Verify OSPF Routes

- Check routing table after fix

[Route Verification](./screenshots/7_r4_ospf_route_verify.png)

---

## 🔍 Step 7 - Check Connectivity

- Ensure devices can communicate

[Connection Check](./screenshots/8_connection_check.png)

---

## 🔍 Step 8 - Identify Missing Neighbors

- Additional neighbor issue detected on R2

[R2 Missing Neighbors](./screenshots/9_r2_missing_neighbors.png)

---

## 🔍 Step 9 - Check OSPF Timers

- Timer mismatch identified

[R5 Timer Settings](./screenshots/12_r5_sh_ip_ospf_timer.png)  
[No Hello Timer](./screenshots/13_no_hello_no_timer.png)

---

## 🛠️ Step 10 - Fix Timer Mismatch

- Restore default Hello/Dead timers

---

## 🔍 Step 11 - Verify External Connectivity

- External ping initially fails

[External Ping Failure](./screenshots/15_pc1_external_ip_ping_fail.png)

---

## 🔍 Step 12 - Check Routing Configuration

- Verify running config on R5

[R5 Running Config](./screenshots/16_r5_sho_run.png)

---

## 🔍 Step 13 - Check Default Route

- Default route missing

[No Default Route](./screenshots/17_r5_no_default_route.png)

---

## 🛠️ Step 14 - Configure Default Route

- Default route added and advertised

[Default Route Configured](./screenshots/18_r5_default_route.png)

---

## 🔍 Step 15 - Verify Route Propagation

- R1 now learns external route

[R1 Learned Route](./screenshots/19_r1_shows_learned_route.png)

---

## 🔍 Step 16 - Final Connectivity Test

- External connectivity restored

[External Ping Success](./screenshots/20_external_ip_ping_verify.png)

---

## 🔍 Step 17 - Verify OSPF Database

- LSDB synchronized across routers

[OSPF Database](./screenshots/21_ospf_database.png)

---

## 🧠 Key Takeaways

- OSPF adjacency issues are often caused by:
  - Network type mismatches
  - Timer mismatches
  - Missing configuration

- FULL adjacency is required for route exchange

- DR/BDR behavior impacts adjacency formation

- Always verify:
  - Neighbor state
  - Routing table
  - OSPF database

---

## 🚀 Skills Practiced

- OSPF troubleshooting methodology
- Interpreting `show ip ospf neighbor`
- Diagnosing adjacency states
- Fixing configuration mismatches
- Verifying end-to-end connectivity

---
