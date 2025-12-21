# Canonical Definitions  
*(Authoritative for the Intelligent Cybersecurity Engine Reference Architecture)*

---

## BELIEF

**BELIEF** is the authoritative, human-declared description of what the system is intended to enforce and why.

It captures semantic intent, including:
- permitted and prohibited interactions,
- identity and scope constraints,
- default behaviors (e.g., deny by default),
- and the risk rationale that justifies those constraints.

BELIEF is:
- authored by humans,
- stored in version-controlled form,
- the sole source of intent,
- and never inferred from observed behavior.

BELIEF may be expressed as prose and derived into structured schemas, but derived structures never replace the original semantic intent.

---

## TRUTH

**TRUTH** is the set of observable, collected artifacts that describe what the system actually did or allowed during a specific time window.

TRUTH includes:
- configurations,
- logs,
- telemetry,
- deterministic test results,
- and other runtime observations.

TRUTH is:
- observational, not interpretive,
- time-bounded,
- collected via controlled, read-only mechanisms,
- and independent of BELIEF.

TRUTH does not imply correctness or safety; it only establishes what was observed.

---

## EVIDENCE

**EVIDENCE** is TRUTH that has been preserved, correlated, and retained in a form suitable for explanation, audit, and scrutiny.

EVIDENCE exists when:
- artifacts are time-stamped,
- references between artifacts are resolvable,
- integrity is preserved,
- and the artifacts remain interpretable over time.

EVIDENCE supports defensibility; it does not make decisions.

---

## DRIFT

**DRIFT** is a detected mismatch between BELIEF and TRUTH.

DRIFT indicates that:
- the observed system behavior, configuration, or evidence no longer aligns with the declared intent.

DRIFT:
- is detected deterministically (by scripts),
- is classified but not judged,
- does not imply a breach or incident,
- and must be recorded as an OPEN ISSUE for disposition.

---

## OPEN ISSUE

An **OPEN ISSUE** is a persisted, accountable record representing an unresolved condition that requires human review.

OPEN ISSUES may arise from:
- detected DRIFT,
- evidence insufficiency,
- ambiguity,
- assumption gaps,
- or violated risk commitments.

An OPEN ISSUE:
- preserves context and evidence,
- assigns ownership,
- records disposition decisions,
- and prevents silent acceptance through inaction.

---

## Engine X

**Engine X** is the deterministic execution engine responsible for:
- running approved scripts,
- collecting TRUTH,
- performing BELIEF ↔ TRUTH comparisons,
- generating DELTA artifacts,
- opening and routing OPEN ISSUES.

Engine X:
- does not infer meaning,
- does not interpret risk,
- does not make decisions,
- and does not modify BELIEF autonomously.

---

## Model X

**Model X** is a constrained semantic analysis component used only to preserve coherence, meaning, and interpretability across artifacts.

Model X may:
- classify drift,
- evaluate evidence sufficiency,
- compress change narratives,
- detect assumption gaps,
- bound claims to evidence.

Model X may not:
- execute code,
- change system state,
- write canonical records,
- decide risk,
- or override deterministic results.

Model X exists to prevent semantic decay, not to automate judgment.

---

## Storage X

**Storage X** is the authoritative, immutable system of record for:
- BELIEF,
- TRUTH,
- EVIDENCE,
- XRESULT artifacts,
- and OPEN ISSUES.

Storage X:
- preserves historical integrity,
- supports traceability,
- enables audit and oversight,
- and separates knowledge retention from execution and analysis.

---

## Semantic Plan

A **Semantic Plan** is the human-readable articulation of security intent that forms the root of BELIEF.

It describes:
- zones and trust boundaries,
- allowed and prohibited behaviors,
- assumptions,
- and risk rationale.

The Semantic Plan is authoritative.  
All structured representations are derived from it and must remain faithful to its meaning.

---

## Explicit Allow / Implicit Deny

**Explicit Allow / Implicit Deny** is the enforcement principle stating that:
- only specifically authorized interactions are permitted,
- all other interactions are denied by default,
- and denial does not require enumeration.

This principle must be expressed in BELIEF and verifiable in TRUTH; it cannot be assumed.

---

## Risk Threshold

A **Risk Threshold** is a pre-established boundary that defines when an observed condition requires escalation, acceptance, or action.

Risk Thresholds:
- are defined by humans,
- are external to Model X,
- govern disposition of OPEN ISSUES,
- and prevent ad-hoc or emotional decision-making.

---

## XRESULT

An **XRESULT** is a structured, non-authoritative analytical artifact that evaluates the relationship between BELIEF, TRUTH, EVIDENCE, and declared commitments.

XRESULTs:
- do not enforce controls,
- do not decide risk,
- do not replace deterministic testing,
- and do not grant authority to AI.

They exist to preserve:
- explainability,
- evidence integrity,
- semantic fidelity,
- and defensible oversight.

---

© 2025 Dan Schaupner  
Licensed under the Apache License, Version 2.0.