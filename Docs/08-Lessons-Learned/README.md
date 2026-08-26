# \# RC-001 — Lessons Learned

# 

# \## Purpose

# 

# This document records the principal engineering, security, research, and

# project-management lessons derived from the design, implementation,

# verification, and experimental evaluation of RC-001.

# 

# \---

# 

# \## 1. Design Before Configuration

# 

# Developing the requirements, HLD, LLD, IP plan, and architectural decision

# records before completing device configuration provided a structured basis

# for implementation.

# 

# This reduced arbitrary configuration decisions and made later verification

# and troubleshooting easier because implementation choices could be compared

# against documented design intent.

# 

# \### Lesson

# 

# Network implementation is more reproducible when configuration follows an

# explicit engineering baseline rather than being developed directly in the

# simulator.

# 

# \---

# 

# \## 2. Hierarchical and Modular Addressing Improves Scalability

# 

# Separating addressing by site and function simplified routing and network

# expansion.

# 

# During M10, VLAN 70 and the 10.10.70.0/27 Research subnet were introduced

# without renumbering existing networks.

# 

# \### Lesson

# 

# Address space should be allocated with future organizational and site growth

# in mind rather than only satisfying immediate host requirements.

# 

# \---

# 

# \## 3. VLAN Segmentation Requires End-to-End Consistency

# 

# Several early connectivity problems were associated with VLAN and trunk

# configuration.

# 

# Successful segmentation required consistency across:

# 

# \- VLAN creation

# \- access-port assignment

# \- trunk configuration

# \- allowed VLAN lists

# \- native VLAN configuration

# \- router subinterfaces

# \- endpoint addressing

# 

# \### Lesson

# 

# A VLAN should be treated as an end-to-end service path rather than an isolated

# switch configuration.

# 

# \---

# 

# \## 4. Verification Must Occur at Multiple Layers

# 

# A successful ping alone did not provide sufficient evidence that the network

# was correctly engineered.

# 

# RC-001 therefore used commands and tests covering:

# 

# \- interface state

# \- VLAN membership

# \- trunk operation

# \- MAC-address learning

# \- gateway reachability

# \- OSPF neighbors

# \- routing tables

# \- SSH operation

# \- ACL counters

# \- DNS resolution

# \- HTTP services

# 

# \### Lesson

# 

# Strong verification combines control-plane, data-plane, management-plane,

# and application-level evidence.

# 

# \---

# 

# \## 5. Dynamic Routing Provides Observable Recovery Behavior

# 

# EXP-01 demonstrated that OSPF reacted to a controlled WAN interruption by

# removing affected reachability and subsequently restoring routes after the

# link returned.

# 

# \### Lesson

# 

# Dynamic routing should be evaluated not only when the network is healthy but

# also during controlled failure and recovery.

# 

# \---

# 

# \## 6. Positive and Negative Security Testing Are Both Necessary

# 

# Testing only successful SSH access would have demonstrated availability but

# not access-control effectiveness.

# 

# EXP-03 included:

# 

# \- authorized SSH access

# \- unauthorized management-access attempts

# \- ACL counter inspection

# 

# \### Lesson

# 

# Security validation should demonstrate both that authorized activity succeeds

# and that prohibited activity fails for the intended reason.

# 

# \---

# 

# \## 7. Service Reachability and Name Resolution Are Different Tests

# 

# The introduction of centralized DNS and internal HTTP services showed that IP

# connectivity alone does not establish application usability.

# 

# Successful testing required validation of both direct IP reachability and DNS

# name resolution.

# 

# \### Lesson

# 

# Infrastructure services should be tested at the service layer in addition to

# the underlying network layer.

# 

# \---

# 

# \## 8. Regression Testing Is Essential After Network Changes

# 

# The addition of VLAN 70 changed switching, routing, and OSPF configuration.

# 

# After the change, existing enterprise connectivity and intranet services were

# retested.

# 

# \### Lesson

# 

# A change is not fully validated merely because the new function works.

# Previously working services must also be shown to remain operational.

# 

# \---

# 

# \## 9. Requirements Traceability Prevents Overstatement

# 

# The M10 traceability review identified an important distinction between what

# the architecture was designed to support and what was experimentally tested.

# 

# The original EXP-04 requirement proposed future-branch expansion, while the

# implemented experiment introduced a new Headquarters departmental VLAN.

# 

# \### Lesson

# 

# A technically successful experiment should not automatically be described as

# satisfying a requirement if its methodology differs materially from the

# approved requirement.

# 

# The correct engineering response is to document the deviation and classify

# the requirement accordingly.

# 

# \---

# 

# \## 10. Simulation Results Have Boundaries

# 

# Cisco Packet Tracer provides an effective environment for architecture,

# configuration, protocol, and functional testing, but it does not reproduce

# every characteristic of production networks.

# 

# \### Lesson

# 

# Observed convergence times, platform behavior, security capabilities, and

# performance characteristics should not be generalized directly to production

# hardware.

# 

# Simulation limitations should be stated explicitly.

# 

# \---

# 

# \## 11. Documentation Is Part of the Engineering Deliverable

# 

# The project evolved from a functioning topology into a documented engineering

# case study through the use of:

# 

# \- requirements

# \- HLD and LLD

# \- ADRs

# \- IP planning

# \- risk analysis

# \- milestone verification

# \- troubleshooting records

# \- screenshots

# \- experiments

# \- research journal

# \- requirements traceability

# 

# \### Lesson

# 

# A configuration demonstrates that a network can work.

# 

# Documentation and reproducible evidence demonstrate why it was designed that

# way, how it was tested, what failed, what was learned, and what remains

# unresolved.

# 

# \---

# 

# \## 12. Version Control Improves Experimental Discipline

# 

# Git checkpoints allowed documentation, Packet Tracer revisions, experiments,

# and evidence to evolve while retaining project history.

# 

# \### Lesson

# 

# Version control is valuable for network engineering research because it

# provides traceability between implementation changes and documented results.

# 

# \---

# 

# \## Overall Reflection

# 

# RC-001 reinforced that network engineering is not simply the process of

# making devices communicate.

# 

# A defensible engineering workflow requires:

# 

# \*\*requirements → design → implementation → verification → experimentation →

# interpretation → documentation → revision\*\*

# 

# The most important lesson from RC-001 is that limitations and unsuccessful or

# partial validations are valuable engineering results when they are identified,

# explained, and documented rather than hidden.

