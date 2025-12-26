# XRESULT Example — Category 1: Schema Conformance Results

## Purpose

This document provides a **literal, concrete example** of an `XRESULT` produced by **Model X** for **Category 1: Schema Conformance Results**.

Scope is intentionally limited to:
- Structural validity
- Schema adherence
- Cross-reference resolvability

This XRESULT does **not**:
- Detect drift
- Judge risk
- Recommend actions
- Override deterministic scripts

---

## Context

### Inputs Submitted to Model X

- **BELIEF** object (expected state)
- **TRUTH** object (logs and configurations)
- **DELTA** object (script-generated differences)

Model X is asked only:

> “Do these artifacts conform to the declared schemas and reference each other consistently?”

---

## Declared Schemas (Excerpts)

### BELIEF Schema
```
interface_id: string
zones:
  source: string
  destination: string
default_policy: enum[deny, allow]
permitted_flows:
  - source_identity: string
    destination_identity: string
    protocol: string
    port: integer
    auth: string
risk_reference: string
```
### TRUTH Schema

```
firewall_config:
  rules: list
firewall_logs:
  timestamped_entries: list
test_results:
  ta:
    tests: list
  tb:
    tests: list
```
### DELTA Schema
```yaml
delta_id: string
delta_type: string
expected_reference: string
observed_reference: string
```
##Example Submitted Artifacts

### BELIEF (Fragment)
```interface_id: ZA-ZB-001
zones:
  source: Zone_A
  destination: Zone_B
default_policy: deny
permitted_flows:
  - source_identity: payment-api.service
    destination_identity: db-cluster.service
    protocol: https
    port: 443
    auth: mtls
risk_reference: RISK-2025-014

###TRUTH (Fragment)
firewall_config:
  rules:
    - id: FW-17
      src: 10.1.0.0/24
      dst: 10.2.0.0/24
      protocol: tcp
      port: 443

firewall_logs:
  timestamped_entries:
    - ts: 2025-03-12T14:22:01Z
      rule_id: FW-17
      action: allow

test_results:
  ta:
    tests:
      - test_id: TA-443
        result: success
  tb:
    tests:
      - test_id: TB-443
        result: success
```

### DELTA (Script-Produced)
```
{
  "delta_id": "DELTA-009",
  "delta_type": "scope_mismatch",
  "expected_reference": "payment-api.service → db-cluster.service",
  "observed_reference": "10.1.0.0/24 → 10.2.0.0/24"
}
```

## XRESULT Returned by Model X
###Schema Conformance Result

```
{
  "xresult_type": "schema_conformance",
  "overall_status": "non_conformant",
  "checks": [
    {
      "artifact": "BELIEF",
      "status": "conformant",
      "notes": "All required fields present and correctly typed."
    },
    {
      "artifact": "TRUTH",
      "status": "non_conformant",
      "violations": [
        {
          "field": "firewall_config.rules[*].source_identity",
          "issue": "missing",
          "detail": "Observed rules use subnet identifiers; BELIEF requires identity-scoped fields."
        }
      ]
    },
    {
      "artifact": "DELTA",
      "status": "conformant",
      "notes": "Delta fields correctly reference BELIEF and TRUTH artifacts."
    }
  ],
  "cross_reference_integrity": {
    "risk_reference_resolvable": true,
    "rule_id_references_resolvable": true,
    "test_id_references_resolvable": true
  },
  "timestamp": "2025-03-12T14:24:10Z"
}
```


## Interpretation Boundaries
What This XRESULT Is
- Structural validation of evidence artifacts
- Deterministic and verifiable
- Grounded entirely in submitted inputs

What This XRESULT Is Not
❌ A security decision
❌ A risk acceptance or rejection
❌ A control recommendation
❌ An enforcement action
❌ An override of script results

The model asserts only:
“The submitted artifacts do not structurally conform to the declared belief schema.”
## Why This XRESULT Exists
- Deterministic scripts detect configuration drift.
- This XRESULT detects evidence drift:
- Loss of identity semantics
- Schema erosion
- Silent format degradation
This prevents the system from producing false confidence due to structurally invalid evidence.

---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.