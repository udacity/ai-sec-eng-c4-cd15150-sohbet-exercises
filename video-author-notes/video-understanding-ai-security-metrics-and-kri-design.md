# Video: Understanding AI Security Metrics and KRI Design
*Module 7.1 | Topic: Understanding AI Security Metrics and KRI Design*

---

## Opening Hook

> *"A CISO asks 'how is our AI program doing?' and gets handed a 47-tile dashboard with twelve colors and three pie charts. After thirty seconds they realize they cannot tell whether anything is wrong. That dashboard is not a KRI program. That's a metrics museum. The job of this module is to install the difference — KRIs are a *small, derived, actionable* set of indicators that tell the board, at a glance, whether the AI risk register is being managed. And the right place to start when designing them is not the dashboard tool. It's the risk register."*

I want students to leave knowing two things: (1) what a *Key Risk Indicator* actually is and how it's different from a metric, and (2) how to design a KRI set that drives decisions rather than displays activity.

---

## Key Discussion Points

1. **Metric vs KPI vs KRI — get the vocabulary right.**
   - **Metric** — any quantitative measurement. Latency, throughput, accuracy, refusal rate, drift score, jailbreak attempt count. There are thousands of these.
   - **KPI** (Key Performance Indicator) — a metric tracked because it indicates whether the system is *performing its intended function*. Accuracy, uptime, latency. KPIs ask "is the system working?"
   - **KRI** (Key Risk Indicator) — a metric tracked because it indicates whether *a specific risk* on the risk register is materializing. Subgroup FNR delta, drift score, jailbreak-classifier hit rate, vendor SLA breach rate. KRIs ask "is the risk we said we were managing actually being managed?"
   
   Same number can be all three depending on what conversation it's serving. The discipline is *naming the conversation*.

2. **KRIs are *derived* from the risk register, not picked from a vendor catalog.** This is the single most important point in the module. Every KRI must trace back to a specific row in the risk register. The flow: risk register row → "how would we know this risk is materializing?" → that's the KRI. If you can't draw the line from a KRI back to a register row, the KRI is decoration.

3. **The shape of a good KRI.** Six required attributes:
   - **Input source** — exactly which data, log, monitoring stream feeds the metric.
   - **Threshold** — green / amber / red bands with specific numeric values.
   - **Owner** — a *named role* (not a team) accountable for the metric.
   - **Escalation path** — at amber, who is notified; at red, who is paged.
   - **Cadence** — how often the metric is computed (real-time, daily, weekly, monthly).
   - **Board-facing interpretation** — one sentence explaining what this number means and what would trigger action.
   
   Miss any of the six and the KRI isn't actionable.

4. **Leading vs lagging indicators.** A *lagging* KRI tells you the risk has already materialized (incident count, regulator inquiries, customer complaints). A *leading* KRI tells you the conditions for the risk are present (drift score creeping up, anomalous query rate rising, % of models without a current threat model). You want both, but leading KRIs are what give you time to act. Most board dashboards over-index on lagging because they're easier to measure.

5. **Threshold design is where most KRI programs fail.** Picking a number is easy. *Justifying* the number is the work. Green / amber / red bands should be anchored in (a) the risk-register row's tolerance, (b) historical baselines, (c) regulatory or contractual thresholds, or (d) a documented policy decision. A threshold with no rationale flips into "what color is it today?" within a quarter and the program loses credibility.

6. **Escalation as a first-class design dimension.** A KRI without an escalation rule is a metric. The escalation rule answers: at amber, what changes? At red, what changes? "We'll discuss it at the monthly meeting" is not an escalation rule. "At amber, the platform lead is paged within four hours and the KRI is added to the next AI review board agenda; at red, the CRO is paged immediately and the related production model is gated for change-freeze until amber clears" — that's an escalation rule.

7. **The board-facing narrative.** Each KRI needs *one sentence* that translates the number into business meaning. "Refusal rate above 7% indicates either policy drift on the assistant's guardrails or attempted misuse — both warrant investigation." Without the narrative sentence, the board sees a number and asks "so what?" The narrative is the answer to "so what."

8. **Why a dashboard is *not* a KRI program.** The dashboard is a *communication artifact*. The KRI is a *function* (literally — in code, a small unit-testable function that returns `{value, status, owner, timestamp}`). Build the function first. The dashboard is the rendering of the function's output. Tool-agnostic at this stage — the same KRI function should be portable across Tableau, Looker, Grafana, or a Notion table.

9. **Portfolio-level vs system-level KRIs.** A KRI program covers the whole AI portfolio, not one system. Some KRIs roll up across multiple systems (% of production models with a current threat model). Some are system-specific (refusal rate on the customer-support assistant). Get this distinction visible. The CISO cares about portfolio shape; the platform lead cares about system shape.

10. **The "absence of a mature standard AI security baseline" — how to compensate.** Unlike cybersecurity, which has decades of accumulated baselines (NIST SP 800-53 control families, CIS Controls, OWASP Top 10), AI security has no equivalent agreed-upon baseline you can copy. That means *every* KRI program has to derive its set from first principles — from the risk register. Don't apologize for it; design for it. The compensating discipline is rigor in tying each KRI to a risk-register row and to a policy threshold.

11. **The common failure modes.**
    - **Tool-driven KRI selection.** "What does Datadog give us? Let's call that our KRI." No tie to risk register.
    - **Metric proliferation.** 47 KRIs. None of them actionable.
    - **Thresholds without rationale.** Numbers picked because they "feel right."
    - **No escalation specificity.** "We'll watch this" is not an escalation rule.
    - **No board narrative.** The CISO can't tell the audit committee what it means.
    - **Drift into operational metrics.** Confusing KPIs (system working?) with KRIs (risk being managed?).
    - **KRI without an owner.** Nobody is paged when it goes red.

12. **A representative KRI set for an AI portfolio.** Five is roughly the right number for a leadership dashboard — enough to cover the major risk categories without becoming a metrics museum.
    - **Subgroup FNR delta** — fairness signal, derived from a fairness-audit row of the register.
    - **Drift score** — model-validity signal, derived from a model-degradation row.
    - **Jailbreak-classifier hit rate** — GenAI-specific security signal, derived from a prompt-injection / misuse row. (Note: this is distinct from a "refusal rate" KPI — the refusal-rate metric anchors a quality conversation; the jailbreak hit rate anchors an *adversarial misuse* conversation.)
    - **Vendor SLA breach rate** — third-party risk signal, derived from the vendor-onboarding / availability rows. Connects to Module 8.
    - **% of production models with a current threat model** — coverage signal, derived from the threat-modeling-completeness row. Connects to Module 3.
    
    The shape matters — fairness, model validity, adversarial misuse, third-party, coverage. Five risk dimensions, five KRIs.

13. **The KRI calculator as code.** Implement each KRI as a small pure function: input the data, return `{value, status, owner, timestamp}`. That makes it (a) unit-testable, (b) portable across dashboards, (c) auditable. The dashboard becomes a thin presentation layer on top of an audited library.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| Aurora Assistant refusal-rate KRI (mirrors demo) | A B2B SaaS LLM-powered customer-support assistant. One row in the risk register: "Anomalous refusal-rate spikes indicate either policy drift or attempted misuse — both warrant investigation." Derive the KRI: refusal rate; green ≤ 3%, amber 3–7%, red > 7%; daily rolling-24h cadence; escalation Platform Lead → AI Review Board at amber → CRO + AppSec at red. Walk through the six attributes and the narrative sentence. | Walkthrough — anchor example |
| UdaciBank's 5-KRI portfolio (mirrors exercise) | Digital-only fintech, 10 production models, the CISO needs a portfolio-level governance system. Walk through the five KRIs: subgroup FNR delta, drift score, jailbreak-classifier hit rate (LLM customer-support assistant), vendor SLA breach rate, % of production models with a current threat model. Each KRI sized for what it should cover. | Walkthrough — second anchor |
| The tile-museum dashboard | Show conceptually a 47-tile dashboard and ask whether the viewer can tell at a glance which risk is materializing. Use this to motivate the small, actionable KRI set. | Brief mention |
| A KRI without an owner | "Drift score" tracked, no owner named, goes red, nobody pages anyone, three weeks of drift accumulate before anyone notices. Motivates the owner attribute. | Brief mention |
| The two threshold types | One KRI threshold anchored in a regulatory cap (a fairness ratio below 0.80 — EEOC 4/5ths rule, connects to Module 10). Another threshold anchored in a policy decision (a refusal rate above 7%, chosen by AI review board policy). Both legitimate. The discipline is *naming* which one each threshold is. | Brief mention |

---

## What NOT to Cover

- **Python implementation of each KRI function in detail** — implementation module (`compute_subgroup_fnr_delta()`, `compute_drift_score()`).
- **Population stability index math** — implementation module.
- **Fairlearn / AIF360 API specifics** — Module 10. Touch lightly here as the source of fairness metrics.
- **Specific dashboard tools (Tableau, Grafana, Looker)** — out of scope. The point is *tool-agnostic*.
- **MITRE ATLAS technique IDs** — Module 3.
- **Vendor SLA contract negotiation** — Module 8.
- **Incident response playbook design** — Module 6. Mention KRIs as the proactive side that *feeds* incident detection.
- **EU AI Act Article 72 post-market monitoring** — Module 4. Connect lightly: "this is the operational shape of what Article 72 requires."

---

## Additional Notes

- **Analogies.** KRIs are to AI risk what the dashboard cluster is to a car — a small set of indicators the driver glances at without taking eyes off the road. Speed, fuel, RPM, temperature. Not 47 tiles. Five things the driver actually needs to know. A metric is data; a KRI is *intelligence about a specific risk*.
- **Terminology.** "Key Risk Indicator" spelled out on first mention. "Threshold" not "limit." "Escalation path" not "alert chain." "Cadence" not "frequency." These are the words the board reads, so use them.
- **Avoid:** treating "metrics" and "KRIs" as interchangeable. Avoid recommending specific dashboard tools. Avoid implying KRI design is a one-time exercise — KRIs evolve as the risk register evolves. Avoid the "more is better" trap.
- **A grounded line worth seeding:** "I've watched teams build beautiful dashboards that no one acts on. The fix wasn't a better dashboard. It was a smaller KRI set with named owners and real escalation rules. Five KRIs that get acted on beats fifty that get admired."
- **Another:** "Every threshold in your KRI set should have a one-sentence answer to 'why this number?' If the answer is 'felt right,' it won't survive the first quarterly review."
- **A reflective beat:** "Look at the dashboard your team uses today. For each tile, can you name the risk-register row it derives from? If half the tiles fail that test, your KRI set is decoration, not governance." Place near the middle.
- **A throwaway humanity beat:** "The first KRI dashboard I ever shipped had fourteen tiles. The CRO asked me at the readout 'which three of these would wake you up at night?' I could only name two confidently. The next version had five." Use sparingly.
- **Connection to the implementation module.** Students will define five KRIs at portfolio level for UdaciBank in Excel (two pre-filled, three to complete) with input source, thresholds, owners, escalation, cadence, and the board-facing one-sentence narrative; complete the Risk Register Crosswalk tying each KRI back to a register row; lay out a one-page Dashboard Mockup; and implement two KRI functions in Python (`compute_subgroup_fnr_delta()`, `compute_drift_score()`) plus run the provided unit tests, then render a 5-KRI dashboard PNG. After this module they should be able to predict the six attributes a KRI needs, the shape of the function signature, and why each KRI is anchored to a register row.

---
