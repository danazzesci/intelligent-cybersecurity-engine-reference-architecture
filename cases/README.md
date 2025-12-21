# ICE Reference Architecture — Cases

This directory contains **cases** that demonstrate how the Intelligent Cybersecurity Engine (ICE) reference architecture is applied to evaluate specific **security claims** against available evidence.

Cases are **not implementations**, **not findings**, and **not assessments**.  
They are structured reasoning examples that show how the architecture supports **bounded, defensible decision-making**.

---

## What a Case Is

A case illustrates:

- A concrete security claim being asserted
- The evidence presented to support that claim
- What the system can legitimately assert
- Where evidence is insufficient or incomplete
- What decision pressure is created for a human authority

Cases focus on **how reasoning is applied**, not on tooling, dashboards, or scores.

---

## What a Case Is Not

Cases do **not**:

- Declare a system “secure” or “insecure”
- Perform risk scoring or maturity grading
- Predict threats or attacker behavior
- Generate or enforce policy
- Make autonomous decisions

All risk acceptance and judgment remain human responsibilities.

---

## Why Cases Matter

Cases represent the **minimum unit of defensible cybersecurity reasoning**.

They make explicit the separation between:
- **Belief** (what is claimed)
- **Truth** (what is observable)
- **Evidence sufficiency** (what can be justified)
- **Decision** (what a human must decide)

Every advanced use case — ransomware containment, Zero Trust verification, regulatory explainability, insurance defensibility — depends on this reasoning working first.

---

## Relationship to Stories and Use Cases

- **Stories** (`/stories/`) explain *why* a situation matters in human terms  
- **Cases** (`/cases/`) explain *how* the architecture reasons about a claim  
- **Use cases** (`/use-cases/`) (future) formalize tests, artifacts, and enforcement

This separation allows the repository to evolve without premature complexity.

---

## Intended Audience

Cases are written to be readable and meaningful to:

- Security engineers
- Architects and system designers
- Executives and board members
- Risk, legal, and compliance stakeholders
- Regulators and auditors seeking explainability

---

## License

All contents in this directory are licensed under the Apache License, Version 2.0, unless otherwise stated.

---

© 2025 Dan Schaupner. Licensed under Apache License 2.0.