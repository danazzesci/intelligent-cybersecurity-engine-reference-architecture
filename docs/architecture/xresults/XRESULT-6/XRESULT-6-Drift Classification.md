# XRESULT-6 — Drift Classification (Example)

This document shows a **literal example** of an XRESULT-6 artifact produced after deterministic scripts have detected drift between **BELIEF** and **TRUTH** for a single interface.

No detection, enforcement, or decision-making occurs here.  
This artifact **only classifies** script-detected drift.

---

## Context

**Interface:** ZA–ZB–001  
**Zones:** Zone A ↔ Zone B  
**Detection method:** Deterministic scripts comparing BELIEF to observed configs, logs, and test results  
**Disposition:** To be opened as an OPEN ISSUE by Engine X

---

## XRESULT-6 Artifact (Returned by Model X)

```json
{
  "xresult_type": "drift_classification",
  "interface_id": "ZA-ZB-001",
  "timestamp_utc": "2025-12-19T22:41:08Z",

  "detected_drifts": [
    {
      "drift_id": "DRIFT-001",
      "drift_class": "over_permissive_expansion",
      "affected_component": "Firewall F",
      "expected_state_reference": "BELIEF.rule.12",
      "observed_state_reference": "FIREWALL.rule.98",
      "description": "Subnet-wide TCP access from Zone A to Zone B observed where identity-scoped access was expected.",
      "evidence_ids": [
        "fw_config_snapshot_2025-12-19",
        "fw_log_2025-12-19_14:03",
        "ta_nmap_result_2025-12-19"
      ]
    },
    {
      "drift_id": "DRIFT-002",
      "drift_class": "identity_weakening",
      "affected_component": "Firewall F",
      "expected_state_reference": "BELIEF.identity_binding.mtls_required",
      "observed_state_reference": "FIREWALL.rule.102",
      "description": "TLS allowed without client certificate verification.",
      "evidence_ids": [
        "fw_config_snapshot_2025-12-19",
        "fw_log_2025-12-19_14:11"
      ]
    },
    {
      "drift_id": "DRIFT-003",
      "drift_class": "logging_degradation",
      "affected_component": "Firewall F",
      "expected_state_reference": "BELIEF.logging.policy",
      "observed_state_reference": "FIREWALL.logging.runtime",
      "description": "Denied east-west traffic events not logged at configured verbosity.",
      "evidence_ids": [
        "fw_log_gap_2025-12-19",
        "logging_policy_expected.yaml"
      ]
    }
  ],

  "non_detected_drift_classes": [
    "diagram_drift",
    "time_correlation_drift"
  ],

  "classification_summary": {
    "total_drifts_detected": 3,
    "high_impact": 2,
    "medium_impact": 1,
    "low_impact": 0
  },

  "confidence_notes": [
    "All drift classifications are grounded in script-generated deltas.",
    "No classification relies on probabilistic inference.",
    "All referenced evidence artifacts are present in Storage X."
  ]
}
```

## Interpretation Notes (Non-authoritative)
	•	All drifts listed above were first detected by scripts
	•	XRESULT-6 provides classification only
	•	Engine X is responsible for:
		•	creating OPEN ISSUE objects
		•	persisting canonical records in Storage X
		•	routing issues to cognizant decision-making
	•	Model X does not:
		•	write to Storage X
		•	suppress drift
		•	determine risk or remediation

⸻

## Intended Use

This artifact exists to support:
	•	consistent OPEN ISSUE handling
	•	aggregation and trend analysis
	•	governance review
	•	evidence-of-care under scrutiny

It is not a control, policy, or decision artifact.


---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.