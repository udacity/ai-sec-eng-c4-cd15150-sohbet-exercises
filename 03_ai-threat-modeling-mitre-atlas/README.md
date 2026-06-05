# AI Threat Modeling (MITRE ATLAS)

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students how to translate the MITRE ATLAS catalog of adversary tactics, techniques, and procedures (TTPs) into a small set of architecture-specific threat-model entries an AI review board can act on. Students learn the difference between a generic TTP catalog and a scoped threat model, produce a ranked threat-model report, and write a board-facing brief with a launch recommendation. The module anchors to MITRE ATLAS, with STRIDE-ML and LINDDUN as design-time complements.

## File Structure

```
03_ai-threat-modeling-mitre-atlas/
├── demo/
│   └── threat_model_demo.xlsx                  # Filled-in instructor reference (ChatPoint, AML.T0051 walkthrough)
├── exercises/
│   ├── starter/
│   │   └── threat_model_starter.xlsx           # Student starting file (FinTrust, 5 TTP IDs pre-scoped, 2 fully worked)
│   └── solution/
│       └── threat_model.xlsx                   # Completed solution (FinTrust, all 5 TTPs + Board Brief, with Reasoning: annotations)
└── README.md
```

Each workbook contains several sheets: Scenario Brief, Threat Model, Board Brief, Scoring Rubric, ATLAS TTP Reference, Control Family Reference, and ATLAS Reference Notes.

## Demo

**Scenario: ChatPoint** — A B2C customer-support chatbot built on a foundation-model API, deployed on the public internet through a web widget. The product team wants the AI review board to sign off on a new LLM-powered self-serve refund flow before launch.

The instructor walks one MITRE ATLAS technique — **AML.T0051 LLM Prompt Injection** — through ChatPoint's specific architecture: scoping the technique against the public-facing chat surface, scoring it (high likelihood given the public surface, medium-to-high impact given the new refund tool), mapping it to a named control family (input filtering + tool-use guardrails + behavioral monitoring), and translating the result into a single risk-register row a security review can act on. The Threat Model sheet shows AML.T0051 alongside two adjacent TTPs (AML.T0040 ML Model Inference API Access; AML.T0048 External Harms — Financial Loss) so students see how the row format applies across multiple techniques. The Board Brief sheet then ties those rows into a Conditional-Launch recommendation. The supporting reference sheets (Scoring Rubric, ATLAS TTP Reference, Control Family Reference) are the same three sheets students will reuse in the exercise.

## Exercise

**Scenario: FinTrust** — A fintech operating a face-matching identity-verification ML pipeline over a public mobile-app endpoint as part of its customer onboarding (KYC) flow. The model decides whether to admit a new customer to the platform. As security architect, you lead a threat-modeling session and produce both a ranked TTP report and a board brief for the AI review board ahead of launch.

### Task

**Part 1 — Threat Model sheet**

1. **Review the Architecture Description** — Read the FinTrust system overview on the Scenario Brief sheet (model, API surface, image-upload pipeline, KYC decision downstream).
2. **Read the Pre-Filled TTPs** — Two TTPs are already scoped end-to-end on the Threat Model sheet (AML.T0006 Active Scanning and AML.T0040 ML Model Inference API Access). Read them as worked examples.
3. **Scope 3 Additional TTPs** — The starter pre-fills three additional TTP IDs in rows 4–6 (AML.T0015 Evade ML Model — Deepfake / Generative-Liveness Bypass, AML.T0024 Exfiltration via ML Inference API, AML.T0020 Poison Training Data) so everyone works from the same scope. Cross-reference each ID against the ATLAS TTP Reference sheet to understand the technique, then write the Architecture Scoping rationale (one sentence: how the TTP shows up against FinTrust's specific architecture).
4. **Score Likelihood and Impact (1–5)** — For each new TTP, score likelihood and impact using the Scoring Rubric. Risk Score and Risk Level auto-calculate from your inputs.
5. **Map to a Control Family** — For each new TTP, name the primary Control Family from the Control Family Reference and list 1–2 Named Controls that would catch or mitigate it.
6. **Assign Owner and Status** — Set the responsible owner role and an initial Status (Open / Mitigated / Accepted).

**Part 2 — Board Brief sheet**

1. **Top 3 TTPs** — Sort the 5 TTPs from the Threat Model sheet by Risk Score (descending), tie-break by Impact, and fill the Top 3 table on the Board Brief sheet.
2. **Recommended Controls** — For each top TTP, write 1–2 sentences naming the recommended controls and the residual risk after they are in place.
3. **Board Recommendation** — Pick **Launch**, **Conditional Launch**, or **No-Go**. Write a one-paragraph rationale that ties back to the top TTPs and the residual-risk view.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## ATLAS Reference Notes

A few specification details worth keeping in view as you work with the ATLAS catalog. ATLAS is actively maintained — IDs are stable; technique names occasionally update.

- **`AML.T0048` parent vs. sub-techniques.** ATLAS structures *External Harms* (`AML.T0048`) into sub-techniques. The financial-loss case the demo walks through is captured precisely by **`AML.T0048.000` "Financial Harm"** (note `AML.T0048.001` is *Reputational Harm*); ATLAS uses the term *Financial Harm* in the catalog. See [MITRE ATLAS — AML.T0048](https://atlas.mitre.org/techniques/AML.T0048/).
- **`AML.T0018` parent tactics.** ATLAS lists *Backdoor ML Model* under both **Persistence** and **ML Attack Staging** tactics, depending on whether the backdoor is staged before deployment or seeded post-deployment.
- **`AML.T0000` official catalog name** is "Search **for** Victim's Publicly Available Research Materials."
- **Naming evolution.** ATLAS has been renaming the prefix from "ML" to "AI" in some technique names (e.g., `AML.T0040` is "AI Model Inference API Access" in current revisions). Technique IDs are the stable canonical reference; treat the ID as authoritative when the name on the live catalog differs from the workbook label.

For the live, authoritative catalog, see [MITRE ATLAS](https://atlas.mitre.org/).
