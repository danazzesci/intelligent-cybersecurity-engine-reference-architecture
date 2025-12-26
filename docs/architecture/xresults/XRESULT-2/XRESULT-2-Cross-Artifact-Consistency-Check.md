XRESULT #2 — Concrete Example

Cross-Artifact Consistency Check (Simple Firewall Segmentation Only)

This example applies only to a single firewall-governed interface between two security zones.
Deepfake and session governance cases are intentionally excluded.

⸻

Scenario Overview
	•	Zone A: Application zone
	•	Zone B: Data zone
	•	Firewall F: Sole enforcement point between Zone A and Zone B
	•	Policy model: Explicit allow-list, implicit deny
	•	Objective: Ensure that only declared permitted flows exist across the interface

⸻

BELIEF (Expected State)

Human-authored semantic intent:

Zone A may communicate with Zone B only using HTTPS on port 443 from the Payment API service.
All other traffic between Zone A and Zone B must be denied.

Derived expected-state artifact:

```
interface_id: ZA-ZB-001
default_policy: deny
permitted_flows:
	•	source_identity: payment-api.service
destination_identity: db.service
protocol: tcp
port: 443
```

⸻

TRUTH (Observed Artifacts)

1. Firewall Configuration (Excerpt)

```
allow tcp payment-api.service db.service eq 443
deny ip any any
```

⸻

2. Firewall Logs (Excerpt)

```
timestamp: 2025-03-14T10:00:12Z
src: payment-api.service
dst: db.service
dst_port: 443
action: allow

timestamp: 2025-03-14T10:01:45Z
src: 10.1.4.22
dst: 10.2.6.19
dst_port: 22
action: deny
```

⸻

3. Test Results (Ta in Zone A)

```
Test 1: HTTPS (443) → SUCCESS
Test 2: SSH (22) → BLOCKED
Test 3: SMB (445) → BLOCKED
```

⸻

4. Test Results (Tb in Zone B)

```
No inbound connections observed from Zone A
outside of HTTPS/443 during test window
```

⸻

Deterministic Script Outcome (Layer 1)

Scripts evaluate:
	•	Explicit permit exists
	•	Default deny enforced
	•	Sampled non-permitted flows blocked
	•	No unexpected allow rules detected

Script output:

```
interface_id: ZA-ZB-001
script_result: PASS
```

At this point, controls and tests are OK.

⸻

XRESULT #2: Cross-Artifact Consistency Check (Layer 2)

Question Asked

Do BELIEF, configuration, logs, and test results all describe the same interface behavior?

⸻

Cross-Artifact Evaluation
	•	BELIEF asserts exclusive allow-list behavior
	•	Firewall configuration reflects that behavior
	•	Logs show:
	•	Allows only for declared flow
	•	Denies for sampled non-permitted flows
	•	Tests corroborate log behavior
	•	No artifact contradicts another

⸻

XRESULT Output

```
xresult_type: cross_artifact_consistency
interface_id: ZA-ZB-001
status: CONSISTENT
checked_artifacts:
	•	expected_state.yaml
	•	firewall_config.txt
	•	firewall_logs.json
	•	ta_test_results.txt
	•	tb_test_results.txt
```

notes:
All artifacts consistently support the assertion that only declared permitted flows exist across the interface.

⸻

Why XRESULT Is Necessary Here

Even though scripts passed, XRESULT confirms that:
	•	No artifact quietly contradicts another
	•	No “paper compliance” exists
	•	No evidence gap requires later reconstruction

XRESULT does not assert that the policy is sufficient.
It asserts only that the facts agree.

⸻

Key Takeaway

XRESULT #2 confirms that the firewall interface behaves exactly as described by the expected state, and that all evidence artifacts tell a single, coherent story about that behavior.


---

  

© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.