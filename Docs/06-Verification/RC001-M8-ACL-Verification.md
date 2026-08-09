# RC001-M8 ACL-Based Security and Network Segmentation Verification

## Milestone
M8 – ACL-Based Security and Network Segmentation

## Status
PASS

## Objective
Implement and verify role-based network access controls that protect enterprise management networks from unauthorized user VLANs while preserving authorized IT access and legitimate business traffic.

## Security Policy

The following policy was implemented:

- IT networks are permitted to access management networks.
- HR users are denied access to management networks.
- Finance users are denied access to management networks.
- Operations users are denied access to management networks.
- Executive users are denied access to management networks.
- Branch Operations users are denied access to management networks.
- Legitimate non-management traffic remains permitted.

## Protected Management Networks

| Site | Management Network |
|---|---|
| Headquarters | 10.10.99.0/27 |
| Accra | 10.20.99.0/28 |
| Takoradi | 10.30.99.0/28 |

## Pre-Control Baseline

Before ACL implementation, HR-PC1 and IT-PC1 were able to reach management interfaces at all three sites.

This demonstrated that routing alone provided connectivity without role-based access restrictions.

## HQ ACL Implementation

Extended ACLs were applied inbound on the appropriate HQ user VLAN subinterfaces.

Protected user groups:

- HR
- Finance
- Operations
- Executive

The IT VLAN was intentionally excluded from the blocking policy because it represents the authorized administrative network.

## Branch ACL Implementation

Extended ACLs were implemented on ACC-R1 and TAK-R1.

Branch Operations networks were denied access to management networks while branch IT networks retained management connectivity.

## Negative Security Testing

Unauthorized endpoints were tested against management destinations.

Expected result: BLOCKED

Observed result: PASS

Representative tests confirmed:

- HR → Management: BLOCKED
- Finance → Management: BLOCKED
- Operations → Management: BLOCKED
- Executive → Management: BLOCKED
- Accra Operations → Management: BLOCKED
- Takoradi Operations → Management: BLOCKED

## Positive Security Testing

Authorized IT endpoints were tested against management networks.

Expected result: ALLOWED

Observed result: PASS

- HQ IT → Management: ALLOWED
- Accra IT → Management: ALLOWED
- Takoradi IT → Management: ALLOWED

## Business-Traffic Validation

Representative restricted endpoints were tested against the HQ server network.

Legitimate server connectivity remained operational.

This demonstrated that the ACL implementation selectively restricted management-plane access rather than disrupting general routed connectivity.

## ACL Counter Verification

`show access-lists` was used on:

- HQ-R1
- ACC-R1
- TAK-R1

Non-zero match counters were observed on representative deny and permit ACEs.

Examples included:

- ACC-R1 management deny ACEs: 4 matches each
- ACC-R1 permit ACE: 8 matches
- TAK-R1 management deny ACEs: 4 matches each
- TAK-R1 permit ACE: 8 matches
- HQ ACLs recorded deny and permit matches during representative verification tests

Not every individual HQ deny ACE was exercised because representative destination testing was used. No untested ACE is claimed as individually verified.

## Security Outcome

The enterprise moved from unrestricted routed management reachability to role-based management-plane segmentation.

Before M8:

Unauthorized Users → Management = ALLOWED

After M8:

Unauthorized Users → Management = BLOCKED  
Authorized IT → Management = ALLOWED  
Legitimate Business Traffic = ALLOWED

## Final Result

**M8 PASSED**

ACL-based security segmentation was successfully implemented and verified across the RC-001 enterprise network.

