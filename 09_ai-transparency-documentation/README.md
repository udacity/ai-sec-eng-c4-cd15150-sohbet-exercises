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

Each workbook contains six sheets: Scenario Brief, Model Card, Article 11 Crosswalk, Gap Log, Transparency Stack Reference, Article 11 Reference.

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
