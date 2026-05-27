# Video: Understanding Explainable AI (XAI) for Security Auditing
*Module 1.1 | Topic: Understanding Explainable AI (XAI) for Security Auditing*

---

## Opening Hook

> *"A bank declines a loan. The applicant calls customer service. The rep pulls up the case, reads 'declined by model,' and that's it — there's no human in the chain who can answer why. Now imagine that conversation happens four hundred times a day. That's not a UX problem. That's a regulator showing up with a subpoena. And then a different thought: two analysts look at the same SHAP waterfall plot and reach opposite conclusions. One says the model is discriminating by ZIP code. The other says ZIP is a legitimate signal correlated with default risk. They're both reading the chart correctly. The disagreement is upstream of SHAP — it's about what 'discrimination' means. And that's the part XAI cannot resolve for you."*

The hook I want to land is two-edged: black boxes are a legal, fairness, and incident-response problem (not just an engineering taste preference), AND the tools we use to crack them open are powerful but easy to misread. The conceptual module exists in the space between those two truths.

---

## Key Discussion Points

The points I'd lose sleep over if a generic AI write-up missed them:

1. **The black box isn't a property of the model alone — it's a property of the *system around it*.** A logistic regression with three features isn't a black box. The same model with engineered features pulled from a 200-table feature store, served behind three layers of caching, where nobody on-call can trace a prediction back to the inputs that produced it — that's a black box. Most "explainability" failures in production are actually lineage failures.

2. **There are at least four distinct audiences who need explanations, and they want different things.** The model risk team wants global behavior. The regulator wants a specific decision defended. A declined applicant wants a reason code. The on-call engineer wants to know which feature drifted. Don't conflate them — a single SHAP plot does not satisfy all four.

3. **The legal teeth.** Adverse-action notices under ECOA / Reg B, the EU AI Act's Article 86 right to explanation, GDPR Article 22 on automated decisions, fair-housing law, employment law. Spend a real minute on this. The compliance world has been writing rules about "meaningful information" on automated decisions for years now. Students need to feel the legal weight behind "your model needs to be explainable," not just the engineering tidiness.

4. **The security dimension of black-box risk gets undersold.** If you can't explain why a model flagged or didn't flag something, you can't detect that an adversary has manipulated the model into systematically mis-flagging. Explainability is a *detective control* against integrity attacks, not just a UX nicety. This is the connection to MITRE ATLAS evasion tactics in Module 3.

5. **The "interpretable model" trap.** People assume "use a linear model" or "use a decision tree" solves the problem. It doesn't, at scale. A 400-feature gradient-boosted tree with categorical encodings is functionally a black box to a non-technical reviewer even though it's "interpretable" in the textbook sense. Interpretability is about the audience's ability to follow the reasoning, not the model class.

6. **Global vs local — set the language up front.** Global = how the model behaves on average. Local = why *this one* prediction came out the way it did. Almost every confusion in XAI conversations comes from someone using one when they meant the other. The audit finding usually lives where local and global disagree.

7. **SHAP in one sentence:** for a given prediction, SHAP attributes "how much did each feature push this prediction away from the model's average?" The underlying *Shapley values* come from cooperative game theory — Lloyd Shapley's 1953 work on fair allocation of payout across contributors. The *SHAP framework* that applies them to ML predictions is Lundberg & Lee (2017) — two separate things, don't conflate them. You don't need to teach the math. You do need to teach the intuition: SHAP gives you a signed contribution per feature, per instance, that sums to the difference between the prediction and the baseline.

8. **LIME in one sentence:** fit a *simple* local model (typically linear) around the prediction by perturbing the input and seeing how the model's output shifts. LIME gives you a locally faithful explanation, but it's only faithful in a small neighborhood. Push too far from that point and the linear approximation falls apart.

9. **The differences between SHAP and LIME that matter in audit practice.** SHAP is more consistent (the underlying axiom — if a feature's contribution increases in every coalition, its SHAP value increases too). LIME has no such guarantee. LIME is faster and more flexible but its outputs are stochastic — run it twice, you may get different feature rankings. That alone disqualifies it for some regulator-facing audit work. SHAP has model-specific accelerators (TreeSHAP for tree ensembles, DeepSHAP for neural nets) that make it tractable on real models.

10. **Where SHAP and LIME mislead — the three failure modes I want students to internalize:**
    - **Correlation, not causation.** A SHAP value of +0.3 for `zip_code` doesn't mean "the ZIP caused the approval." It means the ZIP was associated with the approval direction in the model's logic. If ZIP is a proxy for protected class, you have a problem. SHAP cannot tell you it's a proxy.
    - **Background-distribution sensitivity.** SHAP values depend on the reference distribution you compute them against. Pick training data vs test data vs a curated baseline, you get different values. Auditors who don't know this can argue past each other for hours.
    - **Class-imbalance artifacts.** Heavily imbalanced data can make a feature look hugely important globally because it dominates minority-class predictions. The plot looks dramatic; the operational story is muddier.

11. **Proxy-variable detection — the actual workflow.** Don't just compute SHAP. Compare local importance to global importance for the same feature across flagged cases. When a feature's local contribution is dramatically larger than its global average in the same direction across multiple flagged instances, that's the proxy signal worth investigating. Then run a counterfactual: ablate the suspect feature to its training-set median and re-score. If the decision flips, you have your audit finding.

12. **The interpretation layer is the *real* deliverable.** Raw SHAP plots are not an audit report. The audit report says: "We computed local and global SHAP values for two declined cases. We found that feature X had a local contribution materially exceeding its global average. Counterfactual ablation of feature X flipped both decisions. We recommend re-review and a fairness audit on feature X." That's what governance reads. The plots are evidence; the *narrative* is the finding.

13. **Where XAI does *not* help.** It doesn't tell you whether the model is causally correct. It doesn't prove fairness. It doesn't establish counterfactual validity by itself. Students should leave this module knowing XAI is one tool in a stack, not a magic stamp of compliance.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| The content-moderation appeal (mirrors the SocialHub demo scenario) | A benign post gets flagged. Without explanation, the appeals reviewer has no way to confirm or overturn — and the platform can't tell whether the model is hitting dialect markers as a proxy. | Walkthrough — the moment that makes the legal risk feel concrete |
| The credit decision and the adverse-action notice | Anchors ECOA / Reg B. Reg B requires *specific* reasons for adverse action — not "model says no." A black-box system literally cannot produce a compliant notice. | Brief mention with the legal hook |
| Counterfactual ablation flipping a decision | A loan declined with ZIP-derived income proxy in the top SHAP contributors. Replace the proxy with the training median. Re-score. Decision flips from decline to approve. This is the move the exercise asks students to perform. | Walkthrough — sets up the implementation module precisely |
| Same model, two SHAP runs, different rankings | Two top-5 feature lists for the same instance computed against two reference sets. Make the room uncomfortable about treating SHAP outputs as deterministic. | Brief mention with the contrast |
| LIME on a non-linear region | A model with a sharp decision boundary. LIME's linear approximation works near the point of interest but mis-extrapolates a few units away. This is why you don't generalize a LIME explanation to nearby instances. | Brief mention with a quick sketch |
| Counter-example: when explainability is fine to skip | Internal-only recommender for product team A/B testing. Low stakes, no affected person, no regulator. Be honest that not every model needs SHAP — avoids the "everything must be explainable" overcorrection. | Brief mention |

---

## What NOT to Cover

- **How to write the audit memo with SHAP plots end-to-end** — that's the implementation module's deliverable (the UdaciBank loan-approval audit). The conceptual module sets up the thinking; the implementation module produces the artifact.
- **Specific library API details** (`shap.TreeExplainer(model)`, `lime_tabular.LimeTabularExplainer`, `detect_proxy_features()` helper) — implementation notebook.
- **Fairness metrics (demographic parity, equalized odds, predictive parity)** — covered in Module 10. Make a clean handoff: "XAI is the per-instance lens; fairness metrics are the population lens. You need both, and they answer different questions."
- **The EU AI Act's high-risk classification details and Article 11 documentation requirements** — Module 4. Reference Article 86 only as the right-to-explanation anchor.
- **MITRE ATLAS evasion tactics in detail** — Module 3. One-line connection only.
- **The math of Shapley values** — out of scope. Conceptual only. If a student wants the proof, point them to Shapley (1953) for the original game-theoretic result, and Lundberg & Lee (2017) for the ML application.

---

## Additional Notes

- **Analogies I'd reach for.** A black-box model is like a doctor who refuses to tell you why they prescribed something — you can sue the doctor, you cannot sue a model, so somebody ends up holding the bag. SHAP is like a credit-card statement that shows what each line item contributed to your total — it tells you what added up to what; it does not tell you whether the dinner at $80 was worth it.
- **Terminology I want used precisely.** "Opaque model" lands better than "black box" in compliance writing because regulators use it — but in the video both work, students will hear both in the wild. Don't say models "explain themselves" — they don't. SHAP "attributes contribution." LIME "approximates locally."
- **Avoid:** "Explainability is mandatory under the EU AI Act." It's nuanced — Articles 13, 50, and 86 each cover a different facet. Better to say "explainability obligations are woven through multiple Articles of the EU AI Act, and we'll get to which ones in Module 4."
- **Avoid framing proxy detection as "federal disparate impact" under Reg B.** Important precision point. The CFPB's April 2026 final rule on Regulation B *eliminated* federal disparate-impact liability under ECOA effective July 21, 2026 — disparate-impact theory is no longer actionable federally under Reg B. Proxy-detection findings now live in disparate-*treatment* via proxy under federal ECOA, plus state fair-lending laws and the Fair Housing Act, which continue to recognize disparate-impact theories. The XAI audit work is still essential; just frame the legal hook correctly.
- **A throwaway humanity beat that's been earned:** something like "the first time I had to defend a model's decision to a compliance lawyer, I realized very fast that 'the SHAP values clearly show feature 7' is not the answer they're looking for." Use sparingly — one such beat in the entire module is plenty.
- **A framing line worth seeding:** *"The single most expensive misuse of SHAP I've seen is treating a single per-instance plot as proof of fairness across a population. SHAP doesn't make that claim. The auditor did."* Pick something like this; it gives the module a quotable moment.
- **A reflective beat to land somewhere in the middle:** "If your auditor asked you to defend a SHAP plot to a regulator, could you also defend everything the plot does *not* say?" That gap is the discipline this module is closing.
- **Connection to the implementation module.** Students will run TreeExplainer on a gradient-boosting loan classifier (UdaciBank), compare local and global importances, detect a proxy variable, run a counterfactual ablation on the most-suspect proxy, and write a memo for model-risk and legal teams. By the end of this conceptual module they should be able to predict roughly what they'll do in the notebook — that's the test for whether the conceptual coverage worked.

---
