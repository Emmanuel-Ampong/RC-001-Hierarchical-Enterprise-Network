# Engineering Log

This document records the implementation progress, issues encountered, troubleshooting steps, lessons learned, and engineering decisions made during the development of RC-001.

---



-------------
# Engineering Log

---

## Session 1

**Date:** 27 July 2026

### Objective

Configure VLANs and trunk links.

### Completed Tasks

- Created VLANs on HQ-SW1
- Created VLANs on HQ-SW2
- Created VLANs on ACC-SW1
- Created VLANs on TAK-SW1
- Configured trunk ports
- Verified trunk status

### Issues Encountered

- Native VLAN mismatch
- Router interface was administratively down

### Resolution

- Configured native VLAN 99 on both trunk ports
- Enabled the router interface using `no shutdown`

### Commands Learned

```bash
vlan
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan
show vlan brief
show interfaces trunk
no shutdown
```

### Lessons Learned

- A trunk requires matching encapsulation and native VLAN settings on both ends.
- Physical interfaces must be active before a trunk can come up.

### Next Session

- Configure Router-on-a-Stick on HQ-R1.




# Session 2– Repository Initialization

**Date:** 29 July 2026

## Objective

Initialize the repository using the Aegis Engineering Standard (AES).

## Completed Tasks

- Created repository folder structure.
- Created documentation files.
- Added CHANGELOG.
- Added LICENSE.
- Added .gitignore.

## Issues Encountered

- Initially experienced difficulty creating files in VS Code.
- Lost the original Packet Tracer project because it was not saved before signing out.

## Resolution

- Recreated the repository structure.
- Adopted a version-controlled workflow.
- Introduced frequent Packet Tracer saves after each milestone.

## Lessons Learned

- Always save Packet Tracer projects before exiting.
- Keep documentation synchronized with implementation.
- Commit changes regularly to GitHub.

## Next Session

Rebuild the RC-001 Packet Tracer topology and save it as `RC-001-v0.1.pkt`.

---


# Session 3– Physical Topology Reconstruction (Milestone M2)

**Date:** 2 August 2026

## Milestone

**M2 – Physical Topology Completed**

---

## Objective

Rebuild the physical enterprise network topology after the original Packet Tracer project was lost due to the project not being saved before exiting the application.

---

## Scope

- Headquarters infrastructure
- Accra branch infrastructure
- Takoradi branch infrastructure

---

## Tasks Completed

### Infrastructure Devices

Placed and renamed:

- HQ-R1
- ACC-R1
- TAK-R1
- HQ-SW1
- HQ-SW2
- ACC-SW1
- TAK-SW1

### End Devices

Added and renamed:

**Headquarters**

- HR-PC1
- FIN-PC1
- OPS-PC1
- IT-PC1
- EXEC-PC1

Servers:

- AD-SRV
- DNS-SRV
- FILE-SRV
- WEB-SRV
- BACKUP-SRV

**Accra**

- ACC-PC1
- ACC-PC2

**Takoradi**

- TAK-PC1
- TAK-PC2

---

## Physical Connectivity

Established the following infrastructure links:

- HQ-R1 ↔ HQ-SW1
- HQ-SW1 ↔ HQ-SW2
- HQ-R1 ↔ ACC-R1
- HQ-R1 ↔ TAK-R1
- ACC-R1 ↔ ACC-SW1
- TAK-R1 ↔ TAK-SW1

The topology was recreated according to the validated High-Level Design (HLD) and Low-Level Design (LLD).

---

## Challenges Encountered

- The original Packet Tracer project was lost because the project file had not been saved before signing out.
- Care was required to ensure the reconstructed topology matched the documented design exactly.

---

## Resolution

- Rebuilt the topology using the project documentation as the source of truth.
- Saved the Packet Tracer project immediately after completing the topology.
- Adopted a milestone-based save and version-control workflow.

---

## Files Created

- PacketTracer/RC-001-v0.1.pkt

---

## Validation

- Verified all infrastructure devices were correctly placed.
- Verified device hostnames.
- Verified physical connections matched the approved logical design.

---

## Lessons Learned

- Documentation significantly reduces recovery time after unexpected data loss.
- Saving the Packet Tracer project frequently is essential.
- Maintaining a Git repository alongside engineering documentation provides a reliable project history.

---

## Next Objective

**Milestone M3**

- Configure VLANs
- Configure management VLAN
- Verify VLAN database




# Session 4– VLAN Implementation (Milestone M3)

**Date:** 2 August 2026


**Objective**
Configured the enterprise VLAN structure across headquarters and branch switches.

## Tasks Completed

- Created VLANs 10, 20, 30, 40, 50, 60 and 99.
- Assigned descriptive VLAN names.
- Configured access ports according to the Low-Level Design.
- Verified VLAN creation using `show vlan brief`.

## Validation

- VLAN database verified on all switches.
- Access ports assigned to the correct VLANs.

## Lessons Learned

- Consistent VLAN numbering across sites simplifies management.
- Descriptive VLAN names improve readability and troubleshooting.

## Next Objective

Configure IEEE 802.1Q trunk links between switches and routers.


---

# Session 4 – IEEE 802.1Q Trunk Configuration (Milestone M4)

**Date:** 2 August 2026

## Objective

Implement IEEE 802.1Q trunking across the enterprise network to support inter-VLAN communication.

## Tasks Completed

- Configured trunk links between HQ switches.
- Configured trunk links between routers and access switches.
- Configured native VLAN 99.
- Restricted allowed VLANs to:
  - 10
  - 20
  - 30
  - 40
  - 50
  - 60
  - 99
- Added interface descriptions.
- Saved switch configurations.

## Validation

Verified trunk operation using:

- `show interfaces trunk`

Validated:

- Trunk state
- Encapsulation
- Native VLAN
- Allowed VLANs
- Forwarding VLANs

All four switches successfully passed verification.

## Lessons Learned

- Trunk ports carry multiple VLANs over a single physical connection.
- Matching native VLANs on both ends prevents VLAN mismatch issues.
- Restricting allowed VLANs is a good security and performance practice.
- `show interfaces trunk` is the primary verification command for trunk links.

## Next Objective

Implement Router-on-a-Stick (Inter-VLAN Routing).


## M6 – OSPF Dynamic Routing

**Status:** Complete  
**Date:** 09 August 2026

### Objective
Implement dynamic routing between Headquarters, Accra, and Takoradi using OSPF.

### Implementation
- Configured OSPF process 1 on HQ-R1, ACC-R1, and TAK-R1.
- Deployed all routed networks in OSPF Area 0.
- Assigned deterministic router IDs:
  - HQ-R1: 1.1.1.1
  - ACC-R1: 2.2.2.2
  - TAK-R1: 3.3.3.3
- Advertised local VLAN networks and WAN point-to-point networks.
- Configured LAN-facing subinterfaces as passive OSPF interfaces.
- Established OSPF adjacencies across both WAN links.

### Verification
- HQ-R1 successfully formed FULL OSPF adjacencies with ACC-R1 and TAK-R1.
- ACC-R1 successfully learned HQ and Takoradi networks dynamically.
- TAK-R1 successfully learned HQ and Accra networks dynamically.
- Cross-site endpoint connectivity was verified using ICMP.
- Accra-to-HQ connectivity passed.
- Accra-to-Takoradi connectivity passed.
- Takoradi-to-HQ connectivity passed.
- Takoradi-to-Accra connectivity passed.
- Branch-to-branch traceroute successfully demonstrated the path:
  ACC-PC1 → ACC-R1 → HQ-R1 → TAK-R1 → TAK-PC1.

### Engineering Observations
OSPF successfully transformed the previously isolated site networks into a dynamically routed enterprise network. Remote networks appeared in the routing tables with OSPF (`O`) route codes without requiring individual static routes.

The hub-and-spoke WAN topology causes branch-to-branch traffic to traverse Headquarters.

### Milestone Result
**M6 PASSED – OSPF dynamic routing and enterprise-wide connectivity successfully verified.**