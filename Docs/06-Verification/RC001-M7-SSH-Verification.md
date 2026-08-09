# RC001-M7 Secure Remote Management Verification

## Objective

Verify deployment of SSH Version 2 and enforcement of SSH-only remote management across the RC-001 enterprise infrastructure.

## Devices

| Device | SSHv2 Configuration |
|---|---|
| HQ-R1 | PASS |
| HQ-SW1 | PASS |
| HQ-SW2 | PASS |
| ACC-R1 | PASS |
| ACC-SW1 | PASS |
| TAK-R1 | PASS |
| TAK-SW1 | PASS |

## Management Reachability

Management interfaces were tested from HQ-SW1 across the enterprise network.

| Network | Result |
|---|---|
| Headquarters Management | PASS |
| Accra Management | PASS |
| Takoradi Management | PASS |

Initial ICMP packets experienced transient loss during some tests; repeated tests achieved full reachability.

## SSH Verification

`show ip ssh` confirmed:

- SSH enabled.
- SSH Version 2.0 operational.

Representative router and switch VTY configurations were inspected and confirmed:

- `login local`
- `transport input ssh`
- 10-minute inactivity timeout

## Negative Security Testing

| Source | Destination | Protocol | Expected | Result |
|---|---|---|---|---|
| HQ-SW1 | HQ-R1 | Telnet | Blocked | PASS |
| HQ-SW1 | ACC-R1 | Telnet | Blocked | PASS |
| HQ-SW1 | TAK-R1 | Telnet | Blocked | PASS |

The destination devices were reachable, but the Telnet sessions were closed by the remote devices.

This confirms enforcement of the SSH-only VTY policy.

## Limitation

An authenticated interactive SSH login was not directly validated because the tested Cisco Packet Tracer endpoint/switch client implementation did not support the required SSH client command.

Accordingly, interactive SSH authentication is not claimed as verified.

## Acceptance Criteria

| Requirement | Result |
|---|---|
| SSHv2 enabled | PASS |
| RSA keys generated | PASS |
| Local administrative authentication configured | PASS |
| VTY uses local authentication | PASS |
| VTY restricted to SSH | PASS |
| Management networks reachable | PASS |
| Cross-site management reachability | PASS |
| Telnet prohibited | PASS |
| Interactive SSH client login | NOT DIRECTLY VERIFIED |

## Final Result

**M7 PASSED WITH DOCUMENTED SIMULATION LIMITATION**

The RC-001 management plane has been hardened to use SSHv2, and insecure Telnet access has been successfully restricted.