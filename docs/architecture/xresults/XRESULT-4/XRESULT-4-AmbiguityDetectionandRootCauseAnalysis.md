# XRESULT-4 Example  
## Ambiguity Detection and Root-Cause Hypothesis

---

### XRESULT Metadata

- **XRESULT Type:** Ambiguity Detection  
- **Interface ID:** ZA-ZB-001  
- **Timestamp (UTC):** 2025-12-19T21:32:11Z  

---

## Claim Under Test

> *Zone A must not initiate any connectivity to Zone B, except for the PaymentAPI service communicating to the Database service over TCP/443 using mutual TLS.*

---

## Deterministic Findings (from Scripts)

- **Script ID:** `delta_compare_v1.3`  
- **Script Outcome:** **INCONCLUSIVE**

### Observed Symptoms
- Ta reports TCP/445 as **filtered** (not *closed* or *explicitly denied*).
- Firewall F configuration includes an explicit deny rule for TCP/445 from Zone A to Zone B.
- Firewall F logs contain **no deny events** corresponding to the TCP/445 probe window.
- Host B and Tb logs show **no inbound connection attempts** from Ta.

---

## Ambiguities Detected

### AMB-001 — Telemetry Gap
- **Description:**  
  Expected deny telemetry for TCP/445 is absent. The system cannot demonstrate that Firewall F actively enforced the block during the test.
- **Evidence References:**  
  - `TRUTH/fw_logs_2025-12-19.json`  
  - `TRUTH/ta_nmap_2025-12-19T21-30Z.txt`

---

### AMB-002 — Classification Uncertainty
- **Description:**  
  The scan result `filtered` could indicate:
  - a firewall drop without logging,
  - an upstream network block before Firewall F,
  - IPS or rate-limiting behavior,
  - routing asymmetry, or
  - endpoint-side blocking.
- **Evidence References:**  
  - `TRUTH/ta_nmap_2025-12-19T21-30Z.txt`  
  - `TRUTH/router_acl_snapshot.txt`

---

## Root-Cause Hypotheses

### HYP-001 — Firewall Deny Logging Not Enabled
- **Why Plausible:**  
  Firewall F configuration shows a deny rule, but no deny logs are present during the probe window.
- **Deterministic Falsification Steps:**  
  - Capture deny rule hit counters during repeated TCP/445 probes.  
  - Temporarily enable logging on the deny rule (time-boxed) and rerun probes.  
  - Compare pre- and post-test log presence.
- **Required Additional Artifacts:**  
  - `TRUTH/fw_policy_log_settings.txt`  
  - `TRUTH/fw_rule_hit_counters_before_after.json`

---

### HYP-002 — Traffic Blocked Upstream of Firewall F
- **Why Plausible:**  
  Absence of deny logs on Firewall F and no inbound visibility on Host B suggest packets may not reach Firewall F.
- **Deterministic Falsification Steps:**  
  - Run traceroute or TCP traceroute from Ta to B on TCP/445 and TCP/443.  
  - Collect router interface counters adjacent to Firewall F.  
  - Capture a short, time-boxed packet trace on Firewall F ingress during a controlled probe.
- **Required Additional Artifacts:**  
  - `TRUTH/ta_traceroute_445_443.txt`  
  - `TRUTH/router_interface_counters.json`  
  - `TRUTH/fw_ingress_packet_trace_10s.pcapmeta`

---

### HYP-003 — Time Correlation Skew
- **Why Plausible:**  
  Timestamp misalignment could explain the absence of matching deny events.
- **Deterministic Falsification Steps:**  
  - Verify NTP synchronization on Ta, Engine X, and Firewall F.  
  - Generate a known marker event (permitted TCP/443 connection) and confirm matching timestamps across all logs.
- **Required Additional Artifacts:**  
  - `TRUTH/ntp_status_all_nodes.txt`  
  - `TRUTH/marker_event_correlation_bundle.json`

---

## Model Constraints Observed

- No new facts were introduced by the model.
- All statements trace directly to submitted artifacts.
- No control actions or policy changes were recommended.

---

## Semantic Summary

The desired security outcome—blocking TCP/445 from Zone A to Zone B—was observed. However, the available telemetry cannot prove that Firewall F was the enforcing control. As a result, containment is **assumed but not evidenced**. Additional deterministic artifacts are required to establish causal attribution before the control can be considered provably effective.

---

## Disposition

The security administrator must evaluate this ambiguity against the established **risk threshold** and decide whether to:
- accept the evidentiary gap and continue monitoring, or
- collect additional artifacts, or
- open an incident for further investigation.

---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.