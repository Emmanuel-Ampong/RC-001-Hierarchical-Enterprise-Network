\# EXP-03 — Secure Administration



\## 1. Objective



Evaluate whether RC-001 permits authenticated SSH administration from an

authorized IT network while preventing an unauthorized user network from

accessing the protected management plane.



\## 2. Research Question



Can an authorized IT endpoint securely administer enterprise network

infrastructure using SSHv2 while an unauthorized HR endpoint is prevented

from reaching the same management interface?



\## 3. Environment



\- Platform: Cisco Packet Tracer

\- Managed device: HQ-SW1

\- Management VLAN: VLAN 99

\- Management address: `10.10.99.2`

\- Authorized source: IT-PC1

\- IT network: `10.10.40.0/27`

\- Unauthorized source: HR-PC1

\- HR network: `10.10.10.0/27`

\- Security control: HQ-R1 extended ACL `HQ-HR-IN`



\## 4. Baseline Verification



HQ-SW1 reported:



\- VLAN 99 management SVI: `10.10.99.2`

\- Management SVI status: up/up

\- SSH enabled

\- SSH version: 2.0

\- Local authentication configured for remote administration



During final validation, inconsistent VTY hardening was identified:

VTY lines 0–4 explicitly used local authentication and SSH-only transport,

while VTY lines 5–15 were not configured consistently.



The VTY configuration was normalized so that the remote-access lines use

local authentication and SSH-only transport.



A dedicated lab administrative account was used for validation.

Credentials are intentionally excluded from project documentation.



\## 5. Hypothesis



Expected behavior:



\- Authorized IT source → HQ management interface via SSH: ALLOW

\- Unauthorized HR source → HQ management interface via SSH: DENY



\## 6. Method



1\. Verified the HQ-SW1 management interface and SSH operational state.

2\. Confirmed the authorized IT-PC1 source addressing.

3\. Initiated an SSH session from IT-PC1 to `10.10.99.2`.

4\. Verified successful authenticated administrative access.

5\. Initiated the same SSH connection from HR-PC1.

6\. Observed whether HR-PC1 could reach the authentication stage.

7\. Examined the `HQ-HR-IN` ACL on HQ-R1 for independent policy evidence.



\## 7. Authorized Test



IT-PC1 successfully initiated an SSH connection to:



`10.10.99.2`



Authentication succeeded and an HQ-SW1 command prompt was obtained.



\*\*Result: PASS — authorized administrative access allowed.\*\*



\## 8. Unauthorized Test



HR-PC1 attempted an SSH connection to:



`10.10.99.2`



The connection timed out before an authentication prompt was presented.



\*\*Result: PASS — unauthorized management access blocked.\*\*



\## 9. ACL Corroboration



HQ-R1 reported matches against the explicit rule denying HR traffic to the

HQ management network:



`deny ip 10.10.10.0 0.0.0.31 10.10.99.0 0.0.0.31`



The rule displayed accumulated match activity.



This counter corroborates that HR-to-management traffic is being processed

by the intended deny policy. Because the counter is cumulative, the total

match count is not attributed exclusively to the single EXP-03 SSH attempt.



\## 10. Result



\*\*PASS\*\*



RC-001 successfully allowed authenticated SSH administration from the

authorized IT network while preventing the representative unauthorized HR

endpoint from accessing the protected management interface.

## 11. Evidence

Experimental evidence is stored under:

`Images/M10-Evidence/EXP-03/`

### Evidence Files

1. **EXP03-01-SSHv2-Configuration-Verification.png**
   - Confirms that SSH Version 2 is configured on HQ-SW1.
   - Shows the local administrative authentication configuration used for secure remote management.

2. **EXP03-02-Authorized-SSH-Access-Verified.png**
   - Shows a successful SSH connection to the HQ-SW1 management interface.
   - Successful authentication and access to the `HQ-SW1#` prompt demonstrate authorized encrypted remote administration.

3. **EXP03-03-Unauthorized-HR-SSH-Blocked.png**
   - Shows an SSH connection attempt from the HR network toward the management interface.
   - The connection times out, demonstrating that the unauthorized management-access attempt is prevented.

4. **EXP03-04-HR-Management-ACL-Counters.png**
   - Shows the `HQ-HR-IN` ACL applied to HR traffic.
   - The deny rule protecting the management network contains packet-match counters.
   - These counters provide device-side corroboration that prohibited HR-to-management traffic matched the configured security policy.

### Evidence Summary

The evidence demonstrates both sides of the secure-administration policy. SSH Version 2 provides encrypted remote management, an authorized administrative connection succeeds, an unauthorized HR-originated management connection fails, and ACL counters independently corroborate enforcement of the management-network restriction.



\## 12. Engineering Finding



Final validation identified inconsistent VTY-line hardening on HQ-SW1.



The configuration was corrected so that the remote-access lines consistently

use local authentication and SSH-only transport.



This finding demonstrates the value of final acceptance testing even after

functional milestones have previously passed.



\## 13. Security Interpretation



The experiment demonstrates layered administrative protection:



\- Dedicated management addressing

\- SSHv2 encrypted remote administration

\- Local authentication

\- Source-network authorization through ACL enforcement



Successful SSH configuration alone would not demonstrate authorization.

The positive/negative test verifies that administrative reachability differs

according to source-network policy.



\## 14. Limitations



The experiment used HQ-SW1 as a representative managed device rather than

repeating authenticated SSH testing against every infrastructure device.



ACL counters are cumulative and therefore provide corroborating evidence

rather than a one-to-one measurement of the individual SSH attempt.



Packet Tracer models SSH and network-device behavior but does not reproduce

all characteristics of production authentication and management systems.



\## 15. Conclusion



The observed behavior was consistent with the intended RC-001 secure

administration model. Authorized IT administration succeeded over SSHv2,

while unauthorized HR access to the management plane was prevented.

