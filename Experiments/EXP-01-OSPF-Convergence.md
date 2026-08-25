# EXP-01 — OSPF Convergence and WAN Recovery

## 1. Objective

Evaluate the behavior of RC-001's OSPF routing environment during a
controlled WAN-link interruption and subsequent restoration.

## 2. Research Question

How does the RC-001 routing environment respond when the WAN connection
between Headquarters and the Accra branch becomes unavailable and is
subsequently restored?

## 3. Environment

- Platform: Cisco Packet Tracer
- Protocol: OSPF
- HQ Router: HQ-R1
- Accra Router: ACC-R1
- Simulated failure interface: HQ-R1 GigabitEthernet0/0/1
- Accra WAN peer: 10.255.0.2
- Representative Accra LAN gateway: 10.20.30.1

## 4. Baseline

Before failure injection:

- OSPF neighbor 2.2.2.2 was FULL.
- OSPF neighbor 3.3.3.3 was FULL.
- Accra routes were present through 10.255.0.2.
- HQ-R1 → 10.255.0.2: PASS (5/5).
- HQ-R1 → 10.20.30.1: PASS (5/5).

## 5. Method

1. Verified the healthy OSPF baseline.
2. Administratively shut down HQ-R1 GigabitEthernet0/0/1.
3. Observed OSPF neighbor state and routing-table changes.
4. Tested reachability to the Accra WAN peer and LAN gateway.
5. Restored GigabitEthernet0/0/1 using `no shutdown`.
6. Observed OSPF adjacency recovery.
7. Verified route relearning.
8. Repeated reachability tests after convergence.

## 6. Failure Observation

Following the controlled WAN interruption:

- IOS reported neighbor 2.2.2.2 transitioning from FULL to DOWN.
- The Accra OSPF neighbor disappeared from the neighbor table.
- Accra OSPF routes were withdrawn.
- Takoradi neighbor 3.3.3.3 remained operational.
- Takoradi OSPF routes remained present.
- HQ-R1 → 10.255.0.2: FAIL (0/5).
- HQ-R1 → 10.20.30.1: FAIL (0/5).

The failure therefore remained isolated to the affected WAN path.

## 7. Recovery Observation

After restoring GigabitEthernet0/0/1:

- The physical/link-layer interface returned to the up state.
- OSPF adjacency progressed through transitional states.
- An initial recovery ping to 10.255.0.2 returned 4/5 replies.
- IOS subsequently reported neighbor 2.2.2.2 transitioning from
  LOADING to FULL.
- Accra OSPF routes were relearned through 10.255.0.2.
- HQ-R1 → 10.255.0.2: PASS (5/5).
- HQ-R1 → 10.20.30.1: PASS (5/5).

## 8. Result

**PASS**

RC-001 correctly detected the simulated WAN interruption, removed the
affected OSPF adjacency and learned routes, and restored routing
functionality after the WAN link returned.

## 9. Interpretation

The experiment demonstrates dynamic routing-state adaptation to link
failure and recovery.

It also demonstrates that restoration of the physical interface does not
imply instantaneous routing convergence. Transitional OSPF states were
observed before the adjacency returned to FULL and routes were restored.

## 10. Evidence

Experimental evidence is stored under:

`Images/M10-Evidence/EXP-01/`

### Evidence Files

1. **EXP01-01-OSPF-Healthy-Baseline.png**
   - Establishes the pre-failure network state.
   - Confirms both OSPF neighbors are in FULL adjacency and branch routes are present.

2. **EXP01-02-WAN-Failure-Route-Withdrawal.png**
   - Captures the deliberate shutdown of the HQ–Accra WAN interface.
   - Shows OSPF neighbor 2.2.2.2 transitioning from FULL to DOWN and affected routes being withdrawn.

3. **EXP01-03-OSPF-Reconvergence-In-Progress.png**
   - Captures restoration of the WAN interface using `no shutdown`.
   - Shows OSPF adjacency formation and routing reconvergence in progress.

4. **EXP01-04-OSPF-Recovery-Verified.png**
   - Confirms neighbor 2.2.2.2 returned to FULL adjacency.
   - Confirms withdrawn OSPF routes were restored.
   - Successful ICMP tests verify end-to-end connectivity after recovery.

### Evidence Summary

The captured evidence demonstrates the complete experimental sequence: healthy baseline, controlled WAN failure, OSPF route withdrawal, reconvergence after link restoration, and successful recovery of routing and connectivity.

## 11. Limitation

RC-001 does not provide an alternate WAN path to Accra. Consequently,
withdrawal of the only Accra WAN connection results in loss of Accra
reachability until that connection is restored.

This experiment validates routing convergence and recovery behavior; it
does not demonstrate WAN high availability.

Convergence time was not measured using a controlled timing methodology.
Therefore, no quantitative convergence-time claim is made.

## 12. Conclusion

The observed behavior was consistent with the intended RC-001 OSPF
design. OSPF dynamically withdrew routes following link failure and
relearned them following restoration while the unaffected Takoradi
routing relationship remained operational.