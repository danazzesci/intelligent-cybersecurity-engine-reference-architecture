# XRESULT-7 Example  
## Change Narrative Compression (Verbose Example)

---

## XRESULT Identifier

- **XRESULT Type:** XRESULT-7  
- **Name:** Change Narrative Compression  
- **Interface:** ZA–ZB–001  
- **Security Zones:**  
  - Zone A (Application / User Zone)  
  - Zone B (Protected Service / Database Zone)

---

## Purpose of This XRESULT

This XRESULT documents how the **meaning of the enforced security boundary** between Zone A and Zone B has changed relative to the originally approved security intent (**BELIEF**), based solely on deterministic observations and deltas.

This artifact does **not** detect the change, assess risk tolerance, or mandate remediation.  
It exists to preserve **semantic clarity** for human review.

---

## Authoritative BELIEF (Expected State)

The following intent was approved and stored as the BELIEF for this interface:

> **“Zone A must not initiate communication to Zone B except for the Payment API service communicating with the database service over mutually authenticated TLS on port 443. No other hosts, services, protocols, or ports are permitted.”**

This BELIEF embeds the following constraints:

- Default deny between Zone A and Zone B  
- A single authorized source (Payment API / Host A)  
- A single authorized destination (Database service / Host B)  
- Identity-scoped access, not zone-scoped access  
- Application-layer cryptographic authentication (mTLS)

---

## Observed TRUTH (Inputs)

The following observed artifacts were submitted to Model X:

### Configuration Artifacts
- Firewall F running configuration snapshot
- Firewall F access control rules

### Log Artifacts
- Firewall permit/deny logs (24-hour window)
- Router logs associated with Firewall F

### Test Artifacts
- **Ta (Zone A)**: nmap scans initiated from multiple hosts within Zone A  
- **Tb (Zone B)**: confirmation of inbound connection attempts

---

## Deterministic DELTA Summary (Produced by Scripts)

The following DELTA object was generated prior to Model X involvement:

```json
{
  "delta_id": "D-0042",
  "delta_type": "over_permissive_source_scope",
  "expected_source": "Host A (Payment API)",
  "observed_source": "Zone A subnet",
  "protocol": "TCP",
  "port": 443,
  "first_observed": "2025-03-14T02:17:09Z"
}
```

### Scripts additionally confirmed:
	•	Non-authorized hosts in Zone A successfully established TCP connections to Zone B on port 443
	•	Application-layer authentication subsequently failed for those hosts
	•	No data access was granted

⸻

## Compressed Change Narrative (XRESULT-7 Output)

### Narrative Summary

The security boundary between Zone A and Zone B no longer enforces identity-scoped initiation as described in the expected state. Instead, it enforces zone-scoped protocol access, allowing any host co-located in Zone A to initiate network communication with Zone B on port 443.

⸻

### Narrative Details

- The approved expected state authorizes only a single named source (Payment API / Host A) to initiate communication to Zone B.
- The currently enforced firewall configuration permits all hosts within Zone A to initiate TCP connections to Zone B on port 443.
- Although unauthorized hosts are rejected at the application layer due to failed mutual TLS authentication, network-layer reachability is granted prior to that rejection.
- This results in a semantic change from “only the authorized service may communicate” to “any host in Zone A may attempt communication, subject to later rejection.”

⸻

### Change Characterization

	•	Type: Expansion of initiation scope
	•	Layer Affected: Network-layer enforcement (L3/L4)
	•	Nature of Change: Broadening of allowed source population beyond declared intent

⸻

### Risk-Relevant Interpretation (Non-Decision)

This change alters the assumed blast-radius boundary by allowing:
	•	Lateral movement attempts from compromised hosts within Zone A
	•	Network-level probing of Zone B services
	•	Credential misuse attempts prior to application-layer rejection

No statement is made regarding acceptability or urgency.

⸻

### Evidence References

The following artifacts support this narrative:
	•	firewall_config_snapshot_20250314.txt
	•	fw_permit_logs_20250314.json
	•	ta_nmap_results_zoneA_20250314.log
	•	tb_connection_attempts_20250314.log

Each referenced artifact is time-stamped and preserved in Storage X.

⸻

### Confidence Statement
	•	Confidence Level: High
	•	Basis:
	•	Deterministic script confirmation of rule scope
	•	Reproducible test results from multiple Zone A hosts
	•	Consistent firewall logging behavior

⸻

### Explicit Non-Claims

This XRESULT does not assert that:
	•	A breach has occurred
	•	Data has been exposed
	•	Risk tolerance has been exceeded
	•	A remediation must be applied

Those determinations remain the responsibility of human risk management.

⸻

## Intended Use

This XRESULT is intended to:
	•	Support human review against pre-established risk thresholds
	•	Enable consistent interpretation across reviewers and time
	•	Preserve the original semantic meaning of the security decision
	•	Reduce reliance on raw logs and tribal knowledge

⸻

One-Sentence Interpretation

**“Although only HTTPS traffic is permitted, the enforced boundary now allows any host in Zone A to initiate contact with Zone B, which differs from the original intent that only the authorized Payment API service could do so."**

---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.