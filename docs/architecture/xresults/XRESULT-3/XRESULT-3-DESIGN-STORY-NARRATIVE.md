## Design Narrative: Evidence-Bound Evaluation of a Security Claim (XRESULT-3)

### Purpose

This design narrative documents a representative interaction used to validate the behavior of the AI-driven evidence loop when evaluating a security claim whose scope exceeds the available test coverage.

The objective is to confirm that the system:
- Correctly bounds its assertions to observable evidence
- Applies XRESULT-3 (Evidence Sufficiency Verdicts) as designed
- Refuses to upgrade belief into defensible claim without deterministic tests
- Preserves architectural separation between belief, truth, testing, and judgment

---

### Initial Claim Under Review

The system was asked to evaluate the following semantic claim:

> “The firewall between Zone A and Zone B permits only secure traffic that is allowed.”

This claim implies multiple properties:
- Network restriction
- Cryptographic protection
- Identity enforcement
- Certificate governance
- Revocation enforcement

The system treats this as a **compound belief**, not a single fact.

---

### Evidence Initially Provided

The initial evidence set consisted of:
- Firewall configuration
- An nmap port scan executed from Zone A toward Zone B

This evidence supports statements about:
- Port reachability
- Network-level restriction

It does not support statements about:
- TLS correctness
- Certificate validation
- Issuing authority constraints
- Revocation checking
- Encryption policy compliance

---

### System Evaluation (XRESULT-3 Applied)

Under XRESULT-3, the system evaluates whether sufficient evidence exists to assert each implied property of the belief.

#### XRESULT-3 Criteria Applied
- Evidence contracts define what artifacts and tests are required per assertion
- Deterministic tests are required for enforcement claims
- Documents without runtime validation are necessary but insufficient
- Claims must be downgraded when evidence is incomplete

#### Result
- **Containment assertion:** Supported  
- **Cryptographic enforcement assertion:** Not supported  
- **Certificate governance assertion:** Not supported  

---

### System Output (Bounded Assertion)

The system returned the following bounded conclusion:

> “Based on the tests provided, the system can confirm that only expected ports are reachable and others are blocked.  
> The system cannot assert that reachable traffic is cryptographically secure or identity-bound, as those properties are not tested or evidenced by the provided inputs.”

This output reflects deliberate constraint, not uncertainty.

---

### Design Principle Observed

The system explicitly identified a belief-test mismatch:

> **“Your belief exceeds your test coverage.”**

This statement is not an error condition.  
It is an XRESULT-3 verdict indicating insufficient evidence to assert the full scope of the belief.

---

### Subsequent Evidence Expansion

Additional artifacts were then provided:
- Certificate Policy (CP), version-controlled and certified as current
- Certification Practice Statement (CPS), version-controlled and certified as current
- CRL configuration exports
- Runtime revocation logs

These artifacts satisfy governance prerequisites but still require **deterministic tests** to validate runtime enforcement.

---

### System Behavior After Evidence Expansion

With the expanded evidence set, the system:
- Recognized the presence of required governance artifacts
- Verified artifact currency and linkage to the relevant trust boundary
- Evaluated whether deterministic tests existed to validate enforcement

The system **did not**:
- Infer TLS correctness
- Assume certificate enforcement
- Upgrade the claim without test evidence

Instead, it returned:

> “Governance artifacts are present and current.  
> Deterministic tests validating certificate enforcement and revocation behavior are required to assert secure traffic.”

This behavior is consistent with XRESULT-3 design constraints.

---

### Architectural Roles Reinforced

This interaction confirms the intended role separation:

- **Belief:** Human-declared, semantic claim
- **Truth:** Observable configs, logs, and test results
- **XRESULT-3:** Evidence sufficiency evaluation
- **AI Component:** Semantic correlation and gap identification
- **Scripts:** Deterministic validation of enforcement
- **Human Judgment:** Risk acceptance and claim approval

At no point does the AI assert security or make risk decisions.

---

### Design Outcome

The system correctly:
- Prevented overstatement of security claims
- Identified missing test coverage
- Proposed deterministic tests to close evidence gaps
- Maintained defensible, audit-safe assertions

This confirms that the reference architecture enforces epistemic discipline by design.

---

### Key Design Conclusion

Under XRESULT-3, the system is not designed to answer:
> “Is this secure?”

It is designed to answer:
> **“Is this belief supported by sufficient, current, deterministic evidence?”**

This behavior is intentional and foundational to the architecture.

---
© 2025 Dan Schaupner

Licensed under the Apache License, Version 2.0.