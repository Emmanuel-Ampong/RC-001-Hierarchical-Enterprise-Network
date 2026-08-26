# \# RC-001 — Future Work

# 

# \## Purpose

# 

# This document identifies extensions that could build upon the validated

# RC-001 architecture.

# 

# Future work is separated from completed RC-001 functionality so that proposed

# capabilities are not confused with experimentally verified results.

# 

# \---

# 

# \## 1. Complete Future-Branch Scalability Validation

# 

# The highest-priority follow-up is to close the documented EXP-04 traceability

# gap.

# 

# A future experiment should introduce an additional branch with:

# 

# \- a new site addressing block

# \- branch router

# \- branch switch

# \- user VLAN

# \- management VLAN

# \- point-to-point WAN subnet

# \- OSPF participation

# 

# The experiment should determine whether the new site can be integrated

# without renumbering or redesigning existing sites.

# 

# This would directly evaluate the original future-branch requirement.

# 

# \---

# 

# \## 2. WAN Redundancy and Failure Resilience

# 

# RC-001 currently contains single WAN paths between HQ and the modeled

# branches.

# 

# Future work could introduce:

# 

# \- secondary WAN links

# \- alternate OSPF paths

# \- redundant edge routers

# \- route-cost manipulation

# \- controlled primary-link failures

# 

# This would allow quantitative comparison of convergence and availability under

# redundant and non-redundant designs.

# 

# \---

# 

# \## 3. Multi-Area OSPF

# 

# The current topology uses OSPF Area 0.

# 

# A larger topology could evaluate migration to a multi-area design and compare:

# 

# \- routing-table size

# \- LSDB complexity

# \- convergence behavior

# \- route summarization

# \- operational complexity

# 

# \---

# 

# \## 4. Expanded Security Architecture

# 

# Future security work could extend beyond the current SSH and ACL controls to

# include technologies such as:

# 

# \- centralized AAA

# \- RADIUS or TACACS+

# \- firewall policy

# \- VPN connectivity

# \- IDS/IPS

# \- stronger Layer 2 security

# \- role-based administrative access

# \- Zero Trust-oriented access principles

# 

# These capabilities should be evaluated as new experiments rather than

# retroactively attributed to the RC-001 baseline.

# 

# \---

# 

# \## 5. Monitoring and Telemetry

# 

# A future iteration could introduce centralized operational visibility using:

# 

# \- Syslog

# \- SNMP

# \- NetFlow or comparable flow telemetry

# \- NTP

# \- centralized event collection

# \- availability monitoring

# 

# This would create a foundation for subsequent detection and incident-analysis

# projects within Project Aegis.

# 

# \---

# 

# \## 6. Network Automation

# 

# The manually configured RC-001 environment provides a useful baseline for

# automation research.

# 

# Future work could investigate:

# 

# \- configuration templates

# \- Python-based validation

# \- Ansible

# \- automated configuration backups

# \- compliance checking

# \- automated regression tests

# 

# Results could compare manual and automated approaches in terms of consistency,

# deployment time, and configuration error rates.

# 

# \---

# 

# \## 7. IPv6 and Dual-Stack Operation

# 

# RC-001 currently focuses on IPv4.

# 

# A future extension could introduce IPv6 or dual-stack addressing and evaluate:

# 

# \- IPv6 subnet planning

# \- OSPFv3

# \- management accessibility

# \- service reachability

# \- security-policy equivalence

# \- transition complexity

# 

# \---

# 

# \## 8. Production-Grade Emulation

# 

# Because RC-001 was implemented in Cisco Packet Tracer, selected experiments

# could be reproduced in a higher-fidelity environment such as EVE-NG, GNS3, or

# physical networking equipment.

# 

# This would help distinguish architectural findings from simulator-specific

# behavior.

# 

# \---

# 

# \## 9. Quantitative Experimental Measurement

# 

# Future experiments could collect more formal metrics, including:

# 

# \- convergence duration

# \- packet loss during failure

# \- recovery time

# \- configuration change duration

# \- route-count growth

# \- number of devices affected by a change

# \- security-policy match counts

# 

# Repeated trials would improve the statistical strength and reproducibility of

# the results.

# 

# \---

# 

# \## 10. Security Detection and Response Integration

# 

# RC-001 can serve as a network foundation for subsequent Project Aegis work.

# 

# Future projects can extend the environment from network construction and

# hardening into:

# 

# \*\*OBSERVE → DETECT → INVESTIGATE → RESPOND → ADAPT\*\*

# 

# Possible research directions include telemetry collection, anomaly detection,

# intrusion detection, incident investigation, automated response, and

# resilience against emerging threats.

# 

# \---

# 

# \## Research Direction

# 

# RC-001 establishes a controlled enterprise-network baseline.

# 

# Future work should increasingly shift from asking:

# 

# > Does the network function correctly?

# 

# toward questions such as:

# 

# > How does the network behave under failure, attack, expansion, and defensive

# > intervention?

# 

# That transition provides a pathway from network implementation toward

# repeatable cybersecurity and network-resilience research.

