# AI Governance Operating Model

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students to design the core of an AI governance operating model — an AI Review Board charter and a RACI matrix covering the 5 most-decided decision types — to map each element to **both NIST AI RMF Govern and ISO/IEC 42001** (December 2023, AI Management Systems standard) on the Govern Crosswalk so learners see both maps in one place rather than as competing standards, and to stress-test the design against the two named common failure modes (governance on paper; decision bottlenecks). The stress test is then rolled forward into an **Iteration Log** showing v1 → v2 RACI / charter changes driven by the findings. Students learn that "the board" is not a meeting but an authority structure that meets, that decision rights are the single most-skipped section in real-world charters, and that **SR 11-7 effective challenge** is the gold-standard validation pattern even outside banking.

## File Structure

```
12_ai-governance-operating-model/
├── demo/
│   └── governance_demo.xlsx                    # Filled-in instructor reference (FinReady fintech AIRB charter)
├── exercises/
│   ├── starter/
│   │   └── ai_governance_core.xlsx             # Student starting file (MegaShop e-commerce)
│   └── solution/
│       └── ai_governance_core.xlsx             # Completed solution with Reasoning: annotations
└── README.md
```

Each workbook contains eight sheets: Scenario Brief, Charter, RACI Matrix, Reporting Cadence, Red-Team Governance, Govern Crosswalk (with both NIST AI RMF Govern and ISO/IEC 42001 columns), Failure Mode Stress Test, Iteration Log.

## Demo

**Scenario: FinReady** — A 1,500-person fintech building an AI review board from scratch. Two missed approvals last quarter caused a launch slip; ad-hoc governance is no longer survivable.

The instructor drafts the AI review board charter live across five sections (scope, membership, decision rights, cadence, reporting), using FinReady as the case study, and shows why most charters fail at "decision rights." The walkthrough then maps each charter element to a NIST AI RMF Govern subcategory on the Govern Crosswalk sheet, and runs the design through the two named failure modes on the Failure Mode Stress Test sheet.

## Exercise

**Scenario: MegaShop** — A global e-commerce retailer with 12 AI use cases in flight (recommendation, fraud, demand forecasting, ad targeting, customer service, dynamic pricing, search ranking, supply-chain optimization). The current state is ad-hoc: each business unit governs its own models, there is no central review board, and post-incident reviews show repeated decision-bottleneck and "governance on paper" failure modes.

As Chief AI Risk Officer, design the core of MegaShop's AI governance operating model — RACI matrix and AI review board charter, plus an outline of reporting cadence and red-team governance for follow-up engineering.

### Task

**Part 1 — Charter**

1. **Scope** — Which decisions does the AIRB own? Which does it explicitly NOT own?
2. **Membership** — Named roles (not generic titles): chair, voting members, advisory members.
3. **Decision Rights** — For each decision type the AIRB owns, mark whether the AIRB approves, recommends, or is informed.
4. **Cadence and Quorum** — Standing meeting cadence, ad-hoc trigger, quorum requirement.
5. **Reporting Outputs** — One-page board update, audit-committee deck.

**Part 2 — RACI Matrix**

1. **Cover 5 decision types** — launch approval, retraining sign-off, vendor onboarding, incident escalation, **jailbreak red-team commissioning** (with explicit jailbreak / prompt-injection / adversarial-prompt scope).
2. **For each decision type, assign R / A / C / I** — Responsible / Accountable / Consulted / Informed across the named roles. Two decision types are pre-filled.

**Part 3 — Reporting Cadence (outline)**

1. **List the cadences in bullets only** — monthly board update, quarterly audit committee, annual regulator pack. Full templates are out of scope.

**Part 4 — Red-Team Governance (outline)**

1. **List the red-team governance points in bullets only** — commissioner, findings recipient, remediation sign-off. Full procedure is out of scope.

**Part 5 — Govern Crosswalk**

1. **Map each charter element / RACI row to a specific NIST AI RMF Govern subcategory** — Govern 1.1, 1.2, etc.
2. **Map the same element to its corresponding ISO/IEC 42001 control** — A.2.2 AI policy, A.3.2 Internal organization, A.6.2.5 AI system deployment, A.10.2 Suppliers, etc. The Govern Crosswalk has both columns side-by-side so you see them as complementary maps, not competing standards.

**Part 6 — Failure Mode Stress Test**

1. **For each named failure mode (governance on paper; decision bottlenecks)** — write one paragraph naming where in your design that failure mode would land, and the specific element that prevents it.

**Part 7 — Iteration Log**

1. **Translate stress-test findings into v1 → v2 changes** — for at least three elements, name the Charter § or RACI # row, describe the v1 state, the v2 state, and which named failure mode finding drove the change. The point is to show the design is not fire-and-forget: governance models iterate, and an Iteration Log makes the iteration legible to the AI Review Board.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the ISO/IEC 42001 and NIST AI RMF citations used in this lesson.

- **ISO/IEC 42001 Annex A — supplier vs allocation controls.** Within Clause A.10 (Third-party and customer relationships), **A.10.3 "Suppliers"** is the dedicated supplier-management control covering assessment, due diligence, and ongoing oversight. **A.10.2 "Allocating responsibilities"** in the same clause covers how the organization divides responsibilities for the AI system across its lifecycle. Where the Govern Crosswalk references A.10.2 in a vendor-onboarding context, A.10.3 is the closer anchor; both controls can apply in tandem. See [ISMS.online — A.10.3 Suppliers](https://www.isms.online/iso-42001/annex-a-controls/a-10-third-party-and-customer-relationships/a-10-3-suppliers/).
- **ISO/IEC 42001 Annex A — incident reporting.** Operational AI-incident reporting in ISO 42001 sits primarily under Clause **A.9 (Use of AI systems)** and **A.6.2 (AI system life cycle — operation and monitoring)**, with A.6.2.6 covering operation and monitoring specifically. Clause A.4 covers Resources for AI systems. A.4.6 'Human resources' addresses documentation of human competencies across the AI lifecycle — training, role assignments, and accountability for AI decisions — which is the role A.4.6 plays in the Crosswalk's red-team remediation sign-off (the human-accountability anchor for the sign-off). For incident detection and reporting workflows specifically, A.6.2.6 (AI system operation and monitoring) and Clauses A.9 (Use of AI systems) and A.8.3 (Reporting of concerns) are the closer anchors.
- **NIST AI RMF Govern 6.x — third-party and contingency scope.** [NIST AI 100-1 Govern 6.1](https://airc.nist.gov/airmf-resources/playbook/govern/) addresses *"Policies and procedures address AI risks from third-party entities."* Govern 6.2 addresses *"Contingency processes handle failures or incidents in third-party data or high-risk AI systems."* The Govern 6.x family's primary scope is third-party / vendor risk and contingency. Where the Crosswalk maps internal reporting cadence to Govern 6.1 or stakeholder communication to Govern 6.2, those mappings capture the third-party-reporting view of those controls; broader internal stakeholder communication aligns with the **Govern 5.x family** ("Processes are in place for robust engagement with relevant AI actors").
- **NIST AI RMF Govern 1.4 vs 1.5.** Govern 1.4 = "Risk management process and outcomes are established through transparent policies, procedures, and other controls." Govern 1.5 = "Ongoing monitoring and periodic review of the risk management process and its outcomes are planned." Effectiveness-evaluation framing aligns more precisely with Govern 1.5; the two subcategories together cover policy establishment + periodic review.

For the live, authoritative references, see [NIST AI 100-1 Playbook — Govern](https://airc.nist.gov/airmf-resources/playbook/govern/) and the [ISO/IEC 42001:2023 catalog](https://www.iso.org/standard/42001).
