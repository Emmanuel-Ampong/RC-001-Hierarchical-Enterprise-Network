# Research Journal

## Project

RC-001: Hierarchical Enterprise Network Design and Implementation

---

# Entry 1

## Date

July 2026

## Activity

Project planning and scope definition.

## Objectives

* Define network requirements.
* Establish project goals.
* Identify deliverables.

## Observations

A hierarchical architecture appears suitable due to the multi-site nature of the organization.

## Next Steps

Develop high-level architecture.

---

# Entry 2

## Date

July 2026

## Activity

High-Level Design development.

## Objectives

* Define architectural layers.
* Identify site connectivity requirements.

## Observations

The hierarchical model improves scalability and fault isolation.

## Next Steps

Develop Low-Level Design.

---

# Entry 3

## Date

July 2026

## Activity

Low-Level Design development.

## Objectives

* Define IP addressing.
* Define VLAN architecture.
* Define routing strategy.

## Observations

OSPF provides a scalable solution for branch connectivity.

## Next Steps

Implement Packet Tracer topology.

---

# Entry 4

## Date

July 2026

## Activity

Packet Tracer implementation.

## Objectives

* Build topology.
* Configure VLANs.
* Configure routing.

## Observations

Initial connectivity issues were observed due to VLAN trunk configuration.

## Resolution

Trunk ports were reconfigured and validated.

## Next Steps

Conduct testing.

---

# Entry 5

## Date

July 2026

## Activity

Validation testing.

## Objectives

* Verify OSPF.
* Verify SSH.
* Verify connectivity.

## Observations

Network functionality met all defined acceptance criteria.

## Next Steps

Prepare final documentation and presentation.

---

# Lessons Learned

Key lessons from this project include:

* Importance of structured design documentation.
* Benefits of VLAN segmentation.
* Importance of routing protocol validation.
* Need for systematic testing.
* Value of architecture decision records.

---

# Future Research Opportunities

Potential future investigations include:

* IPv6 deployment
* Network automation
* Zero Trust architecture
* Software Defined Networking (SDN)
* Enterprise monitoring and telemetry


---

# Entry 6

## Date

August 2026

## Activity

Dynamic routing implementation and OSPF validation.

## Objectives

* Establish dynamic routing between Headquarters, Accra, and Takoradi.
* Verify OSPF neighbor relationships.
* Confirm propagation of enterprise routes.
* Validate end-to-end inter-site connectivity.

## Observations

OSPF Area 0 successfully established routing relationships between the
enterprise routers. Branch networks were dynamically learned and became
reachable across the modeled WAN.

Routing-table and neighbor-state verification provided stronger evidence than
connectivity testing alone.

## Engineering Insight

A functioning ping verifies reachability at a particular moment, whereas
routing-table and adjacency inspection provides evidence about how that
reachability is being produced.

## Next Steps

Harden and validate the management plane.

---

# Entry 7

## Date

August 2026

## Activity

SSH management-plane implementation and verification.

## Objectives

* Configure SSH Version 2.
* Establish dedicated management addressing.
* Restrict normal remote administration to SSH.
* Verify administrative connectivity.

## Observations

SSHv2 was successfully configured and validated on the managed
infrastructure. Management VLAN 99 provided logical separation between
administrative and normal user traffic.

Packet Tracer behavior introduced some limitations in reproducing
production-equivalent authentication behavior.

## Engineering Insight

Security claims should distinguish between configuration evidence, functional
test evidence, and simulator limitations.

## Next Steps

Introduce and test explicit management-plane access restrictions.

---

# Entry 8

## Date

August 2026

## Activity

Management-plane ACL implementation and security validation.

## Objectives

* Restrict administrative access to approved sources.
* Verify authorized access.
* Verify unauthorized access is denied.
* Corroborate observed behavior using ACL counters.

## Observations

Authorized administrative traffic was permitted while an HR-originated
unauthorized SSH attempt was blocked.

ACL counters provided additional evidence that the configured policy was
responsible for the observed behavior.

## Engineering Insight

Security testing requires both positive and negative cases.

Demonstrating that an authorized user can connect proves availability;
demonstrating that an unauthorized source cannot connect provides evidence
that the security control is enforcing policy.

## Next Steps

Introduce centralized infrastructure services and verify application-level
connectivity.

---

# Entry 9

## Date

August 2026

## Activity

Centralized infrastructure-services implementation.

## Objectives

* Introduce centralized DHCP services.
* Configure DHCP relay where required.
* Implement internal DNS.
* Implement an internal HTTP/intranet service.
* Validate services from representative enterprise endpoints.

## Observations

Centralized services were successfully integrated into the existing routed
and segmented architecture.

DNS A records enabled internal service-name resolution, while the internal
web service demonstrated application-layer connectivity beyond basic ICMP
testing.

Regression testing confirmed continued operation of the underlying network.

## Engineering Insight

Network reachability and service availability are related but distinct.

A host may successfully reach a server IP while DNS, DHCP, or application
services remain incorrectly configured. Service-layer verification is
therefore necessary.

## Next Steps

Move from implementation verification to controlled experimental evaluation.

---

# Entry 10

## Date

August 2026

## Activity

Experimental validation and requirements traceability.

## Objectives

* Evaluate OSPF behavior during WAN failure and recovery.
* Validate departmental VLAN segmentation.
* Evaluate secure administrative access.
* Test architectural scalability.
* Perform regression testing.
* Trace experimental results back to approved requirements.

## Experiments

The following controlled experiments were documented:

* EXP-01 — OSPF Convergence
* EXP-02 — VLAN Segmentation
* EXP-03 — Secure Administration
* EXP-04 — Scalability Validation

## Observations

EXP-01 demonstrated route withdrawal and restoration following a controlled
WAN interruption.

EXP-02 demonstrated departmental VLAN separation, trunk operation, dynamic
MAC learning, and correct endpoint/gateway integration.

EXP-03 demonstrated SSH-based administration, successful authorized access,
blocked unauthorized management access, and ACL-counter corroboration.

EXP-04 demonstrated that VLAN 70 and the Research subnet could be introduced
without renumbering existing networks. OSPF propagated the new network to
remote sites, and existing services remained operational following the
change.

## Requirements Traceability Finding

The M10 traceability review identified that the implemented EXP-04 methodology
did not exactly match the original experimental requirement.

The original requirement proposed adding a future branch. The implemented
experiment instead introduced a new Headquarters departmental VLAN.

The experiment therefore provides evidence of modular scalability but does
not fully validate future-branch expansion.

The associated requirement was classified as PARTIAL rather than overstated
as fully satisfied.

## Engineering Insight

A research result remains valuable when it reveals a limitation or incomplete
validation.

Requirements traceability provides a mechanism for distinguishing between:

* what was designed,
* what was implemented,
* what was tested, and
* what the available evidence actually supports.

## Project Outcome

RC-001 progressed from a network implementation exercise into a documented
engineering and experimental case study incorporating:

* requirements engineering,
* architectural design,
* detailed implementation,
* network verification,
* security hardening,
* infrastructure services,
* controlled experiments,
* regression testing,
* evidence collection, and
* requirements traceability.

## Next Steps

Complete the final documentation and repository audit, establish a release
baseline, and use RC-001 as the foundation for subsequent Project Aegis
research projects.

---

# Final Research Reflection

RC-001 demonstrated that building a functioning enterprise network is only
one stage of network engineering.

The stronger research questions emerged after implementation:

* How does routing react to failure?
* Does segmentation behave as intended?
* Can management policy distinguish authorized from unauthorized access?
* Can the architecture expand without disrupting existing services?
* Do experimental results actually satisfy the requirements they claim to
  validate?

This progression from **BUILD** to **HARDEN** and ultimately to controlled
observation and experimentation establishes the methodological foundation for
the later stages of Project Aegis:

**OBSERVE → DETECT → INVESTIGATE → RESPOND → ADAPT**
