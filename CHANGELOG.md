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