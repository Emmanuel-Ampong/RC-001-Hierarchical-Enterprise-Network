\# RC001-M10 — Experimental Validation



\## Document Information



| Field | Value |

|---|---|

| Project | RC-001 — Secure Hierarchical Enterprise Network |

| Milestone | M10 — Experimental Validation |

| Document ID | RC001-M10 |

| Platform | Cisco Packet Tracer 9.0.0.0810 |

| Status | Completed |

| Author | Emmanuel Ampong |



\---



\## 1. Objective



M10 extended RC-001 from implementation verification into controlled

experimental evaluation.



The milestone evaluated four engineering properties of the network:



1\. OSPF behavior during a simulated WAN failure and recovery.

2\. VLAN-based departmental segmentation.

3\. Secure administrative access and management-plane restrictions.

4\. Scalability of the addressing, switching, and routing architecture.



The experiments were designed to test observable network behavior while

preserving the previously validated RC-001 baseline.



\---



\## 2. Experimental Scope



The following experiments were completed:



| Experiment | Description | Result |

|---|---|---|

| EXP-01 | OSPF Convergence | PASS |

| EXP-02 | VLAN Segmentation | PASS |

| EXP-03 | Secure Administration | PASS |

| EXP-04 | Scalability Validation | PASS WITH SCOPE LIMITATION |



Detailed methodology, observations, results, interpretation, and limitations

are maintained in the individual experiment documents under `/Experiments`.



\---



\## 3. EXP-01 — OSPF Convergence



\### Test



A functioning OSPF environment was first established as the healthy baseline.



The HQ-to-Accra WAN interface was then administratively disabled to simulate a

WAN failure. OSPF adjacency and routing-table behavior were observed during

failure and after restoration of the link.



\### Observations



\- The initial OSPF adjacency was established successfully.

\- The simulated WAN failure caused the affected adjacency to transition down.

\- Routes dependent on the failed adjacency were withdrawn.

\- Restoring the interface caused OSPF adjacency formation to begin again.

\- The neighbor relationship returned to FULL state.

\- OSPF routes were restored.

\- Connectivity was successfully re-established.



\### Result



\*\*PASS\*\*



RC-001 demonstrated dynamic route withdrawal and recovery following a

controlled WAN interruption.



\### Evidence



Evidence is stored under:



`Images/M10-Evidence/EXP-01/`



including healthy baseline, WAN failure, reconvergence, and verified recovery

screenshots.



\---



\## 4. EXP-02 — VLAN Segmentation



\### Test



The Headquarters VLAN architecture was inspected and representative endpoints

were validated to confirm departmental separation and correct gateway

assignment.



Trunk operation and dynamic MAC-address learning were also inspected.



\### Observations



\- Departmental VLANs were present and active.

\- 802.1Q trunks carried the required VLANs.

\- VLAN 99 operated as the management VLAN.

\- Dynamic MAC-address learning occurred across the switched infrastructure.

\- HR and Finance endpoints were assigned to their intended IP networks.

\- Representative endpoints successfully reached their respective gateways.



\### Result



\*\*PASS\*\*



The experiment demonstrated logical Layer 2 segmentation of departmental

networks and correct integration with inter-VLAN routing.



\### Evidence



Evidence is stored under:



`Images/M10-Evidence/EXP-02/`



\---



\## 5. EXP-03 — Secure Administration



\### Test



The management plane was evaluated through SSH configuration verification,

authorized administrative access, unauthorized access testing, and ACL

counter inspection.



\### Observations



\- SSH Version 2 was configured.

\- Authorized SSH management access succeeded.

\- An unauthorized HR-originated SSH attempt was blocked.

\- The management ACL showed matching deny/permit counters consistent with

&#x20; observed traffic.

\- Management access controls therefore produced both positive and negative

&#x20; test evidence.



\### Result



\*\*PASS\*\*



RC-001 demonstrated functional SSH-based administration together with

management-plane access restrictions.



\### Evidence



Evidence is stored under:



`Images/M10-Evidence/EXP-03/`



\---



\## 6. EXP-04 — Scalability Validation



\### Test



A new Headquarters departmental network was introduced:



\- VLAN 70 — RESEARCH

\- New router subinterface/gateway

\- Trunk propagation

\- OSPF advertisement

\- Research endpoint integration



The existing enterprise environment was then regression-tested.



\### Observations



\- VLAN 70 was successfully added to the switching environment.

\- The new Research gateway became operational.

\- OSPF advertised the new network.

\- Accra and Takoradi learned the Research route dynamically.

\- The Research endpoint reached required enterprise infrastructure.

\- Existing intranet/service connectivity remained operational after the

&#x20; expansion.



\### Result



\*\*PASS WITH SCOPE LIMITATION\*\*



The experiment demonstrates modular departmental expansion without

renumbering or redesigning the existing network.



However, the original NRS EXP-04 requirement proposed addition of a future

branch. M10 introduced a new Headquarters VLAN rather than an additional

branch router/site.



The result therefore supports the scalability characteristics of the

architecture but does not constitute complete validation of the original

future-branch experiment.



\### Evidence



Evidence is stored under:



`Images/M10-Evidence/EXP-04/`



\---



\## 7. Regression Assessment



Following M10 changes, previously implemented network functionality was

rechecked.



The validation confirmed continued operation of:



\- Existing VLANs

\- Inter-VLAN routing

\- OSPF routing

\- Branch route learning

\- Centralized DNS

\- Internal HTTP/intranet service

\- Enterprise endpoint connectivity



No observed M10 change required renumbering of existing production-style

subnets.



\---



\## 8. Requirements Traceability



Detailed mapping between the approved RC-001 requirements and implemented

capabilities is maintained in:



`RC001-M10-Requirements-Traceability-Matrix.md`



The traceability review identified one material experimental scope gap:

future-branch expansion remains partially validated because EXP-04 evaluated

departmental rather than site-level expansion.



\---



\## 9. Limitations



The experimental results must be interpreted within the following

constraints:



\- RC-001 is implemented in Cisco Packet Tracer.

\- Timing and convergence behavior should not be interpreted as equivalent to

&#x20; production hardware measurements.

\- The topology does not provide full WAN redundancy.

\- Advanced enterprise security technologies are outside the baseline scope.

\- EXP-04 does not implement a physical/logical fourth branch.

\- Results demonstrate behavior within the modeled RC-001 environment and

&#x20; should not be generalized beyond that environment without further testing.



\---



\## 10. Engineering Assessment



M10 demonstrates that RC-001 is not merely a functioning Packet Tracer

topology. The implemented network can be subjected to controlled changes,

failures, security tests, and expansion while producing observable and

documented engineering outcomes.



The milestone provides evidence of:



\- routing resilience,

\- segmentation,

\- management-plane security,

\- modular scalability,

\- regression testing,

\- experimental documentation, and

\- explicit treatment of simulation limitations.



\---



\## 11. Conclusion



\*\*M10 COMPLETED WITH DOCUMENTED EXP-04 SCOPE LIMITATION\*\*



EXP-01, EXP-02, and EXP-03 directly satisfied their experimental objectives.



EXP-04 successfully demonstrated modular network expansion but only partially

satisfied the original NRS future-branch experiment.



The limitation is retained explicitly in the project record to preserve

requirements traceability and avoid overstating the experimental result.

