# EXP-04 — Scalability Validation Through Network Expansion



## 1\. Experiment ID

EXP-04



## 2\. Title

Validation of Enterprise Network Scalability Through Addition of a Research VLAN



## 3\. Objective

To determine whether the RC-001 hierarchical enterprise network can accommodate
a new departmental network without disrupting existing routing, segmentation,
infrastructure services, or branch connectivity.



## 4\. Research Question

Can a new departmental VLAN and IP subnet be introduced into the existing
RC-001 architecture while preserving end-to-end connectivity and existing
enterprise services?



## 5\. Hypothesis

If RC-001 is sufficiently modular and scalable, then adding a new Research VLAN
should require only localized Layer 2 and Layer 3 configuration changes while
OSPF dynamically propagates the new subnet to remote sites without disrupting
existing services.



## 6\. Experimental Change

A new departmental network was introduced at headquarters:

* VLAN ID: 70
* VLAN Name: RESEARCH
* Network: 10.10.70.0/27
* Default Gateway: 10.10.70.1
* Test Endpoint: RESEARCH-PC1
* Access Switch: HQ-SW2
* Access Port: Fa0/11

The new VLAN was propagated through the existing trunk infrastructure and
advertised into OSPF Area 0.



## 7\. Variables

### Independent Variable

Addition of VLAN 70 (RESEARCH) and subnet 10.10.70.0/27.

### Dependent Variables

* VLAN availability
* Trunk propagation
* Default-gateway reachability
* OSPF route propagation
* Cross-site connectivity
* Centralized infrastructure reachability
* Existing-service availability

### Controlled Variables

The existing enterprise topology, WAN addressing, OSPF Area 0 design,
departmental VLANs, server network, and branch topology remained unchanged.



## 8\. Procedure

1. Established the existing RC-001 network as the experimental baseline.
2. Created VLAN 70 (RESEARCH) at the headquarters switching layer.
3. Added VLAN 70 to the required 802.1Q trunks.
4. Assigned HQ-SW2 Fa0/11 as an access port for VLAN 70.
5. Created HQ-R1 subinterface G0/0/0.70.
6. Configured 10.10.70.1/27 as the Research VLAN default gateway.
7. Added 10.10.70.0/27 to OSPF Area 0.
8. Configured G0/0/0.70 as an OSPF passive interface.
9. Verified that ACC-R1 and TAK-R1 dynamically learned the new network.
10. Connected and configured RESEARCH-PC1.
11. Tested local gateway, centralized infrastructure, and cross-site connectivity.
12. Performed regression testing against the existing internal DNS/web service.



## 9\. Results

### Layer 2 Expansion

VLAN 70 was successfully created and propagated through the headquarters
trunk infrastructure.

**Result: PASS**

### Layer 3 Gateway

HQ-R1 G0/0/0.70 became operational with address 10.10.70.1/27.

**Result: PASS**

### Dynamic Routing

ACC-R1 and TAK-R1 dynamically learned 10.10.70.0/27 through OSPF with a
route metric of 2.

**Result: PASS**

### Research Endpoint Connectivity

RESEARCH-PC1 successfully reached:

* 10.10.70.1 — Research default gateway
* 10.10.60.11 — centralized DNS server
* 10.20.30.1 — remote Accra network
* 10.30.30.1 — remote Takoradi network

The final connectivity tests showed 0% packet loss.

**Result: PASS**

### Existing-Service Regression Test

An existing HQ client successfully resolved:

intranet.aegis.local → 10.10.60.13

The subsequent connectivity test completed with 0% packet loss.

**Result: PASS**



## 10\. Experimental Observation

The network accommodated the additional departmental subnet without requiring
static route configuration on the branch routers. Once the new subnet was
advertised from HQ, OSPF automatically propagated reachability information to
the Accra and Takoradi routers.

The experiment also demonstrated that the existing trunk and router-on-a-stick
architecture could accommodate an additional VLAN with localized configuration
changes.

A temporary DNS regression was observed during recovery following an
unexpected Packet Tracer application closure. Investigation showed that the
DNS service remained enabled but its resource-record table was empty. The
required A record was restored, after which hostname resolution and service
connectivity passed. This condition was therefore determined to be associated
with saved simulation state rather than the VLAN 70 expansion itself.

## \## 11. Evidence

## 

## Experimental evidence is stored under:

## 

## `Images/M10-Evidence/EXP-04/`

## 

## \### Evidence Files

## 

## 1\. \*\*EXP04-01-VLAN70-Trunk-Verification.png\*\*

## &#x20;  - Confirms VLAN 70 (RESEARCH) is active.

## &#x20;  - Verifies VLAN 70 is propagated across the required headquarters 802.1Q trunks.

## 

## 2\. \*\*EXP04-02-Research-Gateway-OSPF-Verification.png\*\*

## &#x20;  - Confirms HQ-R1 G0/0/0.70 is operational with address 10.10.70.1.

## &#x20;  - Shows 10.10.70.0/27 advertised into OSPF Area 0.

## &#x20;  - Confirms the Research subinterface is configured as an OSPF passive interface.

## 

## 3\. \*\*EXP04-03-ACC-OSPF-Research-Route.png\*\*

## &#x20;  - Confirms ACC-R1 dynamically learned 10.10.70.0/27 through OSPF.

## 

## 4\. \*\*EXP04-04-TAK-OSPF-Research-Route.png\*\*

## &#x20;  - Confirms TAK-R1 dynamically learned 10.10.70.0/27 through OSPF.

## 

## 5\. \*\*EXP04-05-Research-PC1-IP-Gateway-Verification.png\*\*

## &#x20;  - Confirms RESEARCH-PC1 can reach its 10.10.70.1 default gateway.

## &#x20;  - Confirms reachability to the centralized DNS server at 10.10.60.11.

## 

## 6\. \*\*EXP04-06-Research-PC1-Enterprise-Connectivity.png\*\*

## &#x20;  - Confirms successful connectivity from the new Research network to remote enterprise networks.

## &#x20;  - Tests to the Accra and Takoradi destinations completed with 0% packet loss.

## 

## 7\. \*\*EXP04-07-Existing-Intranet-Service-Regression-Pass.png\*\*

## &#x20;  - Confirms the existing hostname `intranet.aegis.local` resolves to 10.10.60.13.

## &#x20;  - Confirms successful connectivity to the existing intranet service after the network expansion.

## 

## \### Evidence Summary

## 

## The evidence demonstrates the complete scalability-validation chain: Layer 2 expansion, Layer 3 gateway integration, dynamic OSPF propagation, endpoint connectivity, cross-site reachability, and successful regression testing of an existing enterprise service.



## 12\. Interpretation

The results support the experimental hypothesis.

RC-001 demonstrated horizontal network extensibility at the departmental level.
A new logical network could be incorporated using the existing VLAN, trunking,
router-on-a-stick, and OSPF architecture while maintaining connectivity to
centralized services and remote sites.

The experiment provides evidence that the architecture is not merely functional
for its original topology but can accommodate controlled expansion without
requiring redesign of the underlying routing architecture.



## 13\. Limitations

The experiment was conducted in Cisco Packet Tracer and therefore does not
measure real-world forwarding performance, convergence under production load,
hardware resource utilization, or application latency.

The experiment validates logical scalability rather than production-scale
performance scalability.



## 14\. Conclusion

EXP-04 successfully demonstrated that RC-001 can incorporate an additional
departmental VLAN and subnet while preserving enterprise routing and existing
service availability.

Overall Result: PASS WITH SCOPE LIMITATION





