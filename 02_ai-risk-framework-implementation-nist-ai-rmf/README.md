# AI Risk Framework Implementation (NIST AI RMF)

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This lesson covers AI risk assessment frameworks using the NIST AI Risk Management Framework (AI RMF). Students learn to identify, categorize, and score risks across the four NIST functions (Govern, Map, Measure, Manage), build risk registers, and visualize risk profiles using Python. The exercise includes producing an executive summary of risk findings.

## File Structure

```
02_ai-risk-framework-implementation-nist-ai-rmf/
├── demo/
│   ├── risk_assessment_demo.xlsx # Filled-in instructor reference
│   └── risk_scoring_demo.ipynb            # Notebook walkthrough for risk visualization
├── exercises/
│   ├── starter/
│   │   ├── risk_assessment.xlsx           # Student starting file (with hints)
│   │   └── risk_scoring.ipynb             # Notebook with TODO placeholders
│   └── solution/
│       ├── risk_assessment.xlsx           # Completed solution
│       └── risk_scoring.ipynb             # Completed notebook
└── README.md
```

## Demo

**Scenario: CareBot Health** — A hospital network operating DiagnosAI, a clinical decision-support system that recently had a near-miss drug interaction incident.

The instructor populates a risk register live with 7 risks across all four NIST AI RMF functions (Govern, Map, Measure, Manage), scoring them by likelihood and impact, and calculating overall risk levels. The notebook demonstrates how to visualize risk scores with a heat map (color-coded by risk category) and generate summary statistics.

## Exercise

**Scenario: FinGuard AI** — A fintech company (400 employees) whose FraudShield fraud detection system has been flagged for socioeconomic bias, disproportionately flagging transactions from lower-income zip codes.

### Task

**Part 1 — Risk Register (Excel)**

1. **Risk Identification** — Complete the 18-row risk register. The starter xlsx ships with 15 base risks pre-filled across all four NIST AI RMF functions (Govern, Map, Measure, Manage); rows R016–R018 are GenAI-specific student-fill placeholders covering hallucinated explanations, prompt-injection vulnerabilities, and training-data poisoning.
2. **Risk Scoring** — For each risk, assign likelihood (1–5) and impact (1–5) scores using the provided Scoring Rubric sheet, then calculate the risk level (Critical / High / Medium / Low).
3. **Mitigation Planning** — Specify a mitigation strategy and a target date for each risk; risk owners come pre-assigned in the register (review and adjust if your analysis suggests a better owner).

**Part 2 — Risk Visualization (Notebook)**

1. Load the 15 base risks into a pandas DataFrame and calculate risk scores (Impact × Likelihood). The 3 GenAI-specific risks (R016–R018) are completed in the xlsx register but are not wired into the notebook visualization pipeline so the visualization stays focused on the core register.
2. Assign risk levels using thresholds: Critical (≥15), High (10–14), Medium (5–9), Low (<5).
3. Generate a ranked risk register sorted by score.
4. Create a risk heat map (Impact vs. Likelihood scatter plot, color-coded by risk category).
5. Build a grouped bar chart showing average and maximum risk score by category (Technical, Ethical, Legal, Operational).
6. Create a pie chart showing risk level distribution (Critical / High / Medium / Low).
7. Produce a formatted executive summary report with risk level breakdown, top 5 priority risks, and key findings.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few framing details worth flagging for learners who want to map this lesson to the underlying standards.

- **Risk-scoring scheme.** The `Risk Score = Impact × Likelihood` formula and the four bands (Critical ≥ 15, High 10–14, Medium 5–9, Low < 5) are one common operationalization used here for clarity. NIST AI 100-1 defines risk as a function of the magnitude of harm and the likelihood of occurrence (see [NIST AI 100-1, Section 1](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)) but is intentionally agnostic about the calculation method, so organizations adopt the scheme that fits their existing ERM stack — multiplicative is one widely used choice; additive and weighted-rubric variants are equally valid.
- **EU AI Act routing for clinical decision support.** Where a system also qualifies as a regulated medical device under EU MDR / IVDR, the High-Risk classification routes through **Annex I** (regulated product safety) in addition to (or rather than) Annex III. The compliance obligations are the same; the statutory anchor differs. See [Annex I](https://artificialintelligenceact.eu/annex/1/) for the product-regulation list.
- **EU AI Act routing for fraud detection.** Annex III §5(b) targets **creditworthiness scoring** of natural persons. Pure transaction-level fraud detection becomes High-Risk by extension when its output materially shapes downstream credit, onboarding, or eligibility decisions; standalone fraud-only models sit outside §5(b). See [Annex III](https://artificialintelligenceact.eu/annex/3/).
- **HIPAA penalty figures.** The "$50K – $1.5M per violation" figures used as a reference are the canonical historical numbers; HHS adjusts them annually for inflation (the 2026 per-violation maximum is approximately **$73K** (effective Jan 28, 2026, per Federal Register inflation adjustment)). Current schedule: [HHS HIPAA Compliance and Enforcement](https://www.hhs.gov/hipaa/for-professionals/compliance-enforcement/index.html).
- Risk scoring is judgment, not arithmetic — on borderline calls two assessments can land a notch apart. Here the workbook register reads R011 and R014 at impact 2 (score 4, Low) while the notebook's scoring pass reads them at 3 (score 6, Medium); that is why one tally shows 3 Medium / 2 Low and the other 5 / 0. The demo shows the same drift on R007 (Impact 3 × Likelihood 4 = 12, High, in the workbook vs 15, Critical, in the notebook; its mitigation — mandatory staff training — lives on the workbook's register row). In practice you would reconcile this in a calibration review.
- Category and NIST-function counts are fixed by the register regardless of scoring: 3 Legal and 3 Operational risks; Govern 4, Map 3, Measure 4, Manage 4.
- EU AI Act anchor: Annex III 5(b) exempts fraud detection from the High-Risk class — FraudShield is governed as High-Risk internally because its outputs can feed credit-limit and eligibility decisions.
