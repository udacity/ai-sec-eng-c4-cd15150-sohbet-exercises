# Third-Party AI Model Risk Assessment

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This lesson covers third-party vendor governance for AI systems, including vendor risk scoring, SLA compliance monitoring, and vendor evaluation frameworks. Students learn to assess vendor risk across multiple dimensions (security, data handling, transparency, financial stability, SLA quality), generate recommendations, and build compliance dashboards.

## File Structure

```
08_third-party-ai-model-risk-assessment/
├── demo/
│   ├── vendor_governance_demo.xlsx      # Filled-in instructor reference
│   ├── vendor_risk_scoring_demo.ipynb            # Notebook walkthrough for vendor risk scoring
│   └── vendor_comparison_demo.png                # Generated visualization (demo output)
├── exercises/
│   ├── starter/
│   │   ├── vendor_governance_starter.xlsx        # Student starting file (with hints)
│   │   └── vendor_risk_scoring_starter.ipynb     # Notebook with TODO placeholders
│   └── solution/
│       ├── vendor_governance_solution.xlsx        # Completed solution
│       ├── vendor_risk_scoring_solution.ipynb     # Completed notebook
│       ├── vendor_risk_comparison.png             # Generated visualization (solution output)
│       ├── vendor_radar.png                       # Generated visualization (solution output)
│       └── sla_compliance_dashboard.png           # Generated visualization (solution output)
└── README.md
```

## Demo

**Scenario: CloudFirst Financial** — A financial services company evaluating 2 AI vendors (CloudVault AI and TitanScale AI) for their fraud detection system after a competitor suffered a 6-hour vendor outage.

The instructor walks through vendor governance concepts live, filling in vendor assessment criteria and risk scores. The notebook demonstrates the full workflow for 2 vendors (CloudVault AI and TitanScale AI): defining evaluation scores across 5 criteria, calculating weighted risk scores (1–5 scale) using predefined weights, generating 30 days of simulated SLA data, analyzing uptime and latency compliance, producing a side-by-side comparison chart, and generating governance recommendations.

## Exercise

**Scenario: InsureLogic AI** — An insurance technology company managing 5 AI vendor relationships (NovaMind API, CloudVault AI, TitanScale AI, DeepLens AI, SafeGuard AI) for claims processing, fraud detection, and customer service. A vendor model update recently caused false claim denials, triggering a formal risk assessment.

### Task

**Part 1 — Vendor Governance (Excel)**

1. **Vendor Assessment** — Evaluate each vendor across security posture, data handling practices, model transparency, financial stability, and SLA compliance. Document certifications, evidence, and risk ratings.
2. **SLA Requirements** — Track vendor SLA performance including uptime, latency, and incident response metrics against contractual thresholds.
3. **Contingency Plan** — Develop response plans for the 8 vendor-risk scenarios (probability, impact, mitigation strategy, backup vendor, migration timeline, data portability, communication plan).

**Part 2 — Vendor Risk Scoring (Notebook)**

Vendor evaluation scores (0–100 per criterion) and 30 days of simulated SLA data are provided inline for all 5 vendors.

1. **Define Scoring Weights** — Assign weights across 7 risk dimensions (Security, Data Handling, Transparency, Financial Stability, SLA Compliance, Exit Strategy, **AI_Model_Governance** — GenAI-specific 7th covering training-data provenance, model-update notification, fine-tuning portability, and liability terms) that sum to 1.0, reflecting insurance-industry priorities.
2. **Calculate Risk Scores** — Implement a function that computes a weighted average of vendor scores (0–100 per criterion) and converts the result to a 1–5 risk scale where 1 = lowest risk and 5 = highest risk. The conversion logic is yours to design — document it in the function docstring.
3. **Vendor Recommendation Logic** — Implement a function that classifies vendors as Highly Recommended (risk ≤ 1.5 + SLA compliant), Recommended (≤ 2.5 + SLA compliant), Acceptable with Monitoring (≤ 3.5), or Not Recommended (> 3.5).
4. **Visualizations** (pre-provided, run and review) — Risk comparison bar chart, 30-day SLA compliance dashboard (uptime + latency tracking), and radar chart comparing top 3 vendors across the six operational dimensions (AI Model Governance feeds the weighted risk score and ranked summary rather than the radar).
5. **Scenario Analysis — Model-Update Incident** — Building on the InsureLogic incident in the scenario, write a brief printed assessment of which vendor(s) carry the highest model-update-notification risk and how you'd justify that ranking against your scoring.
6. **Final Assessment Report** — Review the ranked vendor summary with risk scores, SLA compliance status, and governance recommendations.
7. **Exit-Strategy Analysis** — Bucket each vendor by switching-cost (Low / Moderate / High) using the `Exit_Strategy` dimension. Pick your own thresholds and print which vendors fall in each bucket.
8. **Sensitivity Analysis** (stretch) — Pick one vendor, perturb their per-criterion scores by ±10 points, re-run the risk scoring, and report whether the recommendation tier flips.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the standards and tooling cited in this lesson.

- **PCI DSS notification vs GDPR Article 33 notification.** PCI DSS requires notification of *acquirers / card brands* without undue delay; the timeline is set by the card-brand contracts rather than by PCI DSS itself. The familiar 72-hour deadline is the [GDPR Article 33](https://gdpr-info.eu/art-33-gdpr/) requirement for personal-data breach notification to the supervisory authority. The two regimes can apply in parallel during a payment-data breach; the deadlines are separate.
- **AWS Bedrock Guardrails capabilities.** [Bedrock Guardrails](https://aws.amazon.com/bedrock/guardrails/) provides content-safety filtering (denied topics, contextual grounding to detect hallucinations, PII redaction, and harmful-output filters). Demographic-bias detection in the fairness-metric sense (demographic parity, equalized odds, etc.) is a separate workload typically handled by tools like Fairlearn or AIF360 rather than by Guardrails directly.
- DeepLens is the deliberately weak vendor in this scenario: no published security certification and low model transparency — its notebook scores (15 and 40 on those criteria) reflect that posture.
