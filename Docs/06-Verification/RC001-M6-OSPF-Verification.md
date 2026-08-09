# RC001-M6 OSPF Dynamic Routing Verification

## Objective

Verify OSPF neighbor formation, dynamic route propagation, and end-to-end connectivity between Headquarters, Accra, and Takoradi.

## OSPF Neighbor Verification

| Router | Neighbor | State | Result |
|---|---|---|---|
| HQ-R1 | ACC-R1 (2.2.2.2) | FULL | PASS |
| HQ-R1 | TAK-R1 (3.3.3.3) | FULL | PASS |
| ACC-R1 | HQ-R1 (1.1.1.1) | FULL | PASS |
| TAK-R1 | HQ-R1 (1.1.1.1) | FULL | PASS |

## Route Propagation Verification

| Router | Remote Networks Learned | Result |
|---|---|---|
| HQ-R1 | Accra and Takoradi | PASS |
| ACC-R1 | Headquarters and Takoradi | PASS |
| TAK-R1 | Headquarters and Accra | PASS |

## End-to-End Connectivity

| Source | Destination | Result |
|---|---|---|
| ACC-PC1 | HQ HR-PC1 – 10.10.10.10 | PASS |
| ACC-PC1 | HQ AD-SRV – 10.10.60.10 | PASS |
| ACC-PC1 | TAK-PC1 – 10.30.30.10 | PASS |
| ACC-PC1 | TAK-PC2 – 10.30.40.10 | PASS |
| TAK-PC1 | HQ HR-PC1 – 10.10.10.10 | PASS |
| TAK-PC1 | HQ AD-SRV – 10.10.60.10 | PASS |
| TAK-PC1 | ACC-PC1 – 10.20.30.10 | PASS |
| TAK-PC1 | ACC-PC2 – 10.20.40.10 | PASS |

## Path Verification

Traceroute from ACC-PC1 to TAK-PC1 produced:

1. 10.20.30.1 – ACC-R1
2. 10.255.0.1 – HQ-R1
3. 10.255.0.6 – TAK-R1
4. 10.30.30.10 – TAK-PC1

This confirms that branch-to-branch traffic follows the designed hub-and-spoke path through Headquarters.

## Acceptance Criteria

- OSPF adjacencies reach FULL state – PASS
- Remote routes learned dynamically – PASS
- Headquarters-to-branch routing operational – PASS
- Branch-to-branch routing operational – PASS
- End-to-end endpoint communication operational – PASS
- Routing path conforms to WAN design – PASS

## Final Result

**M6 PASSED**

OSPF dynamic routing is operational across the RC-001 enterprise network.