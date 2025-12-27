# Engineering Driver Statement

We are building an AI system for cybersecurity that produces technical results explicitly intended to support the following statement, when made by a CEO, board member, company officer, CISO, or practitioner—before a court, an insurer, shareholders, customers, business partners, regulators, and the public:

> **“I can stand behind our cybersecurity decisions because we examined the risks that were material to our business and stakeholders, made proportionate choices, and maintained oversight as conditions changed.”**

This statement is not marketing language.  
It is the **engineering constraint** that governs this project.

If the system we build cannot truthfully support this statement under scrutiny, then it has failed—regardless of how many controls pass, dashboards are green, or vendors are deployed.

---

## What This Statement Implies for Engineers

This project does **not** exist to:
- Automate security decisions
- Replace human judgment
- Enforce controls
- Optimize alerts
- Produce compliance artifacts by default

It exists to **produce defensible evidence**.

The system’s output must enable a human being to justify cybersecurity decisions **after the fact**, under legal, financial, regulatory, and public scrutiny.

---

## Non-Negotiable Engineering Requirements

### 1. Belief Is Not Truth

- Beliefs about cybersecurity (configurations, policies, plans, risk decisions, semantic expressions) are **inputs**, not ground truth.
- Beliefs are stored **outside** the system.
- The system may consume belief, but it may never authoritatively store, mutate, or enforce belief.

If belief and truth are conflated, the system becomes self-justifying and loses evidentiary value.

---

### 2. Evidence Must Be Deterministic

- Evidence collection must be deterministic, repeatable, and auditable.
- Tests against the digital estate (e.g., firewall enforcement, MFA paths, DLP flows, segmentation) must produce artifacts that can be independently verified.
- The system must prefer *measured reality* over stated intent.

Evidence that cannot be reproduced cannot support oversight.

---

### 3. Evaluation Is Bounded and Non-Authoritative

- Model-based evaluation is permitted only within strict bounds.
- Models may examine evidence and classify results.
- Models may not:
  - Reach into production systems
  - Change configuration
  - Decide outcomes
  - Override human authority

The system supports accountability; it does not assume it.

---

### 4. Oversight Must Be Longitudinal

- Oversight is not a snapshot.
- Results must persist over time.
- The system must support historical comparison, trend detection, and drift visibility.

A system that cannot show *what changed* cannot claim maintained oversight.

---

## Architectural Consequences

To satisfy the driver statement, the system is intentionally designed with:

- **Multiple security zones** to prevent evidence contamination
- **External belief stores** to preserve independence
- **Deterministic collection engines** for reproducibility
- **Bounded models** for classification, not control
- **Persistent result storage** for longitudinal accountability
- **Human-governed disposition** of findings

These are not optional design preferences.  
They are required to maintain the integrity of the claim the system exists to support.

---

## Definition of Success

The system succeeds if, and only if:

- A reasonable, informed third party can review its outputs and conclude:
  - Risks were examined based on observable reality
  - Decisions were proportionate to what was known at the time
  - Oversight was actively maintained as conditions evolved

If the system cannot support that conclusion, it has failed its purpose.

---

## Engineering Litmus Test

Before adding any component, feature, or optimization, engineers should ask:

> *Does this strengthen or weaken a human’s ability to truthfully stand behind their cybersecurity decisions under scrutiny?*

If the answer is **weaken**, the change is out of scope.

---

This document is the **engineering north star** for the Intelligent Cybersecurity Engine Reference Architecture.

Everything else is implementation detail.