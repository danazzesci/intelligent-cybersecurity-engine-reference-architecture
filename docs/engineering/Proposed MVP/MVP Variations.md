# MVP Permutation Matrix (Technology Variances)

This table enumerates **valid MVP implementation permutations** (hardware + software + IaaS/PaaS/SaaS options) that can all achieve the same outcome:
**belief + observed test evidence → deterministic normalization/DELTA → bounded model evaluation → XRESULT storage → human oversight disposition**.

> Reminder: These are MVP permutations. They preserve the architectural constraints:
> - **Model does not gather evidence**
> - **Model does not enforce**
> - **Human oversight decides**
> - **Belief remains external/ingested per run**

---

## Table A — End-to-End MVP Profiles (Permutations)

| MVP Profile (Permutation) | Hardware / Hosting | Compute Style (ENGINE X + deterministic control) | Model X Option | Storage M Option | Oversight Interface | Belief Input Method | Probe/Test Result Ingest | When This MVP Fits Best |
|---|---|---|---|---|---|---|---|---|
| **P1: Single Linux Box + SaaS Model** | 1 commodity server/VM | Local processes + scripts (single host) | SaaS LLM API | Local SQL | Local web server (or CLI) | File-based YAML/JSON + manual updates | File drop/export + simple API pulls | Fastest “prove the flow” pilot |
| **P2: Single Linux Box + Local Private Model** | 1 server/VM (optionally GPU) | Local processes + scripts | Local inference runtime | Local SQL | Local web server | Files or Git pull | File drop/export + API pulls | Regulated environments that want no external model calls |
| **P3: Hybrid Linux + SaaS Storage + SaaS Model** | Small Linux host/VM | Local deterministic runtime | SaaS LLM API | Managed SQL (DBaaS) | Web app (self-hosted) | Pull from external belief repo + cache snapshot | APIs/webhooks → local normalizer | When you want minimal ops burden but keep deterministic logic under your control |
| **P4: Cloud Serverless Deterministic + SaaS Model** | Cloud (no fixed servers) | Serverless functions + workflows | SaaS LLM API | Managed SQL / serverless DB | Serverless web app | Belief pulled via API per run | Probe outputs delivered via API/webhook | When infra teams prefer serverless and event-driven workflows |
| **P5: Containerized MVP (Laptop/Workstation) + SaaS Model** | Developer workstation | Containers for deterministic logic | SaaS LLM API | Local embedded SQL | Local UI | Manual belief entry + files | Manual import of tool exports | “Demo in a room” proof-of-concept |
| **P6: Air-Gapped Lab MVP** | On-prem isolated lab server(s) | Local deterministic runtime | Local private model (or no-model mode*) | Local SQL | Local web UI | Offline belief bundles | Offline probe exports | Academic / classified / air-gapped validation |
| **P7: MSP / Shared Tenancy MVP** | Multi-tenant hosts | Containerized per-tenant deterministic runners | SaaS or local model (tenant policy) | Per-tenant logical DB | Multi-tenant web UI | Tenant-specific belief adapters | Tenant probe adapters | When you need strict tenant separation and repeatability across clients |
| **P8: “Manual Model Invocation” MVP (Copy/Paste)** | Any Linux box | Local deterministic runtime | Human-mediated prompt (copy/paste) | Local SQL | CLI or simple UI | Manual belief + evidence bundle | Manual imports | Earliest possible validation of schema + XRESULT output format |

\* *No-model mode is allowed for early pilots if you treat the “model evaluation” as a deterministic classification stub. (It’s still MVP-valid for flow testing, just not ML-evaluated.)*

---

## Table B — Component-by-Component Technology Options (Mix-and-Match)

| MVP Element | Minimum Option | Common Variants | IaaS / PaaS / SaaS Options | Notes / Tradeoffs |
|---|---|---|---|---|
| **Deterministic execution (ENGINE X + control logic)** | Scripts on Linux | Containers; workflow engine; serverless functions | IaaS VM; PaaS container platform; serverless compute | Must remain deterministic and auditable |
| **Belief ingestion (per-run snapshot)** | File bundle (YAML/JSON) | Git pull; API fetch; DB query | SaaS config repo APIs; PaaS integration workflows | Key is repeatable “belief snapshot” + provenance |
| **Probe / tool result ingestion** | Export files + importer | REST API pull; webhook push; log shipping | SaaS security tool APIs; PaaS event bus | ICE RA does not dictate probe tools—only ingestion normalization |
| **Normalization & schema validation** | Local parsers + schema checks | Central schema registry; versioned transforms | PaaS schema registry; workflow validators | Versioning prevents “silent reinterpretation” of old results |
| **DELTA computation** | Deterministic diff scripts | Rule engines; policy-as-code comparisons | PaaS rule engines; serverless jobs | DELTA should be reproducible without the model |
| **Model invocation (MODEL X)** | SaaS LLM API | Local private model; small local model | SaaS model APIs; private endpoint; on-prem inference | Must not have direct access to belief stores/probes/estate |
| **Prompting / model constraints** | Structured prompt templates | Function/tool calling; JSON schema outputs | SaaS structured output modes | Prompting is implementation detail; output schema is the real control |
| **XRESULT formatting** | JSON output writer | Signed envelopes; schema registry integration | Serverless formatting step | Keep machine-readable canonical record as the source of truth |
| **Storage M** | Local SQL DB | Managed SQL; object store + index | DBaaS; serverless DB; data warehouse | SQL is great for longitudinal queries and audits |
| **Analytics** | SQL queries + reports | Stream processing; BI dashboards | PaaS analytics; SaaS BI | Analytics must not rewrite results—only query and summarize |
| **Oversight interface** | CLI | Web UI; API; dashboard | PaaS web app; SaaS portal shell | Human disposition is the “governance anchor” |
| **Audit trail** | File logs + DB tables | Append-only logs; signed event records | Logging-as-a-service | Don’t skip this; it’s core to defensibility |

---

## Table C — “Constraints Check” Across Permutations

| Constraint | Must Hold In Every MVP Permutation | How to Implement (Any Tech) |
|---|---|---|
| Model cannot gather evidence | MODEL X only receives an evidence package | Network egress limits + invocation only via control plane |
| Model cannot enforce or remediate | Outputs are advisory XRESULT records | No write privileges to estate systems |
| Belief remains external & snapshotted | Belief is ingested per run | Belief bundle + provenance fields |
| Deterministic DELTA exists independent of model | DELTA computed pre-model | Scripts / rules / diffs |
| Human oversight disposition required | Human decides ticket vs attestation | UI/CLI workflow requiring explicit action |
| Longitudinal record persists | XRESULT history stored | SQL tables + run metadata |

---

## License & Copyright

© 2025 Dan Schaupner  

Licensed under the **Apache License, Version 2.0** (the “License”);  
you may not use this file except in compliance with the License.  
You may obtain a copy of the License at:

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software  
distributed under the License is distributed on an **“AS IS” BASIS**,  
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
See the License for the specific language governing permissions and  
limitations under the License.