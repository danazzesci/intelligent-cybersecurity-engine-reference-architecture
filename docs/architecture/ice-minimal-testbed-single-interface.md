# ICE Minimal Testbed — Single-Interface AI Evidence Loop

## Purpose

This document defines the **minimal authoritative testbed** for the Intelligent Cybersecurity Engine (ICE) Reference Architecture.

It represents the **smallest possible system** capable of continuously proving — not assuming — that a single security-zone interface behaves as intended, while preserving evidence and keeping humans fully accountable.

This testbed is:
- Normative
- Deterministic
- Auditable
- Regulator-safe
- Free of autonomous AI control

---

## System Components (Authoritative)

### Security Zones

- **Zone A**
  - Host A
  - Test unit **Ta** (e.g., `nmap`)
- **Zone B**
  - Host B
  - Test unit **Tb** (e.g., `nmap`)
- **Security Management Zone**
  - **Engine X**
  - **Model X** (locally hosted)
  - **Storage X**

### Network Enforcement

- **Firewall F**
  - Governs the interface between Zone A and Zone B
  - Implements facilitation and safeguards
- **Firewall Fx**
  - Security administration tap
  - Controlled route for observation and administration only
  - No data-plane shortcut between Zone A and Zone B

---

## Authoritative Control Relationships

- **Zone A ↔ Zone B**
  - Communication occurs only via **Firewall F**
  - Explicit allow rules
  - Implicit deny by default
- **Ta / Tb**
  - Test the interface from inside each zone
  - Validate both positive and negative paths
- **Firewall Fx**
  - One-way / restricted management visibility into Firewall F
- **Engine X**
  - Executes deterministic scripts only
  - No autonomous control authority
- **Model X**
  - Local model
  - No direct access to network devices
  - No execution capability
- **Storage X**
  - Single source of retained BELIEF, TRUTH, EVIDENCE, and RESULTS

This separation of duties is intentional and defensible.

---

## End-to-End Control Loop (Applied)

### 1. Supervision — Human Semantic Intent

**Who**
- Security Administrator

**What**
- Human-readable semantic security plan describing:
  - Zones
  - Permitted interactions
  - Explicit denials
  - Risk rationale

**Where**
- Stored in **Storage X**

This is the **only source of intent**.

---

### 2. Belief System — Structured, Derived

**Artifacts**
- Semantic plan (authoritative prose)
- Derived data structures representing desired state:
  - Expected firewall rules
  - Expected zone isolation
  - Expected test outcomes

**Properties**
- Derived, not substitutive
- Version-controlled
- Stored in **Storage X**

This constitutes the **BELIEF object**.

---

### 3. Truth — Observed, Accessible

**Collected by Engine X via Firewall Fx**
- Firewall router logs
- Firewall firewall logs
- Test results from:
  - Ta (Zone A perspective)
  - Tb (Zone B perspective)

**Transport**
- SFTP only
- Read-only
- Predictable paths

This constitutes the **TRUTH object**.

---

### 4. Differentiation — Alignment Check

#### Layer 1: Deterministic Scripts

**Built by**
- Security Administrator (separate process)

**Executed by**
- Engine X

**Purpose**
- Compare:
  - BELIEF vs TRUTH
  - Expected rules vs actual rules
  - Expected blocks vs observed behavior

**Output**
- Structured delta artifacts

No interpretation. No language.

---

#### Layer 2: Models — Semantic Coherence

**Inputs to Model X**
- BELIEF
- TRUTH
- Script-produced deltas
- Script outputs

**Constraints**
- Controlled submission
- No external connectivity
- No execution capability
- No state mutation

Model X answers:

> *Do these observed differences violate the meaning of the intent?*

This preserves semantic fidelity without granting authority.

---

### 5. Dissimilarity — Delta Production

**Produced by**
- Scripts (ground truth)
- Enriched by Model X (semantic meaning)

**Examples**
- Over-permissive rule
- Missing deny
- Identity scope drift
- Test failure contradicting belief

The system produces **explicit, inspectable deltas** — not scores.

---

### 6. Automation — Verification, Not Authority

**Engine X**
- Executes only:
  - Tested
  - Predetermined
  - Approved scripts

**Purpose**
- Verify containment paths
- Re-run tests
- Re-collect logs

AI may propose scripts.  
Humans approve.  
Engine executes.

---

### 7. Control — Bounded, Same Rules

If pre-authorized:

**Engine X may**
- Disable a violating rule
- Quarantine the interface
- Freeze a configuration

**Constraints**
- No new permissions
- No expansion of access
- All actions logged

Control authority is symmetric with automation constraints.

---

### 8. Outcome & Evidence

Stored in **Storage X**:
- Time-stamped logs
- Test outputs
- Delta records
- Model X semantic reports
- Script results

**Properties**
- Immutable
- Correlated
- Retained

This closes the loop back to BELIEF.

---

### 9. Risk Management

**Security Administrator compares**
- Script outputs
- Model X semantic report
- XRESULT
- Pre-established risk thresholds

**Decision**
- (a) Continue → store results
- (b) Open incident

Exploitability is assessed **here**, not earlier.

---

### 10. Knowledge Management & Preservation

**Continuous**
- Cycles repeat
- Drift remains detectable
- Rationale is preserved
- Evidence accumulates

AI acts as:
- Semantic memory
- Structural translator
- Drift amplifier

Humans remain accountable.

---

## Design Rationale

### Included (Intentionally)

- Two zones
- One interface
- Deterministic tests
- Explicit BELIEF / TRUTH separation
- Local model
- Separate engine vs model
- Read-only observation paths

### Excluded (Intentionally)

- No AI agents
- No autonomous policy changes
- No cloud dependency
- No dashboards without evidence
- No scoring without inspection
- No model in the control plane

---

## One-Sentence Validation

This testbed is the smallest possible system that can continuously prove — not assume — that a single security-zone interface behaves as intended, detect drift, preserve evidence, and keep humans fully accountable while using AI only to preserve semantic coherence.

---

© 2025 Dan Schaupner  
Licensed under the Apache License, Version 2.0.