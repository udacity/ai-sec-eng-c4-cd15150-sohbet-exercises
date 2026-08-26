# AI Governance for Bias and Fairness Auditing

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students to run a focused fairness audit by computing the three core metrics (demographic-parity ratio, equalized odds, equal opportunity) **from confusion-matrix primitives first** (~15 lines), with **Fairlearn used as a one-line cross-check**. Students then test one intervention (per-group threshold adjustment), quantify the trade-off between fairness and accuracy, and produce a defensible launch / conditional-launch / no-go memo for the AI review board. An **optional Section 7** runs the same primitives against a small synthetic LLM-hiring-screen fixture to show the metric pattern transfers to a 2026-current GenAI surface without losing the policy interpretation anchor, though the anchor shifts with the domain (ECOA / Reg B for the credit decision; Title VII / EEOC and NYC LL-144 for the hiring screen; EU AI Act Annex III for both). Students learn that fairness metrics are inputs to a governance decision, not the decision itself, and that the AI Risk Officer owns the interpretation layer.

## File Structure

```
10_ai-governance-for-bias-and-fairness-auditing/
├── demo/
│   ├── fairness_demo.ipynb                     # End-to-end demo notebook (auto-insurance pricing model)
│   └── data/
│       ├── insurance_predictions.csv           # Synthetic predictions, labels, age band, region
│       └── README.md                           # Fixture description
├── exercises/
│   ├── starter/
│   │   ├── fairness_audit_starter.ipynb        # TODO scaffolding (3 metrics + 1 intervention + memo)
│   │   └── data/
│   │       ├── loan_predictions.csv            # UdaciBank synthetic predictions + labels + subgroups
│   │       └── llm_hiring_screen.csv           # Section 7 GenAI bonus fixture (200 candidates)
│   └── solution/
│       ├── fairness_audit_solution.ipynb       # Fully implemented + executed reference (incl. Section 7)
│       ├── fairness_metrics_chart.png          # Generated metric-comparison chart
│       └── data/
│           └── llm_hiring_screen.csv           # Section 7 GenAI bonus fixture (200 candidates)
└── README.md
```

## Demo

**Scenario: SafeWheels Insurance — Auto-pricing model** — An auto-insurance pricing model returns a demographic-parity ratio of 0.73 across protected age groups (age band and ZIP-derived geographic cluster). Is 0.73 launchable?

The instructor walks the canonical fairness-audit pipeline live: load predictions + labels + subgroup column; compute DP ratio, equalized odds, and equal opportunity **from confusion-matrix primitives** (~15 lines); cross-check against Fairlearn in one line; compare each metric against the policy thresholds; run a counterfactual showing how per-group threshold adjustment shifts each metric; identify the launch decision (go / conditional / no-go) and the named owner; close with a one-paragraph board-facing summary.

The walkthrough surfaces the impossibility trilemma (you cannot satisfy all three metrics simultaneously) and shows that the interpretation layer — what does "0.73" mean for THIS product? — is the GRC practitioner's job.

## Exercise

**Scenario: UdaciBank — Loan-approval model** — UdaciBank is launching a new loan-approval model. As AI Risk Officer, run the focused fairness audit using the three core metrics, test one intervention (per-group threshold adjustment), quantify the trade-off, and produce the launch recommendation memo for the AI review board.

Subgroups in scope: gender (male / female), race (4 categories), age band (under 25 / 25–44 / 45–64 / 65+).

### Task

**Part 1 — Fairness Audit (Notebook)**

1. **Load the data** — `data/loan_predictions.csv` carries predictions, labels, and the subgroup columns.
2. **Compute the three core metrics from confusion-matrix primitives first** — DP ratio, equalized-odds difference, equal-opportunity difference across each subgroup column (~15 lines), then verify with Fairlearn as a one-line cross-check.
3. **Compare against the policy thresholds** — DP ratio ≥ 0.80, equalized-odds difference ≤ 0.10, equal-opportunity difference ≤ 0.10.
4. **Test one intervention: per-group threshold adjustment** — find a per-group threshold set that brings the worst metric inside the policy bound; report new metrics and the cost in accuracy.
5. **Quantify the trade-off** — change in accuracy vs change in each of the three fairness metrics.
6. **Render the metrics-comparison chart** — before / after on the three metrics, plus accuracy. Save as `fairness_metrics_chart.png`.

**Part 2 — Launch Recommendation Memo (Notebook markdown cell)**

1. **Recommendation** — Pick **Launch** / **Conditional Launch** / **No-Go**. Tie to the audit results.
2. **Recommended controls** — Name 2–3 controls (per-group thresholds, monitoring, retraining cadence).
3. **90-day monitoring plan** — Which metrics, which cadence, which owner, which escalation path.

**Part 3 — Optional bonus**

1. Add predictive parity as a fourth metric.
2. Test a second intervention (post-processing per-group threshold optimization via Fairlearn's `ThresholdOptimizer` — reassigns the decision threshold per protected group rather than reweighting the training data).
3. **Section 7 — GenAI surface.** Run the same primitives against the synthetic LLM-hiring-screen fixture (`data/llm_hiring_screen.csv` — 200 candidates, gender label, LLM advance/screen-out, human qualification label). Show the metric pattern transfers to a 2026-current GenAI use case **without losing the policy anchor** — noting that the US anchor shifts from ECOA / Reg B (credit) to Title VII / EEOC and NYC LL-144 (employment), with EU AI Act Annex III covering both.

### Color Guide

This module is notebook-first (no workbook). The standard C4 color palette doesn't apply to notebook cells the way it does to xlsx sheets — but for any callout in markdown, follow the same convention:

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data / background context | Context — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |

In the starter notebook, markdown cells starting with `📌 TODO` are your work areas; cells starting with `🔒 Reference` are read-only context.

### Further Reading

- **AIF360** (IBM) — alternative fairness-metric library; useful for cross-method validation against this notebook's primitives.
- **Aequitas** (CMU) — fairness audit toolkit oriented to public-policy deployments; complements AIF360.
- **BBQ** (Bias Benchmark for QA) — LLM-specific fairness benchmark for stereotype-anchored question answering.
- **BiasInBios** — fairness benchmark on occupation classification from biographies (used in Section 7's framing).
- **HELM** (Stanford CRFM) — holistic evaluation suite covering accuracy, fairness, robustness, and other axes.


## Reference Notes

A few specification details for learners cross-referencing the fairness-policy thresholds and library APIs used in this lesson.

- **0.10 ceiling for equalized-odds and equal-opportunity differences.** The 0.10 threshold used throughout the SafeWheels and UdaciBank scenarios is a **firm-policy threshold** chosen for this lesson — it is not a regulatory or industry-wide standard. Real organizations set EO / EOpp ceilings based on their policy, regulatory exposure, and the distribution of their training data; common firm policies range from 0.05 to 0.15 depending on the use case and risk tier. By contrast, the **0.80 demographic-parity floor** is anchored to the [EEOC 4/5ths rule](https://www.eeoc.gov/laws/guidance/questions-and-answers-clarify-and-provide-common-interpretation-uniform-guidelines) and has external regulatory provenance.
- **Fairlearn `ThresholdOptimizer` family.** [`ThresholdOptimizer`](https://fairlearn.org/main/api_reference/generated/fairlearn.postprocessing.ThresholdOptimizer.html) is a *post-processing* mitigation that selects a separate decision threshold per protected group to satisfy a fairness constraint (e.g., equalized odds). It does not modify the training data — that's the role of pre-processing techniques like AIF360's [`Reweighing`](https://aif360.readthedocs.io/en/stable/modules/generated/aif360.algorithms.preprocessing.Reweighing.html). Both families are valid mitigations; they intervene at different points in the pipeline.
- **The fairness-impossibility result.** The well-known impossibility result (Chouldechova 2017; Kleinberg-Mullainathan-Raghavan 2016) is formally between **calibration** and **error-rate balance under unequal base rates**. The lesson's framing of an "impossibility trilemma" across DP, EO, and EOpp is a related practical observation — these metrics generally cannot all hold simultaneously except in degenerate cases — but the formal proof targets the calibration-vs-equalized-odds pair specifically.
- **ECOA / Regulation B (2026).** ECOA + Reg B remain the operative federal fair-lending anchor. The CFPB's April 2026 final rule on Regulation B narrowed federal disparate-impact liability, while disparate-treatment analysis (including via proxies) remains actionable. State fair-lending laws and the Fair Housing Act also continue to recognize disparate-impact theories.
