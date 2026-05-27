# Video: Understanding the AI Governance Operating Model
*Module 12.1 | Topic: Understanding the AI Governance Operating Model*

---

## Opening Hook

> *"A CTO walks into the executive offsite and says, 'we have AI governance — we have an AI policy, we have a review board.' Six months later, two launches slipped because nobody could approve them in time. The 'review board' turned out to be a recurring calendar invite nobody attended. The 'policy' was a PDF on the shared drive nobody had opened since onboarding. That's not governance. That's the shape of governance with none of the operating model behind it. The job of this module is to install the difference between governance on paper and an operating model — a real authority structure with decision rights, a real review board with quorum, real reporting cadences, real iteration. Governance is not a meeting. It's an *authority structure that meets*."*

The conceptual job is to install three things: (1) what an operating model actually is and how it differs from policy on paper, (2) the centralized vs federated trade-off and where each fits, and (3) the AI review board, reporting cadence, and the Govern-function feedback loop that ties the operating model back to NIST AI RMF Govern and ISO/IEC 42001.

---

## Key Discussion Points

1. **An "operating model" is an authority structure with decision rights, not a diagram.** The components:
   - **Scope** — which decisions does the operating model own; which does it explicitly *not* own.
   - **Authority** — who has approval power, who has recommendation power, who is informed.
   - **Cadence** — when and how often decisions get made (standing meeting + ad-hoc trigger).
   - **Membership** — named roles (not generic titles).
   - **Outputs** — what artifacts the operating model produces (decisions, board updates, audit packs).
   - **Iteration** — how the model itself evolves based on operating evidence.
   
   Most "governance" failures are missing one or more of these components.

2. **Why decision rights are the single most-skipped section.** Charters tend to be heavy on scope and membership and thin on decision rights. The result: the board meets, discusses, and *doesn't decide*. Months later nobody can tell whether the launch was approved. The fix is brutal specificity per decision type: who approves, who recommends, who is consulted, who is informed. That's it. Without that table, the operating model is decorative.

3. **The five canonical decision types worth designing for.**
   - **Launch approval** — does this AI system go to production?
   - **Retraining sign-off** — does this model get retrained, and on what data?
   - **Vendor onboarding** — does this AI vendor join the production stack? (Connects to Module 8.)
   - **Incident escalation** — when does an AI incident escalate from operational to board-level? (Connects to Module 6.)
   - **Red-team commissioning** — who decides whether to commission an adversarial test, who receives the findings, who signs the remediation off? Critical for jailbreak / prompt-injection / adversarial-prompt scope on GenAI systems.

4. **Centralized vs federated governance.** Two models, each with trade-offs:
   - **Centralized** — one AI review board owns all decisions across the org. Pros: consistency, single audit story, easier to upskill the board. Cons: bottleneck, slower decisions, board lacks domain depth across diverse use cases.
   - **Federated** — each business unit has its own AI governance with a central body for coordination. Pros: speed, domain depth, business ownership. Cons: inconsistent decisions, fragmented audit story, hard to enforce common standards.
   
   The mature pattern is *hybrid*: a strong central board owning high-stakes decisions (launch approval for High-Risk systems, vendor onboarding, incident escalation above S2), with federated subcommittees owning operational decisions within their domain.

5. **RACI matrix as the artifact.** RACI = Responsible, Accountable, Consulted, Informed. The matrix has decision types on one axis and named roles on the other. Each cell is one letter. Discipline:
   - Exactly one Accountable per decision (the person who answers if it goes wrong).
   - One or more Responsible (the people who do the work).
   - Consulted parties have to be heard before the decision; Informed parties learn after.
   - No empty rows, no decision types without an A.
   
   Building a RACI without these rules generates a matrix that looks like a deliverable but doesn't actually constrain behavior.

6. **The AI Review Board (AIRB) charter — five sections worth getting right.**
   - **Scope** — which decisions, which systems, which thresholds for escalation in. Out-of-scope statement is as important as in-scope.
   - **Membership** — named roles. Chair, voting members, advisory members. Tenure. Conflict-of-interest handling.
   - **Decision Rights** — per decision type, whether the AIRB approves, recommends, or is informed.
   - **Cadence and Quorum** — standing meeting cadence (typically monthly for active boards), ad-hoc trigger (e.g., S1 incident, blocking launch decision), quorum requirement (e.g., chair plus three voting members including at least one risk and one product).
   - **Reporting Outputs** — one-page board update, audit-committee deck, annual regulator pack.

7. **Membership shapes outcomes.** The board's membership *is* its bias. A board with no security representation under-weights security. A board with no product representation makes risk-averse decisions that don't ship. A board with no legal misses regulatory exposure. A board with no fairness/ethics rep misses population harm. The composition decision is the strategic decision; everything else is downstream.

8. **The reporting cadence layer.** Monthly board update — one page, KRI status, decisions taken, exceptions granted. Quarterly audit-committee deck — broader picture, risk-register movements, control effectiveness. Annual regulator pack — comprehensive, statutory anchors cited, ready for inspection. Reporting templates are *artifacts of the operating model*, not separate work. If the board's outputs don't flow into reporting, the board isn't connected to the rest of the organization.

9. **Red-team governance as a first-class component.** Jailbreak, prompt-injection, and adversarial-prompt testing isn't a one-off — it's a recurring exercise that has to be commissioned, scoped, executed, and remediated. The governance points: who commissions, who receives findings, who signs off on remediation, who decides when the next red team runs. Most operating models miss this entirely and it shows up as "we ran a red team that one time" in the audit.

10. **The NIST AI RMF Govern function loop.** This is where the operating model plugs back into Module 2. Each operating-model element maps to a NIST AI RMF Govern subcategory:
    - Govern 1.1 — policies and procedures
    - Govern 1.2 — accountability for risk management
    - Govern 1.4 — risk management process and outcomes established through transparent policies (vs. Govern 1.5 — ongoing monitoring and periodic review, which is closer to effectiveness evaluation)
    - Govern 2 — accountability structures
    - Govern 3 — workforce diversity and inclusion
    - Govern 4 — culture of risk-aware decision-making
    - Govern 5.x — robust engagement with relevant AI actors (the internal-stakeholder communication scope)
    - Govern 6.x — third-party / vendor risk and contingency (the third-party scope, vs. internal stakeholder communication which is closer to Govern 5)
    
    The mapping makes the operating model legible to anyone running a NIST AI RMF audit.

11. **The ISO/IEC 42001 (December 2023) parallel map.** The same operating-model elements map to ISO 42001 Annex A controls. The Govern Crosswalk has *both* NIST AI RMF Govern columns and ISO 42001 Annex A columns side by side because they are *complementary*, not competing.
    - A.2.2 — AI policy
    - A.3.2 — Internal organization
    - A.4 — Resources for AI systems (A.4.6 'Human resources' covers documentation of human competencies — training, role assignments, accountability — which is the human-accountability anchor for red-team remediation sign-off)
    - A.6.2 — AI system lifecycle (A.6.2.5 deployment; A.6.2.6 operation and monitoring — the operational AI-incident reporting anchor)
    - A.8.3 — Reporting of concerns
    - A.9 — Use of AI systems
    - A.10.2 — Allocating responsibilities (lifecycle responsibility allocation)
    - A.10.3 — Suppliers (the dedicated supplier-management control covering vendor assessment, due diligence, and ongoing oversight; closer anchor than A.10.2 for vendor-onboarding context)

12. **SR 11-7 effective challenge — the gold-standard validation pattern.** Federal Reserve SR 11-7 governs model risk management in banking. The "effective challenge" concept — that model validation must be *meaningfully independent* of model development, with the authority to reject — is the gold standard *even outside banking*. Mature operating models adopt the principle whether or not they're regulated by the Fed. Land this — students will see SR 11-7 cited in AI governance contexts well beyond finance.

13. **The two named failure modes.**
    - **Governance on paper only** — the charter exists, the RACI exists, the meetings are calendared, and nothing actually constrains decisions. The fix: every charter element has to be *operationalized* — a recurring meeting with quorum that actually happens, a RACI cell that an auditor could point to and a named human would answer, a reporting cadence that produces a board pack that gets read.
    - **Decision bottlenecks** — every decision routes through one body that can't keep up, so launches slip and exceptions accumulate. The fix: federation of operational decisions to subcommittees, with the central board owning only the high-stakes calls. Document the threshold explicitly.

14. **The Iteration Log — making the operating model legible as a living system.** Governance models *iterate*. V1 has gaps. The stress test surfaces them. V2 closes them. A formal Iteration Log — for at least three elements, name the Charter section or RACI row, describe v1 state, v2 state, and which named failure-mode finding drove the change — makes the iteration legible to the AI review board, to auditors, to regulators. It also signals to the org that the operating model is not fire-and-forget.

15. **Common implementation pitfalls.**
    - Charters with no decision rights.
    - RACI matrices with no Accountable owner per row.
    - Standing meetings with no quorum requirement (so they don't decide when half show).
    - Reporting cadences with no template (so each report is bespoke and unreadable).
    - No red-team governance (it shows up in the audit).
    - No iteration log (governance frozen in v1 forever).
    - Single board for the whole org with no federation (bottleneck).
    - Federation with no central body (fragmentation).

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| FinReady AI Review Board build (mirrors demo) | 1,500-person fintech building an AIRB from scratch. Two missed approvals last quarter, launch slipped, ad-hoc governance no longer survivable. Walk through the charter live — scope, membership, decision rights, cadence, reporting — and the Govern Crosswalk mapping to NIST AI RMF Govern + ISO 42001. Show why decision rights is the section most teams skip and what happens when they do. | Deep dive — primary anchor |
| MegaShop e-commerce governance redesign (mirrors exercise) | Global retailer with 12 AI use cases (recommendation, fraud, demand forecasting, ad targeting, customer service, dynamic pricing, search ranking, supply-chain optimization). Current state ad-hoc per business unit, no central review board, repeat decision-bottleneck and governance-on-paper failure modes documented in past PIRs. Walk through designing the RACI across launch approval, retraining sign-off, vendor onboarding, incident escalation, and jailbreak red-team commissioning. | Walkthrough — second anchor |
| The bottlenecked board | A single review board for the org owning every decision. Inbox: 47 pending decisions. Average wait time: six weeks. Launches slip. Use to motivate federation of operational decisions with central ownership of high-stakes calls. | Brief mention |
| The decision-rights black hole | A RACI matrix where one decision has no Accountable owner — every voting member assumed someone else owned it. The decision sat for two months. Use to land the "one A per row" discipline. | Brief mention |
| The red-team that wasn't | An AIRB that approved a GenAI launch six months ago. The launch document referenced a "red team to be commissioned post-launch." Six months later no red team has run; nobody is accountable for commissioning it. The audit finding writes itself. Use to motivate red-team governance as a first-class component. | Brief mention |
| The stress test that drove v2 | The MegaShop design's first pass on RACI assigned "Accountable" for incident escalation to the AIRB chair. The stress test surfaced the failure mode: at 3 a.m. with an S1 incident, the chair is asleep. v2 reassigns Accountable to the on-call AI Risk Officer with the chair as Informed. Iteration log captures the change. | Walkthrough — shows iteration in practice |
| SR 11-7 effective challenge applied outside banking | A SaaS company with no banking exposure adopts effective challenge — its model-validation function reports up a separate org structure from model development, with the authority to reject. Use to ground the principle. | Brief mention |

---

## What NOT to Cover

- **The full text of the charter or RACI sections** — implementation module's deliverable.
- **Specific SR 11-7 sections in depth** — reference the principle by name; don't unpack the supervisory letter.
- **Detailed NIST AI RMF subcategory definitions** — Module 2.
- **ISO 42001 Annex A control text** — reference the control IDs; don't read.
- **EU AI Act Article 27 Fundamental Rights Impact Assessment** — Module 4. Reference once as the deployer-side parallel.
- **Incident response playbook design** — Module 6. Reference incident escalation as a decision type only.
- **Vendor assessment scoring** — Module 8. Reference vendor onboarding as a decision type only.
- **The full ten-element charter template** — implementation module.

---

## Additional Notes

- **Analogies.** An operating model is to AI governance what an org chart is to a company — without it, the company exists but it's a crowd. Another: governance on paper is like a fire-evacuation plan posted on the wall but never drilled — the document exists; the *practice* doesn't. The drill is the operating model. A third: the RACI matrix is the *constitution* of the operating model; the standing meetings are the *legislature*; the AIRB's decisions are the *precedent*. Each piece is necessary.
- **Terminology.** "AI Review Board" or "AIRB" — the standard term. "Operating model" not "governance framework" (the framework is policy; the operating model is the practice). "Decision rights" plural. "RACI" capitalized. "Charter" for the document; "operating model" for the structure the charter describes. "Effective challenge" as the SR 11-7 phrase.
- **Precise nuances worth landing.**
  - NIST AI RMF Govern 1.4 vs 1.5 — 1.4 covers establishment of risk management process through transparent policies; 1.5 covers ongoing monitoring and periodic review. Effectiveness evaluation maps more cleanly to 1.5.
  - NIST AI RMF Govern 6.x's primary scope is third-party / vendor risk and contingency. Internal stakeholder communication maps more cleanly to Govern 5.x.
  - ISO 42001 A.10.2 (Allocating responsibilities) vs A.10.3 (Suppliers) — A.10.3 is the closer anchor for vendor-onboarding context; A.10.2 covers lifecycle responsibility allocation.
  - ISO 42001 A.6.2.6 (operation and monitoring) is the closer anchor for operational incident reporting than the higher-level A.6.2.
  - SR 11-7's effective-challenge principle is the gold standard *even outside banking* — don't suggest it only applies to regulated financial institutions.
- **Avoid:** treating the AIRB as a meeting rather than an authority structure. Avoid centralized-vs-federated as a binary — the mature pattern is hybrid. Avoid "governance" as a synonym for "policy" — the operating model is the practice. Avoid implying the operating model is one-time work — the Iteration Log exists because it isn't.
- **A grounded line worth seeding:** "The single best test for an operating model: if I walked into your office and asked who approved the most recent High-Risk launch, would you have a name and a date and a row in a log? If not, you have governance ambition. You don't have an operating model." Plant this early.
- **Another:** "Every charter I've seen fails the same way — beautiful on scope, beautiful on membership, blank on decision rights. The board meets, discusses, and *doesn't decide*. Decision rights is the section that turns a meeting into governance."
- **A reflective beat:** "Picture your team's last AI launch. Walk back the decision chain. Who actually approved it? In what artifact is that approval recorded? If you can't answer in under thirty seconds, the operating model isn't operating." Place around the decision-rights discussion.
- **A throwaway humanity beat:** "The first AI review board I ever set up had no quorum rule. The first meeting, two people showed up. We made decisions anyway. Three weeks later, one of those decisions came back to bite — and the absent voting members claimed they'd never agreed. After that, we wrote quorum into the charter and held the line." Use sparingly.
- **Connection to the implementation module.** Students will design the operating model for MegaShop in Excel across eight sheets — Scenario Brief, Charter (scope, membership, decision rights, cadence, quorum, reporting outputs), RACI Matrix covering five decision types including jailbreak red-team commissioning (two pre-filled), Reporting Cadence outline, Red-Team Governance outline, Govern Crosswalk mapping each element to NIST AI RMF Govern subcategories *and* ISO/IEC 42001 Annex A controls side-by-side, Failure Mode Stress Test against the two named failure modes (governance on paper; decision bottlenecks), and Iteration Log capturing v1 → v2 changes for at least three elements. After this module they should be able to predict the charter's five sections, the RACI rules (one A per row, no empty rows), why the Govern Crosswalk has both columns, and why the Iteration Log is a first-class artifact rather than an afterthought.

---
