# Changelog

All notable changes to RC-001 will be documented in this file.

## [Unreleased]

### Added

- Engineering log
- Network requirements specification
- High-Level Design
- Low-Level Design
- IP addressing plan
- Architecture Decision Records
- Initial Packet Tracer project structure

### Configured

- Enterprise VLAN design
- IEEE 802.1Q trunking plan

### Fixed

- Native VLAN mismatch between headquarters switches
- Disabled router interface preventing trunk activation

## v0.2.0 – Physical Topology

### Added

- Rebuilt complete enterprise physical topology
- Added routers, switches, PCs and servers
- Recreated inter-site WAN links
- Saved Packet Tracer project (RC-001-v0.1.pkt)

### Documentation

- Updated Engineering Log
- Standardized project documentation structure


## v0.4.0 – IEEE 802.1Q Trunking

### Added

- Configured enterprise trunk links.
- Configured native VLAN 99.
- Restricted allowed VLANs.
- Added trunk interface descriptions.

### Verified

- Trunk state
- Allowed VLANs
- Native VLAN
- Forwarding VLANs

## M6 – OSPF Dynamic Routing – 2026-08-09

### Added
- OSPF process 1 on HQ-R1, ACC-R1, and TAK-R1.
- OSPF Area 0 backbone.
- Explicit OSPF router IDs.
- Dynamic advertisement of enterprise LAN and WAN networks.
- Passive OSPF configuration on LAN-facing subinterfaces.
- Dynamic inter-site route propagation.

### Verified
- HQ-to-branch OSPF neighbor adjacencies.
- OSPF route learning across all three sites.
- HQ-to-branch connectivity.
- Branch-to-HQ connectivity.
- Branch-to-branch connectivity through HQ.
- End-to-end ICMP communication.
- Accra-to-Takoradi forwarding path using traceroute.

### Status
M6 completed successfully.


## M7 – Secure Remote Management – 2026-08-09

### Added
- SSH Version 2 management across enterprise routers and switches.
- RSA-based SSH support.
- Local privileged administrator authentication.
- VTY session inactivity timeout.
- SSH-only remote management policy.

### Security
- Disabled Telnet access through VTY transport restrictions.
- Restricted remote CLI management to SSH.
- Verified management reachability across OSPF-routed sites.
- Confirmed representative Telnet connections were rejected.

### Verification
- SSHv2 status verified.
- HQ-R1 and HQ-SW1 VTY configurations inspected.
- Cross-site management connectivity verified.
- Interactive SSH client validation documented as a Packet Tracer limitation.

### Status
M7 completed successfully.


## M8 – ACL-Based Security Segmentation – 2026-08-09

### Added
- Extended IPv4 ACLs for management-plane protection.
- Role-based access policy for enterprise management networks.
- HQ departmental access-control policies.
- Accra and Takoradi Operations access controls.

### Security
- Restricted unauthorized user access to management VLANs.
- Preserved authorized IT management access.
- Preserved legitimate business and server connectivity.
- Applied least-privilege network segmentation principles.

### Verification
- Performed pre-control baseline testing.
- Performed positive authorized-access testing.
- Performed negative unauthorized-access testing.
- Verified ACL deny and permit hit counters.

### Status
M8 completed successfully.

## [v0.6] — M9 Enterprise Infrastructure Services — 2026-08-17

### Added
- Centralized DHCP service hosted on AD-SRV (`10.10.60.10`)
- DHCP relay across HQ, Accra, and Takoradi user VLANs
- Centralized DNS service hosted on DNS-SRV (`10.10.60.11`)
- Internal `aegis.local` DNS namespace
- Internal DNS A records for core enterprise servers
- Project Aegis / RC-001 internal web portal
- Internal application access through `intranet.aegis.local`
- M9 infrastructure-services verification report

### Changed
- Migrated intended end-user networks from static addressing to centralized DHCP
- Distributed `10.10.60.11` as the DNS server through DHCP
- Updated selected M8 inbound ACLs to permit DHCP bootstrap traffic
- Preserved static addressing for servers, management infrastructure, router interfaces, and WAN links

### Fixed
- Resolved DHCP failure caused by interaction between DHCP bootstrap traffic and existing M8 inbound ACL policy
- Added narrowly scoped UDP BOOTPC-to-BOOTPS exceptions before applicable management-network restrictions

### Verified
- Centralized DHCP operation across Headquarters, Accra, and Takoradi
- Cross-WAN DHCP relay through the OSPF-routed network
- Correct DHCP addressing, subnet masks, gateways, and DNS assignment
- Centralized DNS resolution across all three sites
- Expected failure of nonexistent internal DNS names
- HTTP access to `intranet.aegis.local` from all three sites
- OSPF routing remained operational
- Unauthorized user access to management networks remained blocked
- Authorized IT management access remained permitted
- ACL counters recorded both DHCP permit and management-deny matches

### Engineering Finding
The introduction of centralized DHCP exposed an interaction with the previously validated M8 access-control policy. The issue was isolated through relay, reachability, and ACL verification. A narrowly scoped DHCP exception restored service while subsequent regression testing confirmed that the original management-plane security objective remained intact.

### Checkpoint
- `RC-001-v0.6.pkt`
