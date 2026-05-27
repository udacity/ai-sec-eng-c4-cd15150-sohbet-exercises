# Video: Understanding Bias and Fairness Auditing for AI Governance
*Module 10.1 | Topic: Understanding Bias and Fairness Auditing for AI Governance*

---

## Opening Hook

> *"Your loan-approval model comes back with a demographic-parity ratio of 0.78 between two protected groups. Is 0.78 launchable? An ML engineer says yes — close enough, no other model gets better numbers. A lawyer says no — the EEOC 4/5ths rule sets the floor at 0.80, and 0.78 is two points under. A product manager says it depends — does the business decision flip if we add per-group thresholds, and what does that cost us in accuracy? They're all right. None of them is the AI Risk Officer. That role is the one that has to *interpret* 0.78 — translate the number into a launch decision the AI review board can defend. That interpretation layer is the work this module is about."*

The conceptual job is to install three things: (1) where bias actually comes from in ML systems, (2) the fairness metrics themselves and why no single number is sufficient, and (3) the interpretation layer — turning fairness numbers into launch / controls / no-go decisions that the GRC practitioner owns.

---

## Key Discussion Points

1. **Three kinds of bias to keep separated.**
   - **Data bias** — the training data does not represent the population the model will be deployed on, or it encodes historical inequities the labels carry forward. Examples: a hiring dataset where historical hiring was biased; a medical-imaging dataset overweighted toward one demographic.
   - **Algorithmic bias** — the model architecture, objective function, or training procedure systematically advantages or disadvantages groups even on representative data. Examples: a model that minimizes average loss without considering subgroup performance; a regularization choice that erases minority signal.
   - **Deployment bias** — the system is used in contexts it wasn't designed for, or downstream human decision-makers interact with model outputs differently across groups. Examples: a credit-scoring model trained on US data deployed in another country; a recommendation tool whose suggestions are accepted at different rates by different demographic groups.
   
   Most production failures are mixtures. Don't oversimplify.

2. **Protected attributes — what counts and why it matters.** Protected attributes are categories where discrimination is legally regulated or ethically central — race, color, religion, sex, national origin, age, disability, sexual orientation, gender identity, genetic information, military status. The exact list varies by jurisdiction and statute (Title VII, ECOA, ADA, FHA, state laws, GDPR Article 9 special categories). Get this right because fairness audits depend on which attribute you're auditing against, and that depends on the legal regime that applies.

3. **Why "we just don't use the protected attribute" doesn't work.** Removing race or gender from the input features does not remove bias. The model finds proxies — ZIP code as a proxy for race, name as a proxy for ethnicity, employer as a proxy for socioeconomic class. *Fairness through unawareness* is a known failure mode. The work is detecting and mitigating proxy effects, not pretending the attribute doesn't exist.

4. **The three core fairness metrics.**
   - **Demographic Parity (DP)** — does each group receive the positive outcome at roughly the same rate? Threshold: DP ratio ≥ 0.80 anchors to the EEOC 4/5ths rule (which has external regulatory provenance, not a firm-policy choice).
   - **Equalized Odds (EO)** — does each group have similar true positive *and* false positive rates? Difference ≤ 0.10 is a common firm-policy threshold (varies across organizations from 0.05 to 0.15 depending on use case and risk tier).
   - **Equal Opportunity (EOpp)** — does each group have similar true positive rates? Difference ≤ 0.10 same caveat as Equalized Odds.

5. **Compute the metrics from confusion-matrix primitives first.** This is the pedagogical move. ~15 lines of code that anyone can read: per-group confusion matrix → derive TPR, FPR, FNR, precision → assemble into DP / EO / EOpp. Then validate against Fairlearn as a one-line cross-check. Students who learn the primitives first never get confused later. Students who start with `MetricFrame.by_group(...)` never internalize what the number means.

6. **The impossibility trilemma.** Three metrics generally cannot all hold simultaneously except in degenerate cases. Push one metric inside its bound and others move outside. This is a *practical* observation closely related to the formal impossibility result (Chouldechova 2017; Kleinberg-Mullainathan-Raghavan 2016 — which formally targets *calibration vs error-rate balance under unequal base rates*). The trilemma framing is a pedagogical convenience; the formal result is sharper. Be honest about the relationship.

7. **What the trilemma means for the GRC practitioner.** You cannot pass every fairness metric. You have to pick. The picking is the governance work — which metric matters most for *this* product, in *this* regulatory context, on *this* population? Lending tends to anchor on DP (4/5ths rule) and EOpp (qualified-applicant disparity). Medical diagnostics tends to anchor on EO (false-negative cost parity across groups). Hiring varies depending on the role and the jurisdiction. The choice is documented, defended, and ratified at the review board.

8. **Predictive Parity and other metrics in the family.** Predictive parity = similar positive predictive value across groups. Calibration = predicted probabilities mean the same thing across groups. Counterfactual fairness = decision doesn't change under counterfactual flip of protected attribute. Mention these as part of the broader family so students don't think DP / EO / EOpp is exhaustive. The bonus section in the exercise touches predictive parity.

9. **Interventions and the accuracy trade-off.** Three common interventions:
   - **Pre-processing** — modify the training data. Reweighing (AIF360's `Reweighing` is the canonical implementation), resampling, synthetic data generation. Operates before model training.
   - **In-processing** — modify the training procedure. Adversarial debiasing, fairness constraints in the loss. Operates during model training.
   - **Post-processing** — modify the decision threshold per group. Fairlearn's `ThresholdOptimizer` is the canonical implementation. Operates after the model is trained.
   
   The implementation module focuses on post-processing per-group threshold adjustment as the intervention students test. Every intervention trades off against accuracy. Quantify the trade-off — what's the accuracy cost of bringing the worst metric inside policy bounds?

10. **The interpretation layer — the GRC practitioner's actual job.** Given a fairness audit result, the practitioner has to answer: launchable, conditionally launchable (with which controls), or no-go? The decision rests on (a) policy thresholds, (b) regulatory anchors, (c) intervention options and their costs, (d) the population at risk, (e) the harm if wrong. This is not an ML question. It's a *governance* question that consumes ML evidence. Land this clearly — the room where fairness gets settled is the AI review board, not the ML standup.

11. **The 0.78 question, walked through.** Demographic-parity ratio of 0.78 between two protected groups. Below 0.80 EEOC anchor. Is it launchable?
    - What's the model doing? Loan approval. Regulatory regime: ECOA / Reg B + state fair lending.
    - What's the affected population scope? National? Regional?
    - What's the cost of fixing it? Per-group threshold adjustment might bring DP ratio to 0.84 — at the cost of 1.2 percentage points of overall accuracy.
    - What controls would change the answer? Adding monitoring? Different applicant routing? Manual review on declined applicants in the disadvantaged group?
    - Who signs off? The AI review board, with documented rationale.
    
    The recommendation: not "launch" or "no-go" — it's a *conditional launch* with named controls, named owner, monitoring cadence, escalation rules. That's the shape of a defensible decision.

12. **Where GRC scope ends and legal / ethics scope begins.** GRC owns the framework, the assessment, the metrics, the controls. Legal owns the statutory interpretation (does this violate ECOA / Title VII / the EU AI Act?). Ethics owns the population-impact question that the metrics can't fully answer. Don't collapse these. The AI Risk Officer's role is *integration*, not substitution.

13. **The GenAI surface — the metric pattern transfers.** The same fairness primitives — per-group TPR / FPR / FNR derived from a confusion matrix — apply to LLM-mediated decisions like resume screening or hiring chat agents. The policy anchors still apply: ECOA / Reg B, NYC LL-144, EU AI Act Annex III §4. The technical surface is different (LLM advance/screen-out outputs versus a binary classifier's probability) but the audit shape holds.

14. **Common failure modes.**
    - Picking a metric and treating it as the truth without justifying the choice.
    - Removing protected attributes and declaring fairness solved.
    - Running Fairlearn without understanding what it computes.
    - Treating the impossibility trilemma as a license for inaction ("we can't satisfy all three, so we won't satisfy any").
    - Recommending an intervention without quantifying the accuracy cost.
    - Producing audit numbers without an interpretation memo.
    - Confusing GRC scope (controls and process) with legal scope (statutory interpretation).

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| SafeWheels auto-pricing model with DP = 0.78 (mirrors demo) | Auto-insurance pricing model, demographic-parity ratio of 0.78 between two protected groups (age band and ZIP-derived geographic cluster). Walk through computing all three metrics from confusion-matrix primitives, the Fairlearn cross-check, comparison against policy thresholds, per-group threshold counterfactual, and the launch / conditional / no-go decision with rationale. | Deep dive — primary anchor |
| UdaciBank loan-approval audit (mirrors exercise) | New loan-approval model with three subgroup columns — gender (male/female), race (4 categories), age band (under 25 / 25–44 / 45–64 / 65+). Walk through how the same three metrics get computed across three subgroup dimensions, the policy thresholds (DP ratio ≥ 0.80, EO difference ≤ 0.10, EOpp difference ≤ 0.10), and what the recommendation memo would look like. | Walkthrough — second anchor |
| The proxy-variable trap | A team removes race from the inputs. Fairness through unawareness. The model uses ZIP and surname; the disparity persists. SHAP from Module 1 catches the proxy. Use to motivate that "just don't use the attribute" isn't a strategy. | Brief mention with the Module 1 connection |
| The trilemma in action | A loan model where pushing DP from 0.78 to 0.85 via threshold adjustment widens EO difference from 0.07 to 0.13 — crossing the policy threshold in the other direction. The choice between which metric to favor is the governance work, not the ML work. | Walkthrough — third anchor |
| Pre-processing vs post-processing intervention | Compare conceptually: AIF360 `Reweighing` operates on training data; Fairlearn `ThresholdOptimizer` reassigns the decision threshold per protected group after training. Both valid; they intervene at different points in the pipeline. | Brief mention |
| The LLM hiring screen (Section 7 bonus) | A synthetic LLM hiring-screen fixture — 200 candidates, gender label, LLM advance/screen-out, human qualification label. Run the same DP / EO / EOpp primitives. Show the metric pattern transfers to a GenAI surface without losing the policy anchor (ECOA / Reg B, NYC LL-144, EU AI Act Annex III §4). | Brief mention |
| A defensible "Conditional Launch" memo | What the launch recommendation memo looks like with explicit recommendation, two-to-three controls (per-group thresholds, additional monitoring, retraining cadence), a 90-day monitoring plan with metrics, cadence, owner, escalation path. | Walkthrough — fourth anchor |

---

## What NOT to Cover

- **The full implementation of the fairness primitives in Python** — implementation module.
- **Fairlearn API details (`MetricFrame`, `ThresholdOptimizer` signatures)** — implementation module.
- **AIF360 API details** — implementation module mentions as alternative, doesn't deep-dive.
- **The mathematical proof of the impossibility result** — out of scope; cite the references (Chouldechova 2017; Kleinberg-Mullainathan-Raghavan 2016) and move on.
- **SHAP-based proxy detection** — Module 1. Reference once.
- **EU AI Act Annex III tier classification mechanics** — Module 4. Reference §4 employment and §5(b) creditworthiness as the relevant anchors.
- **GDPR Article 9 special-category data handling** — Module 11.
- **The full further-reading list of fairness benchmarks (BBQ, BiasInBios, HELM)** — flag as resources; don't unpack.
- **Aequitas, AIF360, BBQ, HELM in depth** — out of scope. Reference by name only.

---

## Additional Notes

- **Analogies.** The impossibility trilemma is like trying to optimize for low rent, short commute, and a quiet neighborhood — pick two. The interpretation layer is like the difference between knowing the lab results and knowing the diagnosis — the numbers are evidence, the decision is judgment that consumes the evidence. The interventions are like three different remediation options for a sloped floor — re-pour the slab (pre-processing), shim during construction (in-processing), or shim the furniture after (post-processing). Each has a cost; each has a place.
- **Terminology.** Use full names on first mention — "Demographic Parity (DP)," "Equalized Odds (EO)," "Equal Opportunity (EOpp)." Capitalize. "Per-group threshold adjustment" is the canonical post-processing intervention name. "Protected attribute" not "protected class" (the former is the data-science term, the latter is the legal term; use protected attribute in the technical sections).
- **Precise nuances worth landing.**
  - The 0.80 demographic-parity floor anchors to the EEOC 4/5ths rule — *external regulatory provenance*. The 0.10 ceiling for EO / EOpp is a *firm-policy threshold* chosen here; real organizations set it between 0.05 and 0.15. Don't conflate the two.
  - The formal impossibility result (Chouldechova / Kleinberg) targets *calibration vs error-rate balance under unequal base rates*. The DP / EO / EOpp "trilemma" is a related practical observation, not the formal proof.
  - ECOA + Reg B remain the operative federal fair-lending anchor. The CFPB's April 2026 final rule on Regulation B narrowed federal *disparate-impact* liability, but disparate-treatment analysis (including via proxies) remains actionable. State fair-lending laws and the Fair Housing Act continue to recognize disparate-impact theories.
- **Avoid:** treating any one metric as definitive. Avoid suggesting Fairlearn / AIF360 / Aequitas "solve" fairness — they compute numbers; the interpretation is still the practitioner's. Avoid the "everything is biased so why bother" cynicism — the work is meaningful even where it's imperfect. Avoid implying that a model passing the audit is "fair" — it is *passes the audit under the current thresholds on the current data*. Different framing.
- **A grounded line worth seeding:** "Fairness metrics are inputs to a governance decision, not the decision itself. The day a number replaces a judgment call is the day the program stops being governance." Plant this around the interpretation layer.
- **Another:** "I've watched teams spend three months optimizing a fairness metric they could not have defended choosing if a regulator asked them why. The metric selection is the first audit finding — answer it before you compute anything."
- **A reflective beat:** "Imagine your model returns DP = 0.79. Half a point under the policy threshold. What's the smallest thing you can change about the model's deployment that flips your recommendation from no-go to conditional launch? That answer is your controls menu." Place around the interpretation discussion.
- **A throwaway humanity beat:** "The first fairness audit I produced had beautiful charts and no recommendation. The AI review board asked the obvious question and I had no answer ready. I learned then that the chart isn't the audit — the recommendation is." Use sparingly.
- **Connection to the implementation module.** Students will run a focused fairness audit on UdaciBank's loan-approval model — load `loan_predictions.csv` with three subgroup columns, compute DP / EO / EOpp from confusion-matrix primitives in ~15 lines, validate against Fairlearn as a one-liner, compare against policy thresholds (0.80 / 0.10 / 0.10), test the per-group threshold adjustment intervention, quantify the accuracy trade-off, render a before/after metrics chart, and draft the Launch / Conditional Launch / No-Go memo with recommended controls and a 90-day monitoring plan. The Section 7 bonus runs the same primitives on the LLM hiring-screen fixture to show the pattern transfers to GenAI surfaces. After this module they should be able to predict the audit pipeline, the policy threshold structure, the impossibility-trilemma walk, and the shape of a defensible recommendation memo.

---
