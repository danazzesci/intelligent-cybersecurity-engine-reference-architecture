# Testable Cybersecurity Evidence Lab (CentOS)

## Abstract (No-BS, Builder Version)

This is a **hands-on lab you can run right now** to test whether your network security beliefs are actually true.

You stand up three hosts and a firewall on a single CentOS box using native Linux networking. You write down what you *think* is allowed and blocked as a data structure. You generate real traffic and run nmap from different sides. You collect the logs and scan output. You bundle all of that into one file and hand it to a small ChatGPT-class model whose only job is to tell you, in a strict, machine-readable way, whether reality matches your belief.

No SIEM. No agents. No dashboards. No vendor magic.

Everything runs locally except the model call. Evidence is plain text. Storage is the filesystem. The output is a single artifact per run that says **PASS**, **FAIL**, or **here’s the delta**, and points to the exact logs and scans that justify it.

This is not a product, and it’s not meant to scale. It’s a **proof that the belief → test → evidence loop can be made explicit** using tools you already understand. If you can run CentOS and call an API, you can build this, break it, extend it, or throw it away after you learn something.

If you’ve ever said *“the firewall should block that”* or *“we only allow 443”* and realized you didn’t actually have a clean way to prove it, this lab is for you.

---

## Narrative: A Practical Lab for Exploring Testable Cybersecurity Evidence

The first attempt is designed as a **practical, self-contained lab** that can be assembled on a single CentOS system using native operating system capabilities. The intent is to lower the barrier to experimentation and make the mechanics of the approach immediately accessible, rather than to prescribe a finished system or a required implementation path.

A single CentOS host is sufficient to construct the lab. Using standard Linux networking primitives, the system is configured to represent **three minimally virtualized hosts and a firewall**, with the firewall separating two of the hosts from a designated privileged resource. All segmentation, routing, and enforcement are handled through native commands and kernel features, rather than virtual machines, containers, or orchestration frameworks. This keeps the setup transparent and easy to reason about.

The firewall policy itself is intentionally simple: one explicitly permitted path and explicit denial of everything else. This allows the lab to focus on whether declared intent is actually enforced and observable, rather than on policy complexity. To test enforcement from multiple perspectives, common network utilities—most notably **nmap**—are used to probe the firewall in both directions and from different sources. These tests produce concrete, interpretable results that reflect real system behavior.

For the purposes of this lab, **logs and scan outputs remain local** to the CentOS system. They are treated as available evidence rather than streamed to a centralized collection platform. This assumption keeps the lab lightweight and avoids introducing dependencies that are orthogonal to the core question being explored.

Security intent is captured explicitly by expressing the **network architecture, access expectations, and relevant threat context in a structured data file**. This file represents the system’s belief about its own security posture. It is not derived from configuration or logs and does not depend on runtime inspection. It exists as a declared input, against which observed behavior can be evaluated.

A simple **Python routine** running on the same CentOS host coordinates the lab cycle. Its job is strictly mechanical. It gathers the available logs, scan results, belief data, and threat context into a single consolidated file. This file serves as the complete input to the evaluation step. For the lab, the file is archived after use so that each run can be revisited or compared later, but nothing about the approach requires long-term retention.

That consolidated input is then submitted to a model representing **Model X**. For this lab, Model X can be a **low-scale, commercially available language model accessed via API**, constrained to a narrow task: evaluate whether the declared beliefs align with the observed evidence and return results in a strict, predefined structure. The model is not responsible for collecting evidence, enforcing policy, or managing system state; it exists solely to interpret belief versus evidence and return results in a consistent format.

The model’s response is returned to the Python routine, which validates the structure, appends the results to a flat-file history, and also emits a **single, timestamped output file** representing that specific test cycle. This file is the primary artifact of interest for the lab. It can be inspected directly, analyzed programmatically, or submitted to other tools or models if desired.

The overall effect is a lab that demonstrates, end to end, how security intent can be declared, tested, interpreted, and preserved using ordinary systems and modest tools. Nothing in the setup is specialized or proprietary beyond the optional use of a small external model for interpretation. Anyone with a CentOS system and access to a suitable model can reproduce or adapt the lab to explore the same questions, modify assumptions, or extend the approach in their own direction.

The lab is intentionally permissive in this sense: it is meant to be **run, broken, and challenged**, not finalized or guarded.

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