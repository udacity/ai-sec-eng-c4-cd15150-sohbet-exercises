# Video: Understanding AI Threat Modeling with MITRE ATLAS
*Module 3.1 | Topic: Understanding AI Threat Modeling with MITRE ATLAS*

---

## Opening Hook

> *"Somebody jailbreaks your customer-support chatbot into issuing a refund it shouldn't. Your security team writes up the incident. Two months later, three other companies independently discover the same trick — and they're describing it in three different ways with no shared vocabulary. That's the problem MITRE ATLAS exists to solve. Same attack, same name, same ID, same place in the catalog. That's how a defensive community starts to compound. And here's the second move: a junior engineer comes back from training and proposes STRIDE-ML for your model. The MLOps lead says 'no, we're using MITRE ATLAS.' The privacy team says 'actually it should be LINDDUN.' They're all right. They're all also missing the point — these frameworks answer different questions at different stages of the system's life. The skill is knowing which one to reach for, when."*

The conceptual job here is two-layered: install ATLAS as the shared adversary-tactics vocabulary, then install the *meta-skill* of choosing among ATLAS, STRIDE-ML, and LINDDUN depending on what stage of the system you're working on.

---

## Key Discussion Points

1. **What ATLAS actually is.** ATLAS stands for "Adversarial Threat Landscape for AI Systems." It's a MITRE-maintained knowledge base of real-world tactics, techniques, and procedures (TTPs) used by adversaries against AI systems. Same shape as ATT&CK for enterprise security — the lineage matters because ATT&CK practitioners can read ATLAS without a steep curve.

2. **TTPs, explained for an audience that isn't pure security.** Tactic = *the goal* the adversary is trying to achieve (Reconnaissance, ML Model Access, Evasion, Data Poisoning, Model Extraction, Prompt Injection). Technique = *how* they achieve it. Procedure = *the specific instance* in the wild. ATLAS catalogs the first two; procedures are case studies and write-ups attached to them.

3. **The tactics worth naming.** Don't list all of them. Anchor on the ones that show up in incident reports: Reconnaissance, ML Model Access, Evasion, Data Poisoning, Model Extraction, Inference (membership inference and model inversion), and the LLM-specific Prompt Injection family (AML.T0051). These are the techniques regulators and incident reports keep citing.

4. **ATLAS is *runtime* and *adversarial*. That's its lane.** ATLAS captures what attackers *actually do* against AI in the wild. It does not cover design-time security flaws, privacy threats, or governance gaps — that's STRIDE-ML and LINDDUN's territory.

5. **Why the IDs matter more than the names.** ATLAS technique IDs (`AML.T0051`, `AML.T0020`, `AML.T0040`) are stable; technique names occasionally change (the catalog has been renaming "ML" to "AI" in some entries). When students reference ATLAS in a threat model or risk register, they should cite the ID. That's how risk registers stay legible over time.

6. **The shape of a useful ATLAS-anchored threat-model row.** Technique ID, technique name, the system architecture the technique applies to (the *scoping rationale* — not boilerplate from the catalog, specific to your system), likelihood and impact ratings, a mapped control family, an owner. A TTP catalog is *input*, not output. The output is a scoped, architecture-specific row.

7. **What ATLAS does *not* do.** It does not tell you the control to use against a technique — that's your job. It does not score likelihood or impact for you. It does not enforce a methodology. It's a vocabulary with examples attached. The discipline is in how you use it.

8. **The community angle.** ATLAS is published with case studies — real-world incidents (often anonymized) indexed by ID. When a regulator asks "is this hypothetical?" the answer is "no, here are documented cases against production systems."

9. **The framework decision tree — STRIDE-ML, LINDDUN, ATLAS.**
   - **STRIDE-ML is the design-time security move.** Microsoft's STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) extended for ML systems. Used *during architecture review*, before code ships. Output: design-level findings — missing input validation, missing model integrity checks, missing audit trails.
   - **LINDDUN is the design-time privacy move.** Linkability, Identifiability, Non-repudiation, Detectability, Disclosure, Unawareness, Non-compliance. Same shape as STRIDE but privacy-flavored. Used during architecture review when the system processes personal data. Connects to GDPR / CPRA design work in Module 11.
   - **ATLAS is the runtime adversary move.** Used *after deployment* (or in pre-launch threat-modeling that mimics production) to ask "if an attacker were trying to abuse this live system, what would they try?" Output: runtime findings — missing prompt-injection defenses, missing rate limits on inference, missing monitoring for exfiltration patterns.

10. **The lifecycle picture.** Design phase → STRIDE-ML and LINDDUN. Pre-launch → ATLAS plus STRIDE-ML in combination. Production → ATLAS-driven monitoring and ATLAS-anchored incident response playbooks. They don't overlap; they layer.

11. **The decision tree, explicit.**
    - Reviewing a *design* before code ships? → STRIDE-ML for security, LINDDUN for privacy.
    - Preparing a *production system* for adversarial reality? → ATLAS.
    - Doing a *combined* AI review board pre-launch sign-off? → ATLAS primary, STRIDE-ML / LINDDUN handoffs for unresolved design issues.
    - Investigating a *live incident*? → ATLAS, because adversary behavior is what you're chasing.

12. **Where they converge: the risk register.** Whichever framework you used, the output lands as rows in the same risk register, mapped back to NIST AI RMF Map and Manage. The framework is the generative tool; the register is the persistent artifact. The framework choice doesn't matter to the auditor — what matters is that the resulting register is well-scoped, well-scored, and well-owned.

13. **Common confusions to head off.** "STRIDE doesn't apply to ML because ML isn't deterministic" — wrong, STRIDE applies to the *system* around the model. "LINDDUN is just GDPR" — wrong, LINDDUN is a modeling technique, GDPR is a regulation. "ATLAS replaces STRIDE-ML" — wrong, different stages, different questions.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| AML.T0051 LLM Prompt Injection on a customer-support chatbot (mirrors ChatPoint demo) | Walk how the technique applies to a public-facing chatbot: scope (public web widget), likelihood (high — public surface), impact (depends on what the chatbot can do — escalates sharply with tool-use). Show that the *scoping* is the work; the technique is just the row label. | Walkthrough — anchor example |
| FinTrust face-matching pipeline through both lenses (mirrors exercise) | One architecture, two reads. At design time, STRIDE-ML surfaces Tampering threats on the image-upload pipeline and Information Disclosure threats on the API response. At runtime, ATLAS surfaces AML.T0015 Evade AI Model (formerly "Evade ML Model") via deepfake / generative-liveness bypass and AML.T0024 Exfiltration via AI Inference API. Both findings are real; both are required. | Walkthrough — second anchor |
| AML.T0020 Poison Training Data | Brief: a fraud model whose training data could be poisoned by adversaries submitting crafted transactions that get labeled as legitimate. Shows ATLAS covers staging attacks, not just runtime. | Brief mention |
| AML.T0024 Exfiltration via AI Inference API | Brief: an API surface that lets an adversary reconstruct training data through repeated queries (membership inference / model inversion). Connects to privacy concerns in Module 11. | Brief mention |
| AML.T0006 Active Scanning | Brief: reconnaissance against an AI system is not science fiction — adversaries probe APIs, look for error messages that leak model architecture, fingerprint version updates. This is one of the FinTrust pre-filled worked examples students will read first. | Brief mention |
| AML.T0048.000 Financial Harm (sub-technique of AML.T0048 External Harms) | Brief: a chatbot that can issue refunds becomes a financial-harm vector under AML.T0048.000. Use the precise sub-technique ID — the parent T0048 covers a family (Financial Harm `.000`, Reputational Harm `.001`, Societal Harm `.002`); cite the sub-ID downstream threat models can cross-walk against. | Brief mention |
| When privacy gets dropped | A team uses STRIDE-ML and ATLAS but skips LINDDUN. The system passes review. Six months later, the privacy team flags an identifiability risk neither framework would have caught. Motivates LINDDUN. | Brief mention |
| The chatbot at design vs production | Same chatbot, two perspectives. STRIDE-ML at design: missing input validation, missing rate limiting, no separation between system prompt and user prompt in the data flow. ATLAS at runtime: prompt injection, external harms via the refund tool. Non-overlapping findings on the same system. | Brief mention with the contrast |

---

## What NOT to Cover

- **How to facilitate a threat-modeling session step-by-step** — implementation module.
- **Specific control families to map TTPs to** — implementation module's Control Family Reference sheet.
- **The Board Brief writing format (Top 3 TTPs, recommended controls, residual risk, Launch / Conditional / No-Go)** — implementation deliverable. Set up the *thinking* here, don't draft the brief.
- **NIST AI RMF function integration** — Module 2 covered this. Reference once: "all of these feed the Map and Manage functions."
- **Exhaustive enumeration of all ATLAS tactics and STRIDE-ML/LINDDUN categories** — overkill. Anchor on named uses; don't read lists.
- **MITRE ATT&CK details** — reference once as the parent framework students may already know.

---

## Additional Notes

- **Analogies.** ATLAS is to AI security what ATT&CK is to enterprise security — the shared map. For students with ATT&CK background, leaning on the parallel saves you ten minutes of setup. For the framework choice: STRIDE-ML and LINDDUN are architectural blueprints reviewed for fire safety before construction; ATLAS is the fire marshal's report after a building has been operating for a year and they've seen real fires in similar structures. You need both. You'd never substitute one for the other.
- **Terminology.** Use "ATLAS" (capitalized acronym). Pair a technique name with its ID on first mention (e.g., "AML.T0051 LLM Prompt Injection") — this trains the habit. Use full names on first mention for STRIDE-ML and LINDDUN. Be precise about "threat model" the verb vs the artifact.
- **Don't oversell ATLAS as complete.** Caveat clearly: the catalog is actively maintained, not exhaustive. Some attack categories — especially in the LLM agent / tool-use space — are evolving faster than the catalog. ATLAS is the *best available* shared vocabulary, not a final taxonomy.
- **Avoid:** treating ATLAS as a checklist. The catalog runs to dozens of techniques; you do not threat-model against all of them. You pick the small subset relevant to *your* architecture. Avoid picking a "winner" framework — the module should leave students with the *judgment* to choose.
- **A grounded line worth seeding:** "The biggest mistake I see teams make with ATLAS is they treat it as a list of homework. It's not. It's a list of *vocabulary*. The homework is figuring out which five entries actually apply to the thing you're building." And: "I've watched teams burn six weeks doing STRIDE-ML on a production system that was already shipping prompt-injected outputs in the wild. They had the right work. They had the wrong framework for the moment they were in."
- **A reflective beat to drop near the end:** "Look at the last threat model your team produced. Which lens were they using? And what did they miss because they didn't switch lenses partway through?"
- **Connection to the implementation module.** Students will scope five ATLAS TTPs against FinTrust — a face-matching identity-verification ML pipeline over a public mobile-app KYC endpoint. They'll write architecture-scoping rationale per TTP, score likelihood and impact, map to control families, and produce a Board Brief with a Launch / Conditional / No-Go recommendation. After this module they should be able to predict that the same TTP (e.g., AML.T0015 Evade AI Model, formerly "Evade ML Model") looks utterly different for face-matching than it does for the chatbot in the demo — and that the *scoping work* is what makes that difference visible.

---
