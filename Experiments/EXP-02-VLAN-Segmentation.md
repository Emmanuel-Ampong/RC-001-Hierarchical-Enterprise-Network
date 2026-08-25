# EXP-02 — VLAN Segmentation

## 1. Objective

Evaluate whether the RC-001 Headquarters network implements logical
Layer-2 segmentation using VLANs while providing Layer-3 gateway
connectivity through the enterprise routing architecture.

## 2. Research Question

Does the RC-001 VLAN architecture maintain distinct logical Layer-2
network segments while providing appropriate Layer-3 gateway connectivity?

## 3. Environment

- Platform: Cisco Packet Tracer
- Site: Headquarters
- Access/Distribution Switch: HQ-SW1
- Router: HQ-R1
- Representative VLANs:
  - VLAN 10 — HR
  - VLAN 20 — FINANCE
- Representative endpoints:
  - HR-PC1
  - FIN-PC1

## 4. Baseline Architecture

HQ-SW1 reported the following active enterprise VLANs:

- VLAN 10 — HR
- VLAN 20 — FINANCE
- VLAN 30 — OPERATIONS
- VLAN 40 — IT
- VLAN 50 — EXECUTIVE
- VLAN 60 — SERVERS
- VLAN 99 — MANAGEMENT

HQ-SW1 GigabitEthernet0/1 and GigabitEthernet0/2 were operational
IEEE 802.1Q trunks.

Both trunks carried VLANs:

`10,20,30,40,50,60,99`

VLAN 99 was configured as the native VLAN.

HQ-R1 provided corresponding Layer-3 subinterfaces and gateway addresses
for the enterprise VLANs.

## 5. Method

1. Verified VLAN existence and status using `show vlan brief`.
2. Verified trunk operation using `show interfaces trunk`.
3. Verified HQ-R1 Layer-3 subinterfaces using `show ip interface brief`.
4. Verified HR-PC1 addressing and local gateway reachability.
5. Verified FIN-PC1 addressing and local gateway reachability.
6. Examined the HQ-SW1 dynamic MAC address table to determine whether
   learned Layer-2 addresses were associated with specific VLAN IDs.
7. Compared the observations against the intended RC-001 segmentation
   architecture.

## 6. Observations

### HR VLAN

HR-PC1 reported:

- IPv4 address: `10.10.10.10`
- Subnet mask: `255.255.255.224`
- Default gateway: `10.10.10.1`

Gateway test:

`HR-PC1 → 10.10.10.1: PASS (4/4)`

### Finance VLAN

FIN-PC1 reported:

- IPv4 address: `10.10.20.10`
- Subnet mask: `255.255.255.224`
- Default gateway: `10.10.20.1`

Gateway test:

`FIN-PC1 → 10.10.20.1: PASS (4/4)`

### Layer-2 Learning

The HQ-SW1 dynamic MAC address table showed learned MAC addresses
associated with specific VLAN IDs, including VLAN 10 and VLAN 20.

This is consistent with independent VLAN forwarding domains rather than
a single undifferentiated Layer-2 segment.

## 7. Result

**PASS**

The Headquarters implementation maintains distinct VLAN-based logical
segments and provides corresponding Layer-3 gateways through HQ-R1.

## 8. Evidence

Experimental evidence is stored under:

`Images/M10-Evidence/EXP-02/`

### Evidence Files

1. **EXP02-01-InterVLAN-Gateway-Baseline.png**
   - Shows the HQ-R1 Layer 3 interfaces supporting the existing departmental VLANs.
   - Confirms the configured VLAN gateways are operational.

2. **EXP02-02-VLAN-Trunk-Segmentation.png**
   - Shows the VLAN database on HQ-SW1.
   - Confirms the departmental VLANs are logically separated.
   - Verifies the required VLANs are propagated across the 802.1Q trunk links.

3. **EXP02-03-Dynamic-MAC-Learning.png**
   - Shows dynamically learned MAC addresses associated with their respective VLANs.
   - Provides Layer 2 evidence that endpoint traffic is being learned within separate VLAN broadcast domains.

4. **EXP02-04-HR-VLAN-Endpoint-Verification.png**
   - Shows HR-PC1 operating in the Human Resources subnet.
   - Confirms successful connectivity to the HR default gateway.

5. **EXP02-05-Finance-VLAN-Endpoint-Verification.png**
   - Shows FIN-PC1 operating in the Finance subnet.
   - Confirms successful connectivity to the Finance default gateway.

### Evidence Summary

The evidence demonstrates VLAN-based logical segmentation across the headquarters network. Separate departmental addressing, VLAN membership, trunk propagation, MAC-address learning, and endpoint-to-gateway connectivity collectively verify that the architecture maintains distinct Layer 2 broadcast domains while providing the required Layer 3 gateway functionality.

## 9. Interpretation

The results are consistent with the intended RC-001 segmentation model.

HR and Finance operate in different IPv4 subnets and VLAN contexts, while
HQ-R1 provides the Layer-3 boundary required for routed communication
between VLANs.

The switch MAC address table further demonstrates VLAN-aware Layer-2
learning.

## 10. Security Interpretation

VLAN segmentation should not be interpreted as equivalent to complete
security isolation.

VLANs establish separate logical Layer-2 broadcast domains. Where
communication between VLANs is routed, additional controls such as ACLs
are required to enforce traffic-security policy.

Those controls are evaluated separately from this experiment.

## 11. Limitations

The experiment used representative Headquarters VLANs rather than
repeating endpoint-level validation for every VLAN.

The experiment validates logical segmentation and gateway architecture;
it does not attempt to quantify broadcast traffic or measure VLAN
performance.

## 12. Conclusion

RC-001 successfully implements VLAN-based logical segmentation at
Headquarters. Representative HR and Finance endpoints operated in
distinct network segments, reached their respective Layer-3 gateways,
and were represented within VLAN-specific Layer-2 forwarding contexts.