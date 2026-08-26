# RC001-ADR-006 — Branch VLAN Standardization

## Document Information

| Field | Value |
|---|---|
| Project | RC-001 — Secure Hierarchical Enterprise Network |
| Organization | Ashanti Logistics Ghana Ltd. |
| Document ID | RC001-ADR-006 |
| Version | 1.0 |
| Status | Accepted |
| Author | Emmanuel Ampong |
| Date | 2 August 2026 |

---

## 1. Context

The original IP addressing plan placed all Accra and Takoradi branch users in VLAN 10.

During implementation, the branch endpoints were assigned according to departmental function:

- VLAN 30 — Operations
- VLAN 40 — Information Technology
- VLAN 99 — Network Management

The implemented structure provides more meaningful logical segmentation and aligns departmental VLAN identifiers across headquarters and branch locations.

The IP Addressing Plan and Low-Level Design therefore require revision so that the documentation matches the implemented architecture.

---

## 2. Decision

Accra and Takoradi shall use the following VLAN structure:

| VLAN | Function |
|---:|---|
| 30 | Operations |
| 40 | Information Technology |
| 99 | Network Management |

Each VLAN shall use a unique, site-specific IPv4 subnet.

### Accra

| VLAN | Network | Gateway |
|---:|---|---|
| 30 | 10.20.30.0/26 | 10.20.30.1 |
| 40 | 10.20.40.0/27 | 10.20.40.1 |
| 99 | 10.20.99.0/28 | 10.20.99.1 |

### Takoradi

| VLAN | Network | Gateway |
|---:|---|---|
| 30 | 10.30.30.0/26 | 10.30.30.1 |
| 40 | 10.30.40.0/27 | 10.30.40.1 |
| 99 | 10.30.99.0/28 | 10.30.99.1 |

Branch trunks shall permit only VLANs 30, 40, and 99.

---

## 3. Alternatives Considered

### Alternative 1 — Retain a Single Branch User VLAN

Both branch PCs could remain in VLAN 10.

#### Advantages

- Simpler configuration
- Fewer router subinterfaces
- Fewer subnets to manage

#### Disadvantages

- Operations and IT traffic would share one broadcast domain
- Reduced logical segmentation
- Less consistency with the headquarters VLAN structure
- Weaker foundation for future ACL and firewall policies

**Decision:** Rejected.

### Alternative 2 — Use Different VLAN Numbers at Each Site

Each branch could use locally selected VLAN IDs.

#### Advantages

- Greater local flexibility

#### Disadvantages

- Increased administrative complexity
- More difficult troubleshooting
- Inconsistent enterprise standards
- Greater chance of configuration errors

**Decision:** Rejected.

### Alternative 3 — Standardize Departmental VLAN Numbers

Use VLAN 30 for Operations and VLAN 40 for IT at all relevant sites.

#### Advantages

- Consistent enterprise-wide naming
- Easier troubleshooting
- Clear departmental identification
- Better scalability
- Stronger foundation for security policy enforcement

**Decision:** Accepted.

---

## 4. Rationale

Standardized departmental VLAN numbering improves operational clarity and reduces configuration ambiguity.

An engineer examining VLAN 30 or VLAN 40 at any site can immediately identify its intended departmental function.

The design also creates separate broadcast domains for Operations and IT, providing a cleaner foundation for future:

- Access Control Lists
- Firewall policies
- Traffic monitoring
- Quality of Service
- Security analytics

---

## 5. Consequences

### Positive Consequences

- Consistent VLAN numbering across sites
- Improved logical segmentation
- Smaller branch broadcast domains
- Easier troubleshooting
- Better support for future security controls
- Clearer IP addressing structure

### Negative Consequences

- Additional router subinterfaces are required
- Additional subnets must be managed
- Branch trunk configurations must carry three VLANs
- The IP Addressing Plan and LLD must be updated

---

## 6. Required Documentation Updates

The following documents shall be revised:

- RC001-IPP-001 — IP Addressing Plan
- RC001-LLD-001 — Low-Level Design
- Branch logical topology diagram
- Test Plan
- OSPF network advertisement plan

---

## 7. Implementation Impact

The branch routers shall use:

### ACC-R1

- G0/0/0.30 — 10.20.30.1/26
- G0/0/0.40 — 10.20.40.1/27
- G0/0/0.99 — 10.20.99.1/28

### TAK-R1

- G0/0/0.30 — 10.30.30.1/26
- G0/0/0.40 — 10.30.40.1/27
- G0/0/0.99 — 10.30.99.1/28

Branch switch trunks shall allow:

```text
30,40,99