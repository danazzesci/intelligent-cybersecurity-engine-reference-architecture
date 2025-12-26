# Intelligent Cybersecurity Engine (ICE) — Reference Architecture (ASCII)

This diagram is the **normative ASCII representation** of the ICE Reference Architecture.
It defines security zones, trust boundaries, evidence flow, and separation of duties.

The diagram is intentionally ASCII to preserve:
- Diffability
- Copy/paste fidelity
- Governance traceability

text```
┌──────────────────────────────────────────────┐
│            Security Management Zone           │
│                                              │
│   ┌──────────────┐                           │
│   │   Model X    │                           │
│   │ (Local LLM)  │                           │
│   └──────▲───────┘                           │
│          │ Controlled Submission              │
│          │                                   │
│   ┌──────┴───────┐                           │
│   │   Engine X   │                           │
│   │ (Script Exec │                           │
│   │  + Orches.)  │                           │
│   └──────▲───────┘                           │
│          │ Read / Write Evidence              │
│          │                                   │
│   ┌──────┴───────┐                           │
│   │  Storage X   │◄──────────────────────┐  │
│   │ (Belief +    │                       │  │
│   │  Truth +     │                       │  │
│   │  Evidence)   │                       │  │
│   └──────────────┘                       │  │
│                                          │  │
└──────────────────────────────────────────┘  │
                                               │
        Semantic Plan + Derived Belief          │
        (Human Authored / Versioned)            │
                                               │
               Security Administrator           │
                                               │
────────────────────────────────────────────────────────────────────

        Zone A                                   Zone B
┌──────────────────┐                   ┌──────────────────┐
│   Host A         │                   │   Host B         │
│                  │                   │                  │
│   ┌──────────┐   │                   │   ┌──────────┐   │
│   │  Ta      │   │                   │   │  Tb      │   │
│   │ (nmap)   │   │                   │   │ (nmap)   │   │
│   └────▲─────┘   │                   │   └────▲─────┘   │
│        │ Test    │                   │        │ Test    │
│        │ Traffic │                   │        │ Traffic │
│        ▼          │                   │        ▼          │
└────────┼──────────┘                   └────────┼──────────┘
         │                                         │
         │           Controlled Interface          │
         │    (Explicit Allow / Implicit Deny)     │
         │                                         │
         ▼                                         ▼
                ┌──────────────────────────┐
                │        Firewall F         │
                │  (Facilitation + Guards) │
                └───────────▲──────────────┘
                            │
                            │ Read-Only Logs
                            │ (Router + FW)
                            │
                ┌───────────┴──────────────┐
                │        Firewall Fx        │
                │   (Admin Tap / Control)  │
                └───────────▲──────────────┘
                            │
                            │ SFTP (Logs + Tests)
                            │
                            ▼
                      ┌───────────┐
                      │ Engine X  │
                      │ (Observer │
                      │ + Scripts)│
                      └───────────┘

```

## Semantics and Constraints

- **Security Management Zone**  
  Dedicated control plane for governance, orchestration, and evidence custody.

- **Model X**  
  Local LLM operating under controlled submission rules.
  No direct write access to enforcement or network controls.

- **Engine X**  
  Executes scripts, orchestrates tests, and manages evidence lifecycle.

- **Storage X**  
  System of record for BELIEF, TRUTH, and EVIDENCE objects.

- **Semantic Plan**  
  Human-authored, version-controlled intent that defines expected state.

- **Zone A / Zone B**  
  Segmented security zones subject to validation testing.

- **Controlled Interface**  
  Explicit allow rules only; implicit deny by default.

- **Firewall F**  
  Enforcement point providing facilitation and guardrails.

- **Firewall Fx**  
  Administrative tap providing read-only visibility and control-plane access.

This diagram is normative for ICE RA discussions and audits.

---

© 2025 Dan Schaupner  
Licensed under the Apache License, Version 2.0.