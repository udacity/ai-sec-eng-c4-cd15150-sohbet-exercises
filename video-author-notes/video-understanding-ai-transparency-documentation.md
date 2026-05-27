# Video: Understanding AI Transparency Documentation
*Module 9.1 | Topic: Understanding AI Transparency Documentation*

---

## Opening Hook

> *"Six months after launch, a regulator emails. They want the technical documentation for your AI system under EU AI Act Article 11. You forward the Model Card. They reply: 'this is one document. Article 11 references Annex IV. Where is the rest?' That's the moment a lot of teams discover that 'we have a Model Card' is not the same as 'we have transparency documentation.' A Model Card is *one* artifact in a stack of four, and the stack has to be designed to satisfy three very different audiences — internal engineering, customers, and regulators — without contradiction. The skill this module installs is knowing what each artifact is for, what it isn't for, and how the four pieces line up against the law."*

The conceptual job is to install three things: (1) transparency documentation is a *stack*, not a document, (2) each artifact serves a distinct audience and answers distinct questions, and (3) the stack as a whole maps onto regulatory obligations — particularly Annex IV of the EU AI Act.

---

## Key Discussion Points

1. **The four-artifact transparency stack.**
   - **Model Card** — describes the *model itself*. Intended use, performance, evaluation results, fairness, security considerations, caveats, limitations. Audience primarily internal teams and downstream customers integrating the model.
   - **Datasheet for Datasets** — describes the *training and evaluation data*. Provenance, collection methodology, known biases, demographic distributions, licenses, consent posture. Audience primarily data engineering, ML, legal.
   - **System Card** — describes the *deployed system*, not just the model. Runtime architecture, monitoring approach, human oversight design, integration with other systems, operational metrics. Audience primarily operations, customers, deployers.
   - **AI Impact / Risk Assessment** — describes the *broader impact*. Affected populations, potential harms, mitigations, fundamental-rights considerations. Audience primarily regulators, legal, AI review board.
   
   Each artifact has a primary audience and a primary question. Don't conflate.

2. **No single artifact replaces the others.** The Model Card is what most teams ship first. It's a necessary piece. It is *not* sufficient. Annex IV of the EU AI Act expects information that crosses all four artifacts: training data details (Datasheet territory), monitoring approach (System Card territory), impact on affected persons (Impact Assessment territory). The Article 11 obligation is satisfied by the *stack collectively*, not by any one artifact.

3. **The audience-tailoring problem.** The same underlying technical truth has to be communicated three different ways:
   - **Internal** — full technical detail, including known limitations, residual risk, red-team findings. Honest. Sometimes uncomfortable.
   - **Customer** — enough technical detail to integrate safely. Includes intended use, recommended deployment guardrails, known failure modes, support channels.
   - **Regulator** — formal language, statutory anchors (which Article, which Annex section), conformity-assessment evidence, post-market monitoring plan.
   
   Same facts, different framing. The internal version is rarely the version you ship externally; the external version cannot contradict the internal version. Drift between them is what gets organizations in trouble.

4. **Model Card structure — the sections that matter.**
   - **Model Details** — owner, version, training compute, framework, intended audience.
   - **Intended Use** — primary use cases, out-of-scope uses, downstream user assumptions.
   - **Factors** — demographic / contextual factors the model behavior depends on.
   - **Metrics** — performance metrics overall *and* by subgroup. Subgroup breakdown is the part most Model Cards skip. Connect to Module 10.
   - **Evaluation Data** — what was used to compute the metrics. What was excluded. Why.
   - **Training Data** — high level (Datasheet carries the detail).
   - **Quantitative Analyses** — the actual numbers behind the metrics.
   - **Security Considerations** — known attack vectors (tagged with ATLAS IDs where applicable), mitigations, residual risks, red-team findings. This is the section the implementation module focuses on.
   - **Caveats and Limitations** — what the model is NOT validated for. Out-of-distribution behavior. Known failure modes.
   - **Ethical Considerations** — fairness posture, affected populations, potential harms.

5. **The security-considerations section deserves its own paragraph.** Tag every known attack vector with its MITRE ATLAS ID (e.g., `AML.T0015 Evade ML Model`, `AML.T0051 LLM Prompt Injection`). Document the mitigations. Document the *residual* risk after mitigations. Document red-team findings — not just the headline numbers but the qualitative findings. A Model Card whose security section says "no known issues" is a Model Card that didn't try. Honest security sections build trust with sophisticated reviewers.

6. **The Datasheet for Datasets parallel.** Train students to expect:
   - **Motivation** — why the dataset was created.
   - **Composition** — what's in it.
   - **Collection Process** — how it was gathered, with consent and licensing detail.
   - **Preprocessing** — what cleaning, augmentation, labeling was applied.
   - **Uses** — recommended uses and known unsuitable uses.
   - **Distribution** — license terms.
   - **Maintenance** — update cadence, deprecation plan.
   
   The Datasheet is where regulators look first when bias questions come up. "Where did the training data come from?" lives here.

7. **System Card vs Model Card — the operational vs the artifact.** The Model Card describes the *model*. The System Card describes the *deployed system* — the model plus the scaffolding, monitoring, human oversight, fallback behavior, integration points. The same model can have multiple System Cards (one per deployment context). The same System Card can wrap multiple models. Don't conflate them. The System Card is where Article 12 (logging), Article 14 (human oversight), Article 72 (post-market monitoring) get their documentation home.

8. **The AI Impact / Risk Assessment.** This is where affected-population analysis, fundamental-rights considerations, and stakeholder consultation get documented. It is the artifact that the AI review board uses to authorize the launch. In the EU context this overlaps with the Fundamental Rights Impact Assessment (FRIA) under EU AI Act Article 27 for deployers of certain High-Risk systems. In the broader context it overlaps with traditional Privacy Impact Assessment (PIA) and Data Protection Impact Assessment (DPIA).

9. **Mapping the stack to EU AI Act Article 11 / Annex IV.** This is the bridge to Module 4 and the centerpiece of the exercise. Annex IV has nine sections covering general description, training and evaluation data, monitoring approach, system characteristics, accuracy and cybersecurity, risk management, conformity assessment evidence, post-market monitoring, EU declaration of conformity. The Model Card alone covers maybe sections 1, 4, 5, 6 in part. The Datasheet covers section 2. The System Card covers sections 3, 5, 8. The Impact Assessment covers section 7. The QMS documentation covers section 9. The Article 11 obligation is the *roll-up*.
   
   Note on numbering: when teaching materials refer to "Article 11 §1(a)–(h)," that's pedagogical shorthand for Annex IV sections. Article 11(1) itself is a single paragraph requiring documentation that contains the Annex IV elements. Be precise — sloppy citation in compliance work gets a program flagged.

10. **The gap log as a first-class artifact.** No transparency stack is ever complete on day one. The honest move is documenting the gaps: "Article 11 §5 cybersecurity testing — partial coverage in Model Card §Security Considerations; full coverage pending Q2 red-team exercise; owner: security team lead; target date: 2026-06-30." A gap log shows the program is mature enough to know what it doesn't yet have. Better than papering over.

11. **Audience-specific tailoring without contradiction.** A practical discipline: write the internal Model Card first. The customer Model Card is a subset of the internal one with framing adjusted; the regulator Model Card is a superset of the customer one with statutory anchors. Single source of truth, three audience-specific surface presentations.

12. **The Hugging Face Model Card convention.** For open-weights models, the de facto standard is the Hugging Face Model Card — generated via `huggingface_hub.ModelCard` and rendered as a `README.md` on the model repository. Implementation module uses this. The format is widely understood by ML practitioners and integrates with model-distribution workflows. For proprietary models, the format is more bespoke but the section structure is the same.

13. **Common failure modes.**
    - Shipping a Model Card and treating Article 11 as satisfied.
    - "No known issues" in the security considerations section.
    - Customer Model Card more detailed than the regulator version.
    - Internal Model Card with content that contradicts the external one.
    - No Datasheet for the training data — "we don't have one yet" becomes the answer to every bias question.
    - Sections written as marketing rather than technical truth.
    - No gap log — implying everything is covered when it isn't.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| CodeAssist-7B open-weights model card (mirrors demo) | A 7-billion-parameter open-source code-completion model. Walk through all four artifacts laid down side-by-side — Model Card (Hugging Face format), Datasheet for the training corpus, System Card for the inference-API deployment, Impact Assessment. Show audience tailoring on the same model. | Walkthrough — anchor example |
| FeedbackIQ sentiment-analysis Model Card (mirrors exercise) | B2B customer-feedback SaaS product embedding a sentiment-analysis model. Documentation lead must produce the Model Card the AI review board uses to approve a major EU customer launch. Walk through what the Model Card looks like with subgroup breakdowns by review language and industry segment, with security considerations ATLAS-tagged. | Walkthrough — second anchor |
| The "no known issues" security section | A Model Card with `Security Considerations: No known vulnerabilities.` Compare to one that names AML.T0051 prompt injection, AML.T0024 exfiltration via inference API, AML.T0015 evasion, with mitigations, residual risk, and red-team findings. The first looks confident. The second is trustworthy. Use to land the honesty discipline. | Brief mention with the comparison |
| The Article 11 crosswalk in practice | Take one Model Card section — say, the Quantitative Analyses section with subgroup performance metrics — and walk through which Annex IV section it satisfies (§4 training and evaluation data; §5 accuracy). For sections out of Model-Card scope, identify the sister artifact that carries them. | Walkthrough — third anchor |
| The gap log entry | A gap log row: "Annex IV §7 risk management measures — partial coverage in Model Card §Caveats; full coverage in AI Impact Assessment artifact; owner: AI Risk Officer; target date: end of Q3." Show what a real gap log row looks like. | Brief mention |
| The membership-inference attack as a Security Considerations row | Reference AML.T0024.000 Infer Training Data Membership — a sub-technique of `AML.T0024 Exfiltration via AI Inference API`. The Model Card row needs to cite the sub-ID precisely, not the parent. This is the kind of citation precision that downstream threat models can cross-walk against. | Brief mention |

---

## What NOT to Cover

- **The full text of every Annex IV section** — narrative only. The exercise's Article 11 Reference sheet carries detail.
- **EU AI Act risk-tier classification** — Module 4.
- **Fairness metric mechanics** — Module 10. Reference subgroup breakdowns in Model Card §Metrics only as the place where fairness numbers land.
- **MITRE ATLAS catalog overview** — Module 3. Reference ATLAS IDs only as the tagging convention in §Security Considerations.
- **The Hugging Face Hub publishing workflow** — implementation territory.
- **Datasheet template line-by-line** — the conceptual point is the four-artifact stack, not the Datasheet's full structure.
- **PIA / DPIA process detail** — Module 11.

---

## Additional Notes

- **Analogies.** The four-artifact stack is like an architect's drawing set — structural drawings, MEP drawings, site plan, code-compliance memo. Each serves a different inspector. Each is necessary. Together they describe the building. Try to ship just the structural drawings and the building inspector tells you to come back when you have the rest. Another: the Model Card alone for Article 11 is like submitting your résumé when the application asked for résumé, transcripts, references, and a writing sample. You answered one question.
- **Terminology.** Capitalize the artifact names — Model Card, Datasheet for Datasets, System Card, AI Impact Assessment. Use "transparency stack" for the collection. "Article 11" and "Annex IV" by name. "Security Considerations" is the canonical Model Card section heading; use it. ATLAS technique IDs in `AML.TXXXX` format on first mention, ID alone afterward.
- **A precise nuance worth landing.** When materials refer to "Article 11 §1(a)–(h)," that's pedagogical shorthand. Article 11(1) is a single paragraph requiring "technical documentation drawn up before the high-risk AI system is placed on the market or put into service in such a way that it contains, at a minimum, the elements set out in Annex IV." The topical sections are Annex IV §§1–9. Be precise; sloppy citation gets a program flagged.
- **Another nuance.** ATLAS technique names occasionally change (the catalog has been renaming "ML" to "AI" prefixes; `AML.T0040` now reads "AI Model Inference API Access" in current revisions). Technique IDs are stable; treat the ID as authoritative when the name on the live catalog differs from internal docs.
- **Avoid:** treating Model Card and System Card as interchangeable. Avoid suggesting "no known issues" is acceptable for a security section. Avoid implying the transparency stack is one-time work — it has to be maintained across model versions, training runs, and deployment changes.
- **A grounded line worth seeding:** "The Model Cards I trust most are the ones that say things like 'this model has not been validated for use on populations under 18' or 'we observed a 4-point accuracy drop on samples in dialects underrepresented in training data.' Honest limitations build trust. Confident silence breaks it."
- **A reflective beat:** "If your most senior security reviewer read your Model Card's Security Considerations section today, would they walk away with a clearer picture of residual risk — or a vague sense that the team isn't paying close attention?" Place this around the security-section discussion.
- **A throwaway humanity beat:** "The first Model Card I ever wrote, I left the Caveats section blank because I didn't want to scare the customer. Three months later we had a customer hit exactly the failure mode I'd been afraid to document. After that I started writing the Caveats section first." Use sparingly.
- **Connection to the implementation module.** Students will author a Model Card for FeedbackIQ in Excel (Model Card sheet with pre-filled Model Details / Intended Use / Factors, students populate Metrics with subgroup breakdowns by review language and industry segment, write the Security Considerations section ATLAS-tagged, write Caveats and Limitations), build the Article 11 Crosswalk mapping each Model Card section to a specific Article 11 / Annex IV requirement and naming the sister artifact for out-of-scope sections, and complete the Gap Log. After this module they should be able to predict the Model Card's section structure, why subgroup metrics are required, why ATLAS tagging matters in §Security Considerations, and how the four artifacts roll up to satisfy Article 11.

---
