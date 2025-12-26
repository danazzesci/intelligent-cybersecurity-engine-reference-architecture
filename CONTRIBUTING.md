# Contributing

Thanks for your interest in improving this repository.

## Purpose of this repo

This repository is published as a **public reference architecture and evidence-oriented design artifact**. Contributions are welcome **when they improve clarity, correctness, testability, and defensibility**—without changing the project’s core intent.

## Quick rules (read this first)

- **Use Issues first.** If you have an idea, open an Issue before writing a large PR.
- **Small PRs win.** Keep changes narrowly scoped and easy to review.
- **No sensitive data.** Do not include secrets, customer data, logs with PII, or proprietary internal materials.
- **No third-party IP.** Only submit content you wrote yourself or have the right to license to this project.
- **No “silent scope changes.”** If your change alters core definitions, trust boundaries, or governance assumptions, propose it as an Issue and request discussion first.

## What we welcome

- Corrections to technical accuracy, terminology, and definitions
- Tightening of architecture statements (clearer boundaries, invariants, assumptions)
- Test cases, deterministic scripts, or test harness improvements
- Better evidence schemas / data structures (with examples)
- Documentation improvements (diagrams, walkthroughs, glossaries)
- New XRESULT examples and justifications (clearly labeled)

## What we do *not* accept

- Vendor marketing content or product placement
- Unverifiable claims (“AI will…”, “this guarantees…”) without a falsifiable test path
- Large rewrites that break conceptual continuity without prior discussion
- Code or text copied from other repos, blogs, books, or standards without permission
- Anything that meaningfully weakens the project’s “human-governed” boundary

## How to propose changes

### 1) Open an Issue
Include:
- **What problem are you solving?**
- **What file(s) does it affect?**
- **What is the smallest acceptable change?**
- **How would we test or verify it?** (even if the answer is “doc-only”)

### 2) Submit a Pull Request
Please include:
- A clear summary of the change
- Why it improves correctness / defensibility / testability
- Any assumptions introduced or removed
- Links to the Issue it addresses (e.g., `Fixes #123`)

## Style guidance

- Prefer **plain English first**, then **operator/engineering language** when needed.
- Use consistent terms:
  - **BELIEF** = declared intent / expectations / hypotheses
  - **TRUTH** = observed and test-backed state (what you’d swear to under witness)
  - **DRIFT/DELTA** = mismatch between expected and observed state
  - **OPEN ISSUE** = a recorded mismatch routed to accountable decision-making
- Avoid anthropomorphizing AI. Use “recommend,” “classify,” “summarize,” “translate,” not “decide,” “judge,” “conclude.”

## Tests and scripts

If you contribute scripts or test cases:
- Keep them deterministic and reproducible
- Document prerequisites and expected outputs
- Do not assume privileged access unless clearly stated
- Prefer safe-by-default behaviors and include guardrails

## Licensing and rights (important)

By submitting a pull request, you represent and agree that:

1. **You have the right** to submit the contribution (it is your original work or you have permission to contribute it).
2. Your contribution may be **incorporated into this repository** and **distributed under the same copyright and licensing terms** as the project.
3. You are not submitting confidential, proprietary, or restricted materials.

If you are unsure whether you have the right to submit something, **do not submit it**—open an Issue instead and describe the idea at a high level.

## Review process

- Maintainers may request changes or alternative approaches.
- Not all PRs will be merged.
- Merged contributions may be edited for consistency, clarity, or maintainability.

## Security

If you believe you have found a security issue in any code, scripts, or examples in this repo:
- Do **not** open a public Issue with exploit details.
- Instead, open an Issue that says “Security concern” with minimal detail and request a private path for disclosure.

---

Thank you for helping improve the rigor and usefulness of this work.
