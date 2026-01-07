# Testable Cybersecurity Evidence Lab (CentOS)

## What This Is (Read This First)

This repository contains a **hands-on lab you can run immediately** to test whether your network security beliefs actually hold up when exercised against real system behavior.

You do **not** need enterprise tooling.
You do **not** need multiple machines.
You do **not** need a SIEM.
You do **not** need to wait for anything to be “production ready.”

If you have:
- a single CentOS system, and
- access to a low-scale, API-accessible language model,

you can run this lab, observe real evidence, and produce a concrete answer to a simple question:

> *Does the security posture I believe I have actually survive contact with reality?*

---

## What You Will Do

In this lab, you will:

1. Create three minimally virtualized hosts and a firewall on a single CentOS system using native Linux networking.
2. Declare what you believe the firewall allows and blocks as a **data structure**, not a diagram.
3. Generate real traffic and run `nmap` from multiple perspectives.
4. Collect logs and scan results as plain text files.
5. Bundle beliefs and evidence into a single, replayable input file.
6. Submit that file to a small language model whose only job is to evaluate belief vs. evidence.
7. Receive a **strict, machine-readable result** (PASS / FAIL / DELTA).
8. Preserve the result as a single artifact you can inspect, compare, or share.

That’s it.

No agents.  
No dashboards.  
No magic.

---

## What This Is Not

Be clear about the boundaries:

- This is **not** a product.
- This is **not** a reference architecture for production.
- This is **not** continuous monitoring.
- This is **not** a SIEM replacement.
- This is **not** autonomous security decision-making.

This is a **lab** designed to make the belief → test → evidence loop explicit and undeniable.

---

## Why This Exists

Most security failures are not caused by missing controls.
They are caused by **unexamined assumptions**:

- “We only allow 443.”
- “That subnet can’t reach this one.”
- “The firewall would block that.”
- “We would see it if that happened.”

This lab gives you a way to **prove or disprove those statements** using tools you already understand.

If the loop can’t work here—clearly, cheaply, and visibly—it won’t work when buried under layers of tooling.

---

## Core Principles

This lab is built around a few non-negotiable principles:

- **Belief must be explicit**  
  Security intent is written down as data before testing begins.

- **Behavior must be real**  
  Traffic, scans, and enforcement are not simulated.

- **Evidence must be inspectable**  
  Logs and scans are plain text files on disk.

- **Interpretation must be bounded**  
  The model interprets; it does not collect, enforce, or persist.

- **Results must be durable**  
  Each run produces a standalone artifact that survives the system.

---

## Environment Assumptions

The lab assumes:

- A single CentOS system
- Native Linux networking features:
  - network namespaces
  - virtual ethernet pairs
  - iptables / netfilter
- Standard system tools:
  - `curl`, `openssl`
  - `nmap`
  - `rsyslog`
- Python 3 for orchestration
- Filesystem-based storage (no database required)
- One external dependency:
  - a low-scale, API-accessible language model used only for interpretation

These assumptions are **intentional** and **acceptable** for a lab focused on mechanics rather than scale.

---

## Repository Structure (High Level)

```text
.
├── plans/          # Security beliefs and threat context (JSON)
├── evidence/       # Logs and nmap outputs (plain text)
├── engine_x/       # Python orchestration routines
├── db/
│   ├── temporal/   # Per-run input bundles (archived)
│   ├── permanent/  # Append-only XRESULT history
│   └── artifacts/  # One file per lab run (primary output)
└── README.md

Exact filenames and layouts may vary, but the roles do not.

⸻

The Output You Care About

Each lab run produces:
	•	One per-run artifact
A timestamped file containing:
	•	declared belief
	•	observed evidence
	•	structured evaluation (XRESULTS)

This file is the object of study.

You can:
	•	read it by hand
	•	diff it against previous runs
	•	parse it with Python
	•	submit it to another model
	•	attach it to a ticket
	•	use it in teaching or review

The system itself can disappear.
The artifact should still make sense.

⸻

How to Use This Repository

You are encouraged to:
	•	Run the lab as written
	•	Change the firewall rules
	•	Break the assumptions on purpose
	•	Add or remove scan perspectives
	•	Modify the belief structure
	•	Swap out the model
	•	Compare results across runs

Nothing here is fragile.
Nothing here is sacred.

⸻

Bottom Line

This repository exists to show that defensible cybersecurity does not start with tooling.

It starts with:
	•	explicit belief,
	•	deliberate testing,
	•	honest evidence,
	•	bounded interpretation,
	•	and preserved results.

If you can run CentOS and make an API call, you can do this.

Let ’er rip.