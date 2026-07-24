# AI Transparency Documentation

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students to author the Model Card layer of an AI transparency stack and cross-walk every section of the card to a specific EU AI Act Article 11 technical-documentation requirement. Students learn that no single artifact in the four-document stack (Model Card, Datasheet, System Card, impact assessment) replaces the others — Article 11 is satisfied by the stack collectively — and produce a Model Card whose security-considerations section is honest about residual risk and explicit about which sister artifact covers each gap.

## File Structure

```
09_ai-transparency-documentation/
├── demo/
│   └── model_card_demo.xlsx                    # Filled-in instructor reference (CodeAssist-7B walkthrough)
├── exercises/
│   ├── starter/
│   │   └── model_card.xlsx                     # Student starting file (FeedbackIQ sentiment Model Card)
│   └── solution/
│       └── model_card.xlsx                     # Completed solution with Reasoning: annotations
└── README.md
```

Each workbook contains several sheets: Scenario Brief, Model Card, Article 11 Crosswalk, Gap Log, Transparency Stack Reference, Article 11 Reference, and Reference Notes.

## Demo

**Scenario: UdaciLab — CodeAssist-7B** — An AI lab releasing CodeAssist-7B, a 7-billion-parameter open-source code-completion model. The release manager needs the full AI transparency stack laid down side-by-side.

The instructor walks the four transparency artifacts (Model Card, Datasheet for Datasets, System Card, AI impact / risk assessment), shows how each one is tailored to a different audience (internal engineering vs developer-customer vs EU AI Act regulator), and demonstrates audience-tailoring on the same underlying model. Model Cards are authored with **Hugging Face Model Cards** (`huggingface_hub.ModelCard`, the open-weights default). The walkthrough then maps each Model Card section to a specific Article 11 requirement and flags where the Datasheet / System Card / impact assessment carry the rest of the load. The Gap Log sheet shows how an honest Model Card calls out residual risks rather than burying them.

## Exercise

**Scenario: FeedbackIQ** — A B2B customer-feedback SaaS product that embeds a sentiment-analysis ML model classifying inbound customer reviews. As FeedbackIQ's documentation lead, produce the Model Card the AI review board will use to approve a major customer launch into the EU market. The card must satisfy its slice of Article 11, stand up to a security-team review, and cleanly cross-reference the Datasheet, System Card, and impact assessment that other team members are producing in parallel.

### Task

**Part 1 — Model Card**

1. **Read the pre-filled sections** — Model Details, Intended Use, and Factors are pre-filled as worked examples.
2. **Populate Metrics with subgroup breakdowns** — by review language and industry segment.
3. **Write the Security Considerations section** — known attack vectors (adversarial text, prompt-injection-like payloads), mitigations, residual risks, red-team findings. **Tag each attack vector with its ATLAS ID** (e.g., `AML.T0015 Evade ML Model`, `AML.T0051 LLM Prompt Injection`) so any downstream threat model can cross-walk against it cleanly.
4. **Write Caveats and Limitations** — what the model is NOT validated for; out-of-distribution behavior; known failure modes.

**Part 2 — Article 11 Crosswalk**

1. **Map every Model Card section to a specific Article 11 requirement** — for each section, name the article / paragraph it satisfies. Two mappings are pre-filled.
2. **For sections out of Model-Card scope** — name the sister artifact that covers it (Datasheet for training data, System Card for runtime monitoring, impact assessment for population-level harms).

**Part 3 — Gap Log**

1. **List residual gaps** — for each Article 11 requirement not fully covered by your Model Card, note the gap, the artifact picking it up, the owner, and the target date.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the EU AI Act and MITRE ATLAS citations used in this lesson.

- **Article 11 paragraph numbering — pedagogical shorthand vs statutory structure.** For brevity, this lesson refers to *Article 11 §1(a)–(h)* on the Article 11 Crosswalk and Article 11 Reference sheets. In the published Regulation (EU) 2024/1689, Article 11(1) is a single paragraph that requires technical documentation drawn up before placing on market and *"containing, at a minimum, the elements set out in Annex IV."* The topical content (general description, training methodologies, monitoring approach, accuracy, cybersecurity, etc.) is structured in **Annex IV sections 1–9**. The §1(x) labels used here are a pedagogical shorthand for the corresponding Annex IV sections — designed to give the Model Card crosswalk a row-by-row anchor the AI review board can follow. When sharing this work outside the lesson, use the Annex IV section numbers as the canonical statutory anchor. See [Article 11](https://artificialintelligenceact.eu/article/11/) and [Annex IV](https://artificialintelligenceact.eu/annex/4/).
- **AML.T0024 sub-techniques.** In MITRE ATLAS, the parent technique `AML.T0024` is *"Exfiltration via AI Inference API."* The two sub-techniques are:
  - `AML.T0024.000` *"Infer Training Data Membership"* (membership-inference attacks)
  - `AML.T0024.001` *"Invert AI Model"* (reconstruct training data from model outputs)
  The Model Card Security Considerations row references `AML.T0024.000` for the training-data inference scenario; the demo workbook has been updated to use the precise sub-ID.
- **ATLAS naming evolution.** ATLAS has been renaming the prefix from "ML" to "AI" in some technique names (e.g., `AML.T0040` is now "AI Model Inference API Access" in current revisions). Technique IDs are the stable canonical reference; treat the ID as authoritative when the name on the live catalog differs from the workbook label.

For the live, authoritative catalog, see [MITRE ATLAS](https://atlas.mitre.org/) and the per-technique pages.
- Article 13's transparency duties attach to high-risk systems; for a Limited-risk system like FeedbackIQ, documentation expectations flow from the customer's procurement contract.
- Article 50 splits its duties: 50(1)–(2) bind the *provider* (direct-interaction and synthetic-content disclosure); 50(3)–(4) bind the *deployer* (emotion-recognition / biometric-categorisation notices, deepfake labels).
