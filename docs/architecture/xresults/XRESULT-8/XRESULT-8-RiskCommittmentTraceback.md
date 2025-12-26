# XRESULT-8 Examples  
## Risk-Commitment Traceback

---

## Example 1 — Firewall / Network Segmentation

### Context
**Domain:** Network security  
**Interface:** Zone A ↔ Zone B  
**Risk Commitment ID:** RISK-2025-014

> **Risk Commitment:**  
> Lateral movement from Zone A to Zone B must be prevented to limit ransomware blast radius to Zone A only.

---

### Inputs (Provided to Model X)

- **BELIEF**
  - Expected state: No SMB or unrestricted traffic between Zone A and Zone B
  - Explicit allow: HTTPS (443) from `payment-api.service` → `db-cluster.service` using mTLS
- **TRUTH**
  - Firewall F configuration
  - Firewall and router logs
  - Ta / Tb nmap test results
- **DELTA**
  - Script-detected over-permissive firewall rule

---

### XRESULT-8 — Risk-Statement Traceback

```json
{
  "xresult_type": "risk_statement_traceback",
  "interface_id": "ZA-ZB-001",
  "timestamp": "2025-03-19T14:22:11Z",

  "risk_statements": [
    {
      "risk_statement_id": "RISK-2025-014",
      "risk_text": "Lateral movement from Zone A to Zone B must be prevented to limit ransomware blast radius to Zone A only.",
      "declared_blast_radius": "Zone A",
      "risk_owner": "Security Architecture"
    }
  ],

  "related_deltas": [
    {
      "delta_id": "DELTA-0031",
      "delta_type": "over_permissive_firewall_rule",
      "observed_condition": "Firewall rule permits TCP/445 from Zone A subnet to Zone B subnet",
      "expected_condition": "No SMB permitted between Zone A and Zone B",
      "evidence_refs": [
        "fw_config_snapshot_2025-03-19.txt",
        "fw_log_2025-03-19_13.log",
        "Ta_nmap_results_2025-03-19.json"
      ]
    }
  ],

  "traceback_assessment": {
    "risk_alignment": "violates",
    "violation_reason": "Observed SMB access enables lateral movement from Zone A to Zone B, contradicting declared blast-radius containment.",
    "blast_radius_impact": {
      "declared": "Zone A only",
      "observed": "Zone A + Zone B",
      "change_type": "expansion"
    }
  },

  "confidence_qualifiers": {
    "evidence_completeness": "sufficient",
    "log_time_correlation": "validated",
    "test_coverage": "direct_negative_test_confirmed"
  },

  "human_action_required": true
}
```

**Outcome Interpretation**
	•	The declared risk commitment is no longer true
	•	The blast-radius promise made by leadership is violated
	•	Evidence is sufficient to defend this determination under audit

⸻

## Example 2 — Urinalysis / Recruit Induction

### Context

**Domain:** Military recruit induction
**Process:** Urine sample collection and acceptance
**Risk Commitment ID:** RISK-INDUCT-URINE-002

**Risk Commitment:**
No urine sample will enter the testing pipeline unless it is biometrically associated with the individual who produced it under reasonable supervision.

⸻

**Inputs (Provided to Model X)**

	•	BELIEF
		•	Biometric verification required at both kit issuance and sample acceptance
		•	Continuous chain of custody with tamper-evident seal
	•	TRUTH
		•	Biometric event logs
		•	Kit issuance records
		•	Sample acceptance logs
		•	Seal serial records
	•	DELTA
		•	Script-detected missing biometric acceptance event

⸻

**XRESULT-8 — Risk-Statement Traceback**

```
{
  "xresult_type": "risk_statement_traceback",
  "process_id": "URINE-COLLECTION-INTAKE-01",
  "timestamp": "2025-03-19T16:41:52Z",

  "risk_statements": [
    {
      "risk_statement_id": "RISK-INDUCT-URINE-002",
      "risk_text": "Each urine sample must be biometrically associated with the individual who produced it to prevent substitution and evasion of detection.",
      "declared_risk_outcome": "No unverified samples admitted into testing pipeline",
      "risk_owner": "Recruit Induction Command"
    }
  ],

  "related_deltas": [
    {
      "delta_id": "DELTA-URINE-0047",
      "delta_type": "missing_biometric_acceptance_event",
      "observed_condition": "Sample kit K-77124 accepted without corresponding biometric verification event",
      "expected_condition": "Biometric verification required at sample acceptance",
      "evidence_refs": [
        "kit_issuance_log_2025-03-19.json",
        "sample_acceptance_log_2025-03-19.json",
        "biometric_event_log_2025-03-19.json"
      ]
    }
  ],

  "traceback_assessment": {
    "risk_alignment": "violates",
    "violation_reason": "Absence of biometric acceptance breaks identity-to-sample binding, enabling potential sample substitution.",
    "risk_outcome_impact": {
      "declared": "No unverified samples admitted",
      "observed": "Unverified sample admitted",
      "change_type": "control failure"
    }
  },

  "confidence_qualifiers": {
    "evidence_completeness": "sufficient",
    "log_time_correlation": "validated",
    "custody_chain_continuity": "broken"
  },

  "human_action_required": true
}
```


**Outcome Interpretation**
	•	The risk commitment made by command is not defensible
	•	A sample entered the pipeline without satisfying the required identity binding
	•	The failure point is explicit, time-stamped, and evidence-backed

⸻

## Structural Equivalence (Key Point)

**Both examples:**
	•	Trace a deterministically detected delta
	•	Back to a declared risk commitment
	•	Show how the promised outcome is no longer true
	•	Provide evidence references sufficient for audit, discipline, or remediation

Only the domain physics differ.


---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.