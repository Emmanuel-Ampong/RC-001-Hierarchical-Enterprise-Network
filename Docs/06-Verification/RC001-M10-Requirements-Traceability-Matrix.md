\# RC001-M10 — Requirements Traceability Matrix



\## Document Information



| Field | Value |

|---|---|

| Project | RC-001 — Secure Hierarchical Enterprise Network |

| Document | M10 Requirements Traceability Matrix |

| Source Requirements | RC001-NRS-001 v1.0 |

| Purpose | Trace approved requirements to design, implementation, verification, and evidence |

| Status | Final Validation |

| Author | Emmanuel Ampong |



\---



\# 1. Purpose



This Requirements Traceability Matrix maps the approved RC-001 requirements

baseline to the implemented network, verification artifacts, experiments, and

observed results.



The matrix distinguishes between:



\- \*\*PASS\*\* — requirement directly implemented and verified

\- \*\*PASS — Enhancement\*\* — baseline requirement satisfied and subsequently

&#x20; extended beyond the original scope

\- \*\*PARTIAL\*\* — design intent is supported, but the exact requirement has not

&#x20; been fully demonstrated

\- \*\*N/A / Constraint\*\* — requirement describes an intentional limitation,

&#x20; deferred capability, or design constraint



Later enhancements are not retroactively presented as original baseline

requirements.



\---



\# 2. Functional Requirements



| ID | Requirement | Implementation | Verification / Evidence | Status | Notes |

|---|---|---|---|---|---|

| FR-01 | Multi-site Layer 3 connectivity between Kumasi HQ, Accra, and Takoradi | HQ-R1 connected to ACC-R1 and TAK-R1 using routed WAN links | OSPF verification, cross-site ping tests, M6 verification | PASS | All three enterprise sites participate in the routed architecture |

| FR-02 | Headquarters departments shall use separate VLANs and IP subnets | VLANs 10, 20, 30, 40, 50, 60, and 99 implemented | EXP-02 VLAN segmentation evidence | PASS | Departmental segmentation verified |

| FR-03 | Layer 3 communication between required VLANs | Router-on-a-stick using HQ-R1 802.1Q subinterfaces | Gateway tests and inter-VLAN validation | PASS | Routing occurs through HQ-R1 |

| FR-04 | HQ and branch users shall reach centralized server resources | Centralized Server VLAN 60 at HQ | Server reachability tests; M9 DNS/web validation | PASS — Enhancement | M9 extended this with DHCP, DNS, and internal HTTP services |

| FR-05 | Enterprise WAN shall use OSPF | OSPF process 1, Area 0 | `show ip ospf neighbor`, route tables, EXP-01 | PASS | Dynamic route learning and recovery verified |

| FR-06 | Routers and switches shall support SSH Version 2 | SSHv2 configured on managed infrastructure | M7 verification and EXP-03 | PASS | Authorized SSH administration demonstrated |

| FR-07 | Dedicated management VLANs/IP addresses | VLAN 99 implemented at HQ and branches | Management-interface verification and M8 security testing | PASS | Management traffic logically separated |

| FR-08 | Standardized infrastructure naming | HQ-R1, HQ-SW1, HQ-SW2, ACC-R1, ACC-SW1, TAK-R1, TAK-SW1 | Configuration review | PASS | Naming convention applied consistently |

| FR-09 | Addressing shall support current use and reasonable growth | Site-based modular addressing and VLSM | IP plan and EXP-04 departmental expansion | PASS | VLAN 70 added without renumbering existing networks |

| FR-10 | Architecture shall support future branch addition without complete redesign | Repeatable branch architecture and modular site addressing | Design documentation supports future branch pattern | PARTIAL | Architecture supports the requirement conceptually, but M10 EXP-04 added a new HQ VLAN rather than a fourth branch |



\---



\# 3. Non-Functional Requirements



| ID | Requirement | Implementation | Verification / Evidence | Status | Notes |

|---|---|---|---|---|---|

| NFR-01 | Scalability through modular addressing, dynamic routing, and repeatable branch patterns | Site-based addressing, OSPF, hierarchical topology | IP plan, OSPF validation, EXP-04 | PASS | Departmental expansion demonstrated; branch expansion remains conceptual |

| NFR-02 | Maintainability through consistent hostnames, VLAN IDs, descriptions, addressing, and documentation | Standardized naming, VLAN numbering, documented addressing and interface roles | Repository audit and configuration review | PASS | Documentation substantially supports maintainability |

| NFR-03 | Stable operation under normal conditions | Validated routing, VLANs, services, and management | M10 baseline integrity and regression tests | PASS | Full redundancy intentionally not implemented |

| NFR-04 | Reduce broadcast domains and appropriately size WAN links | VLAN segmentation and /30 point-to-point WAN networks | EXP-02 and IP plan | PASS | Logical broadcast-domain reduction implemented |

| NFR-05 | SSH administration, management separation, unused-port shutdown where practical | SSHv2, VLAN 99, switch hardening | EXP-03 and configuration review | PASS | Some implementation details are platform-dependent |

| NFR-06 | Network shall be understandable, reproducible, and troubleshootable | HLD, LLD, ADRs, IP plan, engineering logs, verification reports | Documentation audit | PASS | Repository contains structured engineering artifacts |

| NFR-07 | Complete engineering documentation set | NRS, HLD, LLD, ADRs, IP plan, risk register, test plan, configs, screenshots, experiments, journal | Repository structure review | PASS | M10 completes the experimental layer |



\---



\# 4. Security Requirements



| ID | Requirement | Implementation | Verification / Evidence | Status | Notes |

|---|---|---|---|---|---|

| SR-01 | Telnet shall not be used for normal remote administration | SSH-only remote management configuration | M7 / EXP-03 | PASS | SSH used for administration |

| SR-02 | SSH Version 2 shall be enabled | `ip ssh version 2` | EXP03-01 | PASS | SSHv2 operational |

| SR-03 | Local administrative credentials shall use supported password protection | Local usernames with IOS `secret` mechanism | Configuration verification | PASS | Credentials excluded from published evidence |

| SR-04 | Management traffic shall use dedicated management VLANs | VLAN 99 | Management verification and ACL testing | PASS | Dedicated management addressing implemented |

| SR-05 | Departmental networks shall use separate VLANs/subnets | VLANs 10–60 | EXP-02 | PASS | Segmentation verified |

| SR-06 | Unused switch access ports should be shut down where practical | Switch hardening applied during implementation | Configuration review | PASS | Requirement is qualified by “where practical” |

| SR-07 | Device banners shall identify authorized-access-only infrastructure | IOS banners configured during hardening | Configuration documentation | PASS | Verify during final configuration archive if needed |

| SR-08 | Published documentation shall not expose plaintext administrative passwords | Evidence and repository avoid plaintext credentials | Repository review | PASS | Password hashes/secrets should also be excluded from portfolio screenshots where possible |

| SR-09 | Advanced ACL/firewall/AAA/VPN/Zero Trust enforcement shall be treated as future enhancements | ACL-based management protection introduced later in M8 | M8 verification and EXP-03 | PASS — Enhancement | ACL implementation is documented as a later scope enhancement rather than part of the original baseline |



\---



\# 5. Routing Requirements



| ID | Requirement | Implementation | Verification / Evidence | Status | Notes |

|---|---|---|---|---|---|

| RR-01 | OSPF shall be the internal dynamic routing protocol | OSPF process 1 | M6 and EXP-01 | PASS | |

| RR-02 | Single-area OSPF using Area 0 | All RC-001 OSPF networks in Area 0 | OSPF running configuration | PASS | |

| RR-03 | Branch LANs shall be advertised into OSPF | Accra and Takoradi LANs advertised | HQ route table | PASS | |

| RR-04 | HQ VLAN networks shall be advertised into OSPF | HQ VLAN subnets advertised | Branch route tables | PASS | VLAN 70 subsequently added during M10 |

| RR-05 | WAN point-to-point networks shall participate in OSPF | 10.255.0.0/30 and 10.255.0.4/30 | OSPF neighbor establishment | PASS | |

| RR-06 | Design shall permit future multi-area evolution | Current architecture uses modular site networks and Area 0 | Design review | PASS | Future capability; multi-area OSPF not implemented |



\---



\# 6. VLAN Requirements



\## Headquarters



| VLAN | Required Purpose | Implemented | Verification | Status |

|---:|---|---|---|---|

| 10 | Human Resources | HR | EXP-02 | PASS |

| 20 | Finance | FINANCE | EXP-02 | PASS |

| 30 | Operations | OPERATIONS | VLAN verification | PASS |

| 40 | Information Technology | IT | VLAN verification | PASS |

| 50 | Executive/Management | EXECUTIVE | VLAN verification | PASS |

| 60 | Servers | SERVERS | M9 infrastructure-services validation | PASS |

| 99 | Network Management | MANAGEMENT | M7/M8 verification | PASS |



\### Additional M10 VLAN



| VLAN | Purpose | Classification |

|---:|---|---|

| 70 | RESEARCH | M10 scalability experiment / scope expansion |



\## Branches



| Requirement | Implementation | Status |

|---|---|---|

| Branch user VLAN | Implemented at Accra and Takoradi | PASS |

| VLAN 99 management network | Implemented at branch sites | PASS |

| Consistent VLAN documentation | Addressing and configurations documented | PASS |



\---



\# 7. Technology and Device Constraints



| Requirement Area | Baseline Requirement | Implementation | Status |

|---|---|---|---|

| Simulation platform | Cisco Packet Tracer 9.0.0.0810 | Packet Tracer used | PASS |

| Routers | Cisco ISR 4331 | HQ-R1, ACC-R1, TAK-R1 | PASS |

| Switches | Cisco Catalyst 2960 | HQ-SW1, HQ-SW2, ACC-SW1, TAK-SW1 | PASS |

| IP protocol | IPv4 | IPv4 addressing throughout | PASS |

| Routing | OSPF | OSPF Area 0 | PASS |

| Trunking | IEEE 802.1Q | Operational switch trunks | PASS |

| Administration | SSH Version 2 | SSHv2 operational | PASS |



Packet Tracer-specific feature differences are treated as simulation

limitations rather than production-equivalent behavior.



\---



\# 8. Device Requirements



| Device Type | Required Devices | Implementation | Status |

|---|---|---|---|

| Routers | HQ-R1, ACC-R1, TAK-R1 | Present and configured | PASS |

| Switches | HQ-SW1, HQ-SW2, ACC-SW1, TAK-SW1 | Present and configured | PASS |

| AD server | AD-SRV | Present as centralized server role | PASS |

| DNS server | DNS-SRV | DNS service implemented | PASS — Enhancement |

| File server | FILE-SRV | Present as centralized server role | PASS |

| Web server | WEB-SRV | Internal HTTP service implemented | PASS — Enhancement |

| Backup server | BACKUP-SRV | Present as centralized server role | PASS |



\---



\# 9. Naming Convention



| Requirement | Verification | Status |

|---|---|---|

| `<SITE>-<DEVICE-TYPE><NUMBER>` infrastructure naming | HQ-R1, HQ-SW1, ACC-R1, TAK-R1, etc. | PASS |

| Server names identify service role | DNS-SRV, FILE-SRV, WEB-SRV, BACKUP-SRV, AD-SRV | PASS |



\---



\# 10. Testing Requirements



| Test Requirement | Verification Artifact | Status |

|---|---|---|

| VLAN creation | M3 / EXP-02 | PASS |

| Access-port assignment | VLAN verification | PASS |

| Trunk establishment | M4 / EXP-02 | PASS |

| Inter-VLAN routing | M5 / EXP-02 | PASS |

| OSPF neighbor establishment | M6 / EXP-01 | PASS |

| OSPF route learning | M6 / EXP-01 | PASS |

| HQ-to-branch connectivity | M6/M9/M10 testing | PASS |

| Branch-to-HQ connectivity | M6/M9 testing | PASS |

| Server reachability | M9 | PASS |

| Management connectivity | M7/M8/EXP-03 | PASS |

| SSH login functionality | M7 / EXP-03 | PASS |

| Route recovery after simulated WAN interruption | EXP-01 | PASS |



\---



\# 11. Experimental Requirements



| ID | NRS Requirement | M10 Experiment | Status | Traceability Note |

|---|---|---|---|---|

| EXP-01 | Investigate OSPF recovery following simulated WAN failure | Controlled HQ–Accra link shutdown and restoration | PASS | Exact requirement directly tested |

| EXP-02 | Evaluate VLAN segmentation compared with flat LAN behavior | VLAN, trunk, MAC-learning, and separate endpoint subnet validation | PASS | Logical broadcast-domain segmentation demonstrated |

| EXP-03 | Compare secure SSH administration with insecure/plaintext administration conceptually or through simulation | SSHv2 operational verification plus authorized/unauthorized management-access tests | PASS | Secure administration directly demonstrated; Telnet comparison primarily represented by configuration/policy rather than live plaintext session |

| EXP-04 | Evaluate how easily addressing/routing can accommodate an additional branch | Addition of HQ VLAN 70 RESEARCH and propagation through OSPF | PARTIAL | Demonstrates modular expansion, but does not implement an actual fourth branch as specified by the original NRS |



\---



\# 12. Acceptance Criteria



| # | Acceptance Criterion | Evidence | Status |

|---:|---|---|---|

| 1 | All required infrastructure devices configured | Router/switch/server implementation | PASS |

| 2 | Required VLANs exist and are assigned correctly | M3 / EXP-02 | PASS |

| 3 | Trunks operate correctly | M4 / EXP-02 | PASS |

| 4 | Inter-VLAN routing functions | M5 / EXP-02 | PASS |

| 5 | OSPF neighbors form successfully | M6 / EXP-01 | PASS |

| 6 | Intended internal routes appear in routing tables | M6 / EXP-01 / EXP-04 | PASS |

| 7 | Branch users can reach required centralized infrastructure | M9 verification | PASS |

| 8 | SSH management works | M7 / EXP-03 | PASS |

| 9 | No Telnet dependency required | SSH-only administration | PASS |

| 10 | Testing evidence captured | Verification reports and screenshot evidence | PASS |

| 11 | Implemented topology matches LLD or deviations documented | Design documentation and engineering logs | PASS |

| 12 | Experimental observations and conclusions published | EXP-01 through EXP-04 documents | PASS WITH NOTE |



\*\*Acceptance Criterion 12 Note:\*\* Four experiments have been documented and

published. However, EXP-04 deviated from the original experiment definition by

testing departmental expansion rather than implementing an additional branch.

This deviation is explicitly recorded rather than being presented as an exact

fulfillment of the original EXP-04 definition.



\---



\# 13. Scope Enhancements Beyond Baseline NRS



The following capabilities were introduced after the original RC001-NRS-001

baseline and are therefore classified as controlled enhancements rather than

retroactively treated as original requirements.



| Enhancement | Milestone | Status |

|---|---|---|

| Extended ACL-based management-network restrictions | M8 | Implemented and verified |

| Positive/negative access-control testing | M8 | Implemented and verified |

| Centralized DHCP | M9 | Implemented and verified |

| DHCP relay | M9 | Implemented and verified |

| Centralized DNS | M9 | Implemented and verified |

| Internal HTTP/intranet service | M9 | Implemented and verified |

| VLAN 70 — RESEARCH | M10 | Implemented and verified |

| Research endpoint integration | M10 | Implemented and verified |



\---



\# 14. Identified Traceability Gap



\## EXP-04 / FR-10 — Future Branch Expansion



The original NRS defined branch expansion as a formal scalability objective

and specified EXP-04 as an evaluation of how easily the addressing and routing

design could accommodate an additional branch.



M10 demonstrated modular expansion by introducing VLAN 70 and subnet

10.10.70.0/27 at Headquarters. The experiment proved that:



\- Existing addressing did not require renumbering.

\- Existing trunks accommodated an additional VLAN.

\- The router-on-a-stick architecture accommodated another subinterface.

\- OSPF propagated the new subnet dynamically.

\- Remote branch routers learned the new network without local configuration.

\- Existing infrastructure remained operational following the expansion.



However, an actual fourth branch router, branch LAN, WAN link, and site block

were not implemented.



Therefore:



\*\*FR-10 / EXP-04 Status: PARTIAL\*\*



This is documented as a traceability gap rather than being overstated as a

fully completed requirement.



\---



\# 15. Overall Traceability Assessment



RC-001 satisfies the large majority of its approved baseline functional,

technical, routing, VLAN, security, testing, and documentation requirements.



The project also exceeds several baseline requirements through later

implementation of ACL-based management restrictions, centralized DHCP,

centralized DNS, internal HTTP services, and controlled network expansion.



The primary remaining traceability gap is the exact EXP-04 future-branch

experiment defined in RC001-NRS-001.



\## Overall Assessment



\*\*SUBSTANTIALLY COMPLIANT — ONE DOCUMENTED PARTIAL REQUIREMENT\*\*



The implementation is suitable for final engineering review provided that the

EXP-04 deviation remains explicitly documented or is closed through a future

fourth-branch scalability experiment.

