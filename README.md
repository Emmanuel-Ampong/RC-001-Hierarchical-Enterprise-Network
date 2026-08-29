# RC-001 — Secure Hierarchical Enterprise Network

> **Foundation Project of Project Aegis**  
> **Building Toward Proactive Network Defense**

RC-001 is a research-oriented network engineering project focused on the
design, implementation, security hardening, and systematic verification of
a multi-site enterprise network.

The project forms the infrastructure foundation of **Project Aegis**, a
multi-project research and engineering portfolio exploring the progression
from secure network architecture toward observable, measurable, and
increasingly proactive cyber defense.

## Final RC-001 Topology

![RC-001 Enterprise Topology](Images/RC-001-Enterprise-Topology.png)

*Final RC-001 multi-site enterprise topology connecting Headquarters, Accra, and Takoradi following M10 experimental validation and scalability testing.*


---


## Project Status

**Current Status: RC-001 Complete — Final Engineering and Experimental Validation Completed**

| Milestone | Engineering Focus | Status |
|---|---|---|
| M1 | Repository & Engineering Foundation | ✅ Complete |
| M2 | Physical Enterprise Architecture | ✅ Complete |
| M3 | VLAN Segmentation | ✅ Complete |
| M4 | IEEE 802.1Q Trunking | ✅ Complete |
| M5 | Inter-VLAN Routing | ✅ Complete |
| M6 | OSPF Dynamic Routing | ✅ Complete |
| M7 | SSHv2 Management Hardening | ✅ Complete |
| M8 | ACL-Based Security Segmentation | ✅ Complete |
| M9 | Enterprise Infrastructure Services | ✅ Complete |
| M10 | Experimental Validation & Project Closeout | ✅ Complete |

**RC-001 Status: COMPLETE**


## Research / Engineering Question

**How can a multi-site enterprise network be designed, progressively
hardened, and systematically validated while preserving required business
connectivity?**

RC-001 approaches this question through iterative engineering milestones,
controlled configuration changes, positive and negative testing, and
version-controlled technical documentation.

---

## Network Architecture

RC-001 models a geographically distributed enterprise consisting of:

- Headquarters (HQ)
- Accra Branch
- Takoradi Branch

Headquarters provides the primary enterprise infrastructure, including
departmental user networks, server infrastructure, network management, and
WAN connectivity to the branch sites.

The branch networks provide local user connectivity while dynamically
exchanging routes with HQ.

### Current Architecture

```text
                         HEADQUARTERS
                              |
                    Enterprise Core Routing
                              |
             +----------------+----------------+
             |                                 |
         Accra Branch                    Takoradi Branch

The detailed topology is implemented and tested in Cisco Packet Tracer.

During M10 experimental validation, the Headquarters architecture was
extended with VLAN 70 (RESEARCH) and the 10.10.70.0/27 subnet to evaluate
modular network expansion while preserving the existing addressing,
routing, and service architecture.

This expansion formed part of EXP-04 and demonstrated logical scalability
within the implemented three-site architecture. It did not constitute the
deployment of an additional branch.



## Engineering Objectives

### RC-001 was designed to:

- Build a structured multi-site enterprise network.
- Segment users and infrastructure using VLANs.
- Develop a scalable IPv4 addressing architecture.
- Implement IEEE 802.1Q trunking.
- Provide inter-VLAN routing.
- Establish dynamic multi-site routing using OSPF.
- Separate infrastructure management traffic from user traffic.
-  Harden remote network-device administration using SSHv2. 
- Apply least-privilege access controls to the management plane.
- Preserve legitimate business connectivity while enforcing security policy.
- Validate network behavior using repeatable positive and negative tests.
- Evaluate routing resilience, segmentation, secure administration, and
  architectural scalability through controlled experiments.
- Document engineering decisions, troubleshooting, limitations, and results.


### Technologies and Engineering Methods
### Technologies and Engineering Methods

| Technology / Method | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation and validation |
| Cisco IOS | Router and switch configuration |
| VLANs | Logical network segmentation |
| IEEE 802.1Q | VLAN trunking |
| Router-on-a-Stick | Inter-VLAN routing |
| IPv4 / VLSM | Structured addressing |
| OSPF | Dynamic multi-site routing |
| SSH Version 2 | Secure remote-management service |
| Extended IPv4 ACLs | Role-based traffic control |
| DHCP | Dynamic IPv4 host configuration and centralized address allocation |
| DNS | Enterprise name resolution and service discovery |
| HTTP | Internal web-service hosting and application reachability validation |
| Git | Engineering version control |
| GitHub | Technical documentation and portfolio publication |
| Controlled Experiments | Repeatable failure, segmentation, security, and scalability testing |
| Requirements Traceability | Mapping requirements to implementation and experimental evidence |

### Network Segmentation
The enterprise uses dedicated VLANs for different organizational and
infrastructure functions.

HQ includes networks for:

- Human Resources
- Finance
- Operations
- IT
- Executive users
- Servers
- Infrastructure Management
- Research

The Research network was introduced during M10 experimental validation as
VLAN 70 using subnet 10.10.70.0/27. It represents a controlled architectural
extension used to evaluate whether RC-001 could accommodate additional
network segments without renumbering or disrupting the existing addressing,
routing, and service architecture.
Branch sites include operational, IT, and management networks appropriate
to their roles.

This segmentation provides the logical foundation for policy enforcement,
traffic isolation, management-plane protection, and controlled security
validation throughout RC-001.

### Dynamic Routing — OSPF

OSPF provides dynamic route exchange between Headquarters, Accra, and
Takoradi.

Baseline verification included:

- OSPF neighbor formation
- Dynamic route learning
- Inter-site reachability
- Branch-to-HQ communication
- Cross-site management-network reachability

A versioned Packet Tracer checkpoint was retained after successful OSPF
validation.

During M10, EXP-01 extended this verification through a controlled WAN
failure-and-recovery experiment. The HQ-to-Accra WAN path was deliberately
interrupted and the resulting OSPF behavior was observed.

Experimental evidence demonstrated:

- Withdrawal of affected routes following WAN failure
- Loss of reachability associated with the failed path
- OSPF reconvergence after restoration of the WAN connection
- Relearning of the affected routes
- Restoration of end-to-end reachability

EXP-01 therefore provided controlled evidence of OSPF convergence and
recovery behavior within the RC-001 simulated environment.

> **Experimental scope:** These observations validate routing behavior
> within Cisco Packet Tracer and should not be interpreted as measurements
> of production-network convergence time or hardware performance.

A versioned Packet Tracer checkpoint was retained after successful OSPF
validation.

### Secure Management — SSHv2

Infrastructure devices were hardened to support SSH Version 2 for secure
remote administration.

Implemented controls include:

- RSA key generation
- SSH Version 2
- Local privileged administrative authentication
- VTY local authentication
- SSH-only VTY transport
- VTY inactivity timeout
- Telnet restriction
- Management-plane access control

Initial M7 verification confirmed the SSHv2 configuration and demonstrated
that insecure Telnet access was restricted.

During M10, EXP-03 extended this verification through controlled positive
and negative management-access testing.

The experiment included:

- Verification of the SSHv2 device configuration
- Successful SSH access from an authorized management source
- An attempted SSH connection from an unauthorized HR-network source
- Inspection of the management ACL following the access tests

The authorized management source successfully established SSH access,
while the unauthorized HR source was prevented from establishing the
management session. The observed behavior was consistent with the
configured management-plane access-control policy.

ACL inspection provided supporting evidence that traffic matched the
configured security policy; however, cumulative ACL match counters were
not treated as proof that every observed counter increment resulted
exclusively from the individual EXP-03 test attempt.

EXP-03 therefore demonstrated controlled SSH-based administration and
source-based restriction of management access within the RC-001
simulation.

### Simulation Limitation

During the original M7 verification, some Packet Tracer endpoint/switch
client combinations did not provide the required SSH client functionality
for authenticated interactive testing. M7 therefore documented
configuration-level verification and the associated simulation limitation.

M10 EXP-03 subsequently provided an authenticated SSH test from a supported
client path together with an unauthorized-source test and ACL
corroboration.

These results validate logical management-plane behavior within Cisco
Packet Tracer and should not be interpreted as a complete evaluation of
production AAA, device operating-system security, cryptographic strength,
or real-world attack resistance.

## ACL-Based Security Segmentation

M8 introduced source-based access control to protect the enterprise
management plane.

### Security Requirement

Ordinary user networks should not be able to initiate traffic to protected
network-management networks.

Authorized IT networks must retain management connectivity.

Legitimate non-management business traffic should remain operational.

### Implemented Policy
HR ----------------X----> Management
Finance -----------X----> Management
Operations --------X----> Management
Executive ---------X----> Management
Branch Operations -X----> Management

IT ---------------------> Management   ALLOWED
Legitimate Traffic -----> Resources    ALLOWED
Extended IPv4 ACLs were applied close to relevant traffic sources.

### Verification

M8 positive and negative testing confirmed that authorized management
sources retained required access while restricted user networks were
prevented from initiating traffic to protected management destinations.

Regression testing also confirmed that the ACL policy preserved required
non-management business connectivity.

The management-plane policy was subsequently exercised during M10 EXP-03,
where authorized SSH administration succeeded and an unauthorized
HR-originated SSH attempt was blocked.

### M8 Security Validation

Before implementing the ACL policy, a baseline test demonstrated that
ordinary user endpoints could reach infrastructure management networks.

After ACL deployment, the tests were repeated.

### Results

| Test | Expected | Result |
|---|---|---|
| HR → Management | Block | ✅ PASS |
| Finance → Management | Block | ✅ PASS |
| HQ Operations → Management | Block | ✅ PASS |
| Executive → Management | Block | ✅ PASS |
| Accra Operations → Management | Block | ✅ PASS |
| Takoradi Operations → Management | Block | ✅ PASS |
| HQ IT → Management | Allow | ✅ PASS |
| Accra IT → Management | Allow | ✅ PASS |
| Takoradi IT → Management | Allow | ✅ PASS |

ACL hit counters provided router-side evidence that representative deny
and permit ACEs were processing traffic.

Not every individual ACE was exercised during representative testing;
untested individual rules are therefore not claimed as independently
verified.

##  Engineering Methodology

RC-001 follows an iterative engineering workflow:

Requirement
    ↓
Design
    ↓
Implementation
    ↓
Baseline
    ↓
Verification
    ↓
Failure / Unexpected Behavior
    ↓
Troubleshooting
    ↓
Re-test
    ↓
Documentation
    ↓
Versioned Checkpoint
    ↓
Controlled Experimental Evaluation
    ↓
Evidence Collection
    ↓
Requirements Traceability
    ↓
Engineering Conclusion
This approach intentionally distinguishes between:

configured, operational, and verified.

A configuration is not considered evidence of successful security control
operation until its behavior has been tested.
Similarly, an experimental result is not treated as fully supported unless
its observation, retained evidence, scope, and limitations are documented
and traceable to the requirement or engineering question being evaluated.

### Verification Philosophy

Testing includes both positive and negative verification.

Examples:

Authorized IT → Management
Expected: ALLOW
Observed: ALLOW
Result: PASS

Unauthorized HR → Management
Expected: DENY
Observed: DENY
Result: PASS

A failed connection can therefore represent a successful security test
when denial is the intended policy.
A test is evaluated against its expected policy outcome rather than whether
connectivity succeeds. Positive tests verify that required services remain
available, while negative tests verify that prohibited communication is
successfully prevented.

Where applicable, observed behavior is corroborated using device state,
routing information, ACL behavior, service responses, and retained
screenshots. Evidence is interpreted within the documented limitations of
the Cisco Packet Tracer simulation environment.

### Documentation

RC-001 maintains a structured, version-controlled engineering record covering
the complete lifecycle of the project from requirements definition through
experimental validation and project closeout.

Repository artifacts include:

- Network Requirements Specification (NRS)
- High-Level Design (HLD)
- Low-Level Design (LLD)
- Architecture Decision Records (ADRs)
- IPv4 addressing and VLAN design
- Device configuration records
- Implementation documentation
- Verification and acceptance testing
- Requirements traceability
- Controlled experimental validation
- Troubleshooting records
- Lessons learned
- Future-work analysis
- Engineering log
- Research journal
- Risk register
- Test plan
- Change history
- Packet Tracer checkpoints
- Experimental evidence and screenshots

The documentation is intended to preserve not only the final operational
network, but also the engineering reasoning, design decisions, failures,
corrective actions, verification evidence, and experimental observations
behind its evolution.

This provides traceability from requirements and architectural decisions
through implementation, verification, and final experimental evaluation.

### Versioned Network Checkpoints

Major validated states of the network were retained as separate Cisco Packet
Tracer checkpoints throughout the engineering lifecycle.

Representative checkpoints include:

RC-001-v0.3.pkt  → OSPF multi-site routing
RC-001-v0.4.pkt  → SSHv2 management hardening
RC-001-v0.5.pkt  → ACL-based security segmentation
RC-001-v0.6.pkt  → M9 Enterprise Infrastructure Services
RC-001-v0.7.pkt  → M10 Experimental Validation and Scalability Testing

These checkpoints preserve milestone-level network states, support rollback
and regression analysis, and provide reproducible evidence of the network's
evolution through RC-001.

The final v0.7 checkpoint contains the validated M10 state used for the
controlled experiments, including the Research VLAN expansion and associated
routing/service regression testing.

### Repository Structure

RC-001-Hierarchical-Enterprise-Network/
│
├── Configurations/
├── Diagrams/
├── Docs/
├── Experiments/
├── Images/
├── PacketTracer/
├── Presentation/
├── References/
├── results/
│
├── .gitignore
├── CHANGELOG.md
├── Engineering-Log.md
├── LICENSE
└── README.md


### Current Findings

RC-001 has demonstrated several important engineering principles:

#### 1. Connectivity and security are different requirements.

Successful routing alone does not imply appropriate access.

#### 2. Segmentation becomes significantly more useful when combined with
enforceable policy.

#### 3. Security controls require negative testing.

Demonstrating that unauthorized traffic fails can be as important as
demonstrating that legitimate traffic succeeds.

#### 4. Security controls must preserve required operations.

Blocking everything is not equivalent to implementing effective
least-privilege policy.

#### 5. Verification limitations should be documented explicitly.

Results should distinguish between what was configured, what was
observed, and what could not be directly tested.



## M9 — Enterprise Infrastructure Services

M9 extended RC-001 from a secured routed infrastructure into a multi-site enterprise environment providing centralized network services.

### Implemented

- Centralized DHCP using `AD-SRV (10.10.60.10)`
- DHCP relay across routed HQ, Accra, and Takoradi VLANs
- Centralized DNS using `DNS-SRV (10.10.60.11)`
- Internal `aegis.local` namespace
- Internal server name resolution
- Internal web service at `intranet.aegis.local`
- Customized Project Aegis / RC-001 intranet portal
- Multi-site service verification
- Security regression testing

### Key Engineering Finding

Initial DHCP testing failed because the existing M8 inbound ACL policy did not permit DHCP bootstrap traffic before clients obtained valid subnet addresses.

The failure was isolated through relay, reachability, and ACL verification. A narrowly scoped DHCP exception was introduced, after which DHCP succeeded.

Regression testing confirmed that the change restored DHCP functionality while preserving the M8 management-plane security policy.

**M9 Result: VERIFIED**

| M9 | Enterprise Infrastructure Services | ✅ Complete |



## M10 — Experimental Validation and Final Engineering Review

M10 completed the experimental and final engineering validation phase of RC-001.

The milestone included:

- OSPF failure and recovery testing
- VLAN segmentation validation
- Secure-administration testing
- Scalability testing
- End-to-end regression testing
- Requirements traceability
- Documentation consolidation
- Lessons learned
- Future-work definition
- Repository cleanup

Four structured experiments were completed:

- EXP-01 — OSPF Convergence and WAN Recovery
- EXP-02 — VLAN Segmentation
- EXP-03 — Secure Administration
- EXP-04 — Scalability Validation Through Network Expansion

EXP-01 through EXP-03 directly satisfied their experimental objectives.

EXP-04 successfully demonstrated modular departmental expansion through the
addition of VLAN 70 (RESEARCH) and its associated subnet without renumbering
existing production-style networks. However, the original NRS requirement
specified the addition of a future branch.

EXP-04 is therefore recorded as **PASS WITH SCOPE LIMITATION**, while the
associated future-branch requirement remains partially validated.

Collectively, M10 demonstrated controlled OSPF failure and recovery,
departmental segmentation, policy-constrained secure administration, and
modular network expansion within the tested Packet Tracer environment.

The results should be interpreted as evidence of logical and functional
behavior within the simulation environment rather than production-scale
performance validation.

**M10 Status: COMPLETED**


# Project Aegis

RC-001 is the infrastructure foundation of Project Aegis.

Project Aegis is a developing multi-project research and engineering portfolio
exploring the progression from secure network architecture toward observable,
measurable, and increasingly proactive cyber defense.

BUILD
  ↓
HARDEN
  ↓
OBSERVE
  ↓
DETECT
  ↓
INVESTIGATE
  ↓
RESPOND
  ↓
ADAPT

RC-001 established the BUILD and HARDEN foundation through structured
enterprise network design, segmentation, dynamic routing, secure management,
infrastructure services, security policy enforcement, and systematic
experimental validation.

With RC-001 complete, the next phase of Project Aegis will begin extending
the environment toward OBSERVE.

## Next Project — RC-002

RC-002 is planned as the next Project Aegis research and engineering project.

It will build on the validated RC-001 infrastructure and begin exploring
network observability, telemetry, monitoring, and measurable network behavior.

The exact experimental scope, requirements, architecture, and evaluation
methodology will be defined during RC-002 requirements development rather
than assumed in advance.

Future Project Aegis work is expected to progressively investigate areas
including centralized security monitoring, IDS/IPS, detection engineering,
behavioral and anomaly analysis, incident investigation, and response
automation.

These are research directions and planned work; they are not presented as
completed capabilities.

## Project Principle

### Build deliberately. Test systematically. Document transparently.
Defend proactively.

## Author

### Emmanuel Ampong

Research interests:

Network Security
Enterprise Networking
Secure Infrastructure
Detection Engineering
Threat Detection and Response
Proactive Cyber Defense
