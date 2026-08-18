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


## M7 – Secure Remote Management with SSH

**Status:** Complete  
**Date:** 09 August 2026

### Objective
Secure the enterprise management plane by enabling SSH Version 2 for remote administration and disabling insecure Telnet access.

### Implementation
- Configured SSH services on all enterprise routers and switches.
- Configured the domain name `aegis.local`.
- Generated RSA key pairs for SSH operation.
- Enforced SSH Version 2.
- Created a local privileged administrative account.
- Configured VTY lines to authenticate against the local user database.
- Restricted VTY access to SSH only.
- Configured a 10-minute VTY inactivity timeout.
- Applied the secure-management baseline to:
  - HQ-R1
  - HQ-SW1
  - HQ-SW2
  - ACC-R1
  - ACC-SW1
  - TAK-R1
  - TAK-SW1

### Verification
- `show ip ssh` confirmed SSH Version 2 operation.
- Management interfaces were reachable locally and across sites.
- Cross-site management traffic successfully traversed the OSPF network.
- Representative Telnet attempts to HQ-R1, ACC-R1, and TAK-R1 were rejected.
- VTY configuration was inspected on HQ-R1 and HQ-SW1.
- `login local` and `transport input ssh` were confirmed.

### Security Validation
Positive verification:
- Management IP reachability: PASS
- SSHv2 service enabled: PASS
- Local VTY authentication configured: PASS

Negative verification:
- Telnet access to HQ-R1: BLOCKED – PASS
- Telnet access to ACC-R1: BLOCKED – PASS
- Telnet access to TAK-R1: BLOCKED – PASS

### Verification Limitation
An authenticated interactive SSH session could not be directly validated because the tested Packet Tracer endpoint/switch client implementation did not provide the required SSH client command.

This limitation does not replace the server-side verification and should remain documented rather than being reported as a successful interactive login.

### Engineering Observation
Secure management requires both reachability and protocol restriction. Successful ICMP reachability to management interfaces demonstrated network availability, while rejected Telnet sessions demonstrated enforcement of the SSH-only VTY policy.

### Milestone Result
**M7 PASSED – SSHv2 secure-management baseline successfully deployed and server-side security controls verified.**



## M8 – ACL-Based Security and Network Segmentation
**Date:** 09 August 2026  
**Status:** Complete

Implemented extended IPv4 ACLs to enforce role-based access to enterprise management networks.

A pre-control baseline demonstrated that user VLANs could initially reach management interfaces across HQ, Accra, and Takoradi.

ACLs were subsequently deployed close to the traffic source on relevant router subinterfaces.

Security policy:
- Authorized IT networks retain management access.
- HR, Finance, Operations, Executive, and branch Operations networks are denied management-plane access.
- Legitimate non-management traffic remains permitted.

Positive and negative testing confirmed successful policy enforcement.

ACL match counters provided router-side evidence that representative permit and deny rules processed traffic as designed.

M8 Result: PASS.

## M9 — Enterprise Infrastructure Services

**Status:** Complete
**Date:** 17 August 2026
**Checkpoint:** RC-001-v0.6

### Objective

Extend RC-001 from a secured multi-site routed network into an operational enterprise environment providing centralized infrastructure services across Headquarters, Accra, and Takoradi.

The milestone focused on centralized DHCP, centralized DNS, an internal application service, and regression testing to ensure that the security controls implemented during M8 remained effective.

### Centralized DHCP Implementation

AD-SRV (`10.10.60.10`) was configured as the centralized DHCP server.

DHCP services were provided to intended user VLANs across:

* Headquarters
* Accra
* Takoradi

Because DHCP broadcast traffic does not traverse routers by default, DHCP relay was configured on appropriate router subinterfaces using:

```text
ip helper-address 10.10.60.10
```

DNS-SRV (`10.10.60.11`) was distributed to DHCP clients as the centralized DNS server.

Server, management, router, and WAN addressing remained static.

### Initial Failure

The first DHCP deployment was tested on HR-PC1.

The client failed to obtain a valid lease and assigned itself an APIPA address from the `169.254.0.0/16` range.

This triggered a structured troubleshooting process.

### Troubleshooting

The following checks were performed:

1. Verified that the HR VLAN router subinterface contained the correct `ip helper-address`.
2. Verified successful IP connectivity between HQ-R1 and AD-SRV.
3. Inspected the inbound `HQ-HR-IN` ACL introduced during M8.
4. Determined that the initial DHCP Discover traffic did not match the existing subnet-based permit entry because the client did not yet possess a valid HR address.
5. Identified the ACL policy as the cause of the failed DHCP bootstrap process.

### Corrective Action

A narrowly scoped DHCP exception was inserted before the existing ACL security rules:

```text
permit udp any eq bootpc any eq bootps
```

The DHCP request was repeated.

HR-PC1 subsequently received:

```text
IPv4 Address:    10.10.10.20
Subnet Mask:     255.255.255.224
Default Gateway: 10.10.10.1
DNS Server:      10.10.60.11
```

The same DHCP-relay architecture was then extended to the remaining intended HQ, Accra, and Takoradi user VLANs.

### Multi-Site DHCP Verification

Centralized DHCP was successfully verified across all three sites.

Representative branch clients successfully received addressing from AD-SRV across the OSPF-routed WAN.

Verification included:

* Valid DHCP-assigned IPv4 address
* Correct subnet mask
* Correct default gateway
* Correct centralized DNS server
* Reachability to local gateway
* Reachability to AD-SRV
* Reachability to DNS-SRV

### Security Regression Testing

After introducing DHCP exceptions, the M8 access-control policy was retested.

Results confirmed:

* Unauthorized HR access to management networks remained blocked.
* Accra Operations access to management networks remained blocked.
* Takoradi Operations access to management networks remained blocked.
* Authorized IT users retained management connectivity.
* Legitimate server and enterprise traffic remained operational.

ACL counters confirmed matches on both:

* DHCP permit entries
* Existing management-network deny entries

This demonstrated that the DHCP correction preserved the least-privilege management security policy.

### Centralized DNS

DNS-SRV (`10.10.60.11`) was configured as the internal centralized DNS service.

The internal namespace used was:

```text
aegis.local
```

A records included:

* `ad.aegis.local` → `10.10.60.10`
* `dns.aegis.local` → `10.10.60.11`
* `files.aegis.local` → `10.10.60.12`
* `intranet.aegis.local` → `10.10.60.13`
* `backup.aegis.local` → `10.10.60.14`

Name resolution was successfully verified from Headquarters, Accra, and Takoradi.

A nonexistent hostname was also tested and correctly failed to resolve, providing negative DNS verification.

### Internal Application Service

WEB-SRV (`10.10.60.13`) was configured as an internal web service.

The internal DNS record:

```text
intranet.aegis.local
```

was mapped to the server.

The default web page was replaced with a customized Project Aegis / RC-001 internal portal.

The portal was successfully accessed by hostname from:

* Headquarters
* Accra
* Takoradi

This verified the complete application-service path:

```text
DHCP
  ↓
DNS
  ↓
Hostname Resolution
  ↓
OSPF Routing
  ↓
HQ Server Network
  ↓
WEB-SRV
  ↓
HTTP Application
```

### Final Verification

Final acceptance testing confirmed:

* Centralized DHCP operational at all three sites
* DHCP relay operational across routed boundaries
* Centralized DNS operational
* Positive DNS resolution operational
* Negative DNS resolution behaved as expected
* Internal HTTP application reachable by hostname
* OSPF routing remained operational
* Management-plane ACL restrictions remained effective
* Authorized IT management access remained available

### Key Engineering Finding

The most significant M9 finding was the interaction between a newly introduced legitimate service and a previously validated security control.

The M8 ACLs were functioning correctly according to their original requirements, but the introduction of DHCP exposed an additional traffic requirement that had not previously existed.

Rather than removing or broadly weakening the ACL, a narrowly scoped exception was implemented and followed by regression testing.

This reinforced an important engineering principle:

> Security controls must evolve with service requirements, but any exception should be narrowly scoped and followed by verification that the original security objective remains intact.

### Milestone Result

**M9 PASSED — centralized DHCP, DNS, and internal application services successfully implemented and verified across the RC-001 enterprise environment while preserving existing routing and security controls.**
