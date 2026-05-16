# Explainable AI (XAI) for Security Auditing

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students to use SHAP for security auditing of machine-learning classifiers. Students learn the difference between local (per-instance) and global feature importance, how SHAP exposes proxy-variable leakage that a fairness-metric scan would miss, and how to write an audit memo for non-technical reviewers (Trust & Safety, Legal, an appeals reviewer) that pairs raw SHAP plots with explicit caveats on what XAI can and cannot show.

## File Structure

```
01_explainable-ai-xai-for-security-auditing/
├── demo/
│   ├── shap_demo.ipynb                         # End-to-end demo notebook (content-moderation classifier)
│   └── data/
│       ├── moderation_classifier.joblib        # Pre-trained logistic-regression model
│       ├── moderation_train.csv                # Training set
│       └── moderation_test.csv                 # Test set with the wrongly-flagged example
├── exercises/
│   ├── starter/
│   │   ├── xai_audit_starter.ipynb             # TODO scaffolding (SHAP audit + memo)
│   │   └── data/
│   │       ├── loan_classifier.joblib          # Pre-trained gradient-boosting model
│   │       ├── loan_train.csv                  # Training set
│   │       ├── loan_test.csv                   # Test set with two flagged declined applicants
│   │       └── flagged_cases.csv               # The two cases the audit memo addresses
│   └── solution/
│       ├── xai_audit_solution.ipynb            # Fully implemented + executed reference
│       ├── shap_explanations_case1.png         # Per-case SHAP waterfall plot
│       ├── shap_explanations_case2.png         # Per-case SHAP waterfall plot
│       └── shap_global_importance.png          # Global feature importance for context
└── README.md
```

## Demo

**Scenario: SocialHub** — A social-media platform's content-moderation model has flagged a benign user post as toxic and removed it. The user has appealed; the audit team must determine why the model flagged it before the appeal is decided.

The instructor uses SHAP to produce a per-instance explanation for the flagged post and contrasts it with the model's global feature importance. The walkthrough surfaces that the model is reacting to dialect-marker tokens (a proxy for the user's regional / ethnic background) rather than the actual content of the post — both an audit finding and a fairness flag. The notebook then drafts a one-paragraph audit note with explicit caveats on what SHAP can and cannot show (correlation, not causation; per-instance only; subject to class-imbalance artifacts).

## Exercise

**Scenario: UdaciBank Loan-Approval Audit** — A regional bank's loan-approval model is generating consumer complaints from declined applicants. As AI Risk Officer, you must produce an audit memo on two flagged cases that the model-risk and legal teams will rely on when responding to the complainants.

### Task

**Part 1 — SHAP Audit (Notebook)**

1. **Load the data and the pre-trained model** — `data/loan_classifier.joblib`, `loan_test.csv`, `flagged_cases.csv` (two declined applicants).
2. **Generate SHAP explanations for both flagged cases** — TreeExplainer; per-instance waterfall plots; save as `shap_explanations_case1.png` and `shap_explanations_case2.png`.
3. **Compare local feature importance against the model's global feature importance** — render the global-importance bar chart as `shap_global_importance.png`.
4. **Identify proxy attributes** — a `detect_proxy_features()` helper flags features whose local SHAP impact is materially larger than the model's global average impact in the same direction across the two cases. Common candidates: ZIP-derived income proxy, employer name proxy, education proxy.
5. **Run a feature-removal counterfactual** — re-score the two flagged cases with the most-suspect proxy ablated to its training-set median, and quantify the change in approval probability + SHAP attribution. (This is the exercise-specific analytical step the demo doesn't cover.)

**Part 2 — Audit Memo (Notebook markdown cell)**

1. **Model behavior summary** — what the model did on both cases.
2. **Explanation evidence** — top-5 features driving each declination, mapped to the SHAP plots.
3. **Counterfactual finding** — which proxy you ablated, what happened to P(approve), did the decision flip.
4. **Caveats on the limits of SHAP** — correlation not causation; per-instance only; sensitivity to background distribution; class-imbalance artifacts. Include an explicit caveat sentence in the memo body.
5. **Recommended next steps** — pick from the defined menu (overturn / re-review / escalate to fairness audit / decline-stand) for each case + a model-level recommendation.

### Color Guide

This module is notebook-first (no workbook). The standard C4 color palette doesn't apply to notebook cells the way it does to xlsx sheets — but for any callout in markdown, follow the same convention:

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data / background context | Context — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |

For this module specifically, the audit-memo template in the starter notebook uses `[Your response here]` placeholders to mark fill-in cells.


## Reference Notes

A few specification details for learners cross-referencing the libraries and legal anchors used in this lesson.

- **Detoxify model variants.** The `detoxify` package ships three checkpoints with different base models: `original` is BERT-based (`bert-base-uncased`); `unbiased` is RoBERTa-based; `multilingual` is XLM-R-based. Where the lesson references "RoBERTa / XLM-R variants," that's specifically the `unbiased` and `multilingual` checkpoints.
- **ECOA / Regulation B context (2026).** ECOA + Reg B remain the operative federal fair-lending framework. The CFPB's April 2026 final rule on Regulation B narrowed federal disparate-impact liability, while disparate-treatment analysis (including via proxies such as ZIP-derived income or education) remains actionable. State fair-lending laws and the Fair Housing Act also continue to recognize disparate-impact theories. See [CFPB ECOA / Regulation B](https://www.consumerfinance.gov/compliance/compliance-resources/other-applicable-requirements/equal-credit-opportunity-act/) for the current schedule.
