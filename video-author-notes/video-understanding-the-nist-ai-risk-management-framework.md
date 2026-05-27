# Video: Understanding the NIST AI Risk Management Framework
*Module 2.1 | Topic: Understanding the NIST AI Risk Management Framework*

---

## Opening Hook

> *"Your company already has an enterprise risk register. You already have ISO 27001 or SOC 2. You already file SOX controls. So when leadership asks, 'why do we need yet another framework just because we shipped a model?' — you should have an answer that takes about ninety seconds. If you don't, the AI risk program never gets funded. And later, when you walk into the AI review board with a beautiful NIST AI RMF risk register, the chief risk officer will look at it and say, 'great — now show me how this lines up with our SOC 2, ISO 27001, SOX, and the ISO 42001 certification we're chasing.' If you can't draw that map on a whiteboard in five minutes, the program loses oxygen all over again."*

I want this module to install three things: (1) why an AI-specific framework is needed at all, (2) what the four NIST functions actually are as *modes of work*, and (3) how this framework integrates with everything else the organization is already doing. Without all three, students leave with framework trivia rather than the ability to operate.

---

## Key Discussion Points

1. **Traditional risk frameworks treat software as deterministic. AI isn't.** ISO 27001, NIST SP 800-53, COBIT — all of these assume that if you specify a control, the system behaves consistently against it. ML systems shift behavior with data, time, and adversarial input. The notion of a "version" of the control surface stops being stable. That alone breaks assumptions a lot of GRC programs are built on.

2. **AI failure modes don't map cleanly onto the CIA triad.** Confidentiality, Integrity, Availability — works fine for a database. A model that develops a fairness drift is not failing on CIA. It's failing on something like "decision validity" or "demographic robustness." These are not in the classic taxonomy. NIST AI RMF gives you a richer taxonomy for things that go wrong with ML.

3. **The AI lifecycle is longer and weirder than software.** Traditional risk management owns systems from procurement to decommissioning. AI adds: training-data sourcing, model retraining, monitoring for drift, fine-tuning, prompt engineering, vendor model version changes you didn't approve. Each of those is a risk event traditional frameworks don't have a row for.

4. **AI introduces *new categories* of stakeholders.** Affected persons (loan applicants, defendants, patients), upstream data subjects, the public. Traditional frameworks track risk to the organization. AI frameworks have to track risk *from* the organization to people who aren't customers. This is where the moral and legal weight comes from, and where most enterprise risk programs are quietly underbuilt.

5. **The four core functions — Govern, Map, Measure, Manage — and what they *actually* do.**
   - **Govern is the control plane, not a documentation pile.** Policies, decision rights, accountability, escalation, what counts as acceptable risk. It's the operating system the other three run on. Common failure: treating Govern as "we wrote a policy" rather than "we operationalized the policy with named owners and review cadences."
   - **Map is scope-setting with teeth.** What are we actually building, who does it affect, in what context, with what data, against what objectives, with what assumptions? Map captures the model purpose, intended population, deployment context, data lineage, and the assumptions the system makes about its environment. Each assumption is a risk.
   - **Measure is how you find out whether the system is actually behaving.** Technical metrics, fairness metrics, security metrics, impact on affected populations, monitoring coverage. Measure is not just *picking* metrics — it's *justifying* them. Why this metric? What does it tell you? What does it miss?
   - **Manage is the action loop, and the function most programs underinvest in.** Prioritize, mitigate, accept, transfer, monitor, respond. Manage turns Measure outputs into actual decisions: launch, don't launch, add controls, retrain, deprecate. A risk register full of "monitor" entries with no threshold, no owner, and no cadence is a Measure function pretending to be a Manage function.

6. **The four functions are not sequential.** Critical. They run *concurrently* with feedback loops. A Measure finding triggers a Manage action triggers a Govern policy update triggers a re-Map of scope. The Venn diagram has overlap on purpose.

7. **Categories, subcategories, and the Playbook.** Each function has categories (e.g., Govern 1, Govern 2) and subcategories (Govern 1.1, etc.). Subcategories are the unit of mapping work. The NIST AI RMF Playbook gives example actions per subcategory. Don't memorize them. Know they're the operational rows when you do an actual mapping.

8. **Profiles — what they are, why they matter.** A "Profile" is the NIST term for a tailored application of the framework to a specific use case or industry. NIST AI 600-1 is the Generative AI Profile (2024) — students will see it referenced often. Profiles let you scope the framework to what's relevant.

9. **The framework landscape, briefly.** NIST AI RMF (US, voluntary, operational), ISO/IEC 42001 (international, certifiable management system, December 2023), the EU AI Act (regulatory, mandatory in scope), ISO 31000 (general risk management spine). They are *complementary*. Most mature programs use NIST AI RMF as the *operational* framework and map outputs to ISO 42001 for certification and to the EU AI Act for legal compliance.

10. **The "Govern" function maps to ISO 42001 cleanest.** Both are about policies, roles, accountability, and management commitment. ISO 42001 Annex A controls A.2 (Policy), A.3 (Organization), A.4 (Resources), A.9 (Use of AI systems) map almost directly to NIST AI RMF Govern subcategories. The mappings get fuzzier in Map / Measure / Manage. Real mapping work is a Venn diagram, not a one-to-one table.

11. **The enterprise risk register hand-off.** AI risks need to *roll up* into the master enterprise risk register, not live in an orphan spreadsheet. The practical move: tag each AI risk register row with (a) its NIST AI RMF subcategory, (b) its ISO 42001 control reference, and (c) its enterprise risk category. That triple tag makes rollup possible. SOC 2, ISO 27001, NIST SP 800-53 cover AI risks that overlap with traditional security; the AI-specific risks (fairness, robustness, drift, hallucination, model extraction) have no clean home in pre-AI security frameworks and need the AI register as a complementary layer.

12. **Common implementation pitfalls.**
    - Trying to bolt AI RMF onto the existing register without rethinking categories.
    - Treating Govern as documentation rather than as the control plane.
    - Skipping Map because it feels like context-gathering when it's actually scope-setting.
    - Confusing Measure (how do we know?) with Manage (what do we do about it?).
    - Letting "we mapped it" substitute for "we operationalized it."

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| CareBot Health / DiagnosAI near-miss (mirrors demo) | A hospital clinical decision-support system has a near-miss drug-interaction event. Walk through which function would have caught what. Govern: was there a clinical-AI policy? Map: was the deployment context understood (which patient populations, conditions)? Measure: were the right metrics tracked? Manage: was there a response playbook? This shows the functions interacting on a real incident. | Deep dive — anchor example |
| FinGuard AI fraud detection with socioeconomic bias (mirrors exercise) | A "working" model passes the traditional security review (good uptime, low latency, clean data flows) and still introduces material risk — disproportionate flagging in lower-income ZIP codes. AI RMF would catch this; SOC 2 wouldn't. Use to motivate the framework. | Walkthrough |
| One AI risk row, four tags | Take a row like "Model drift causing accuracy degradation on protected subgroup." Tag it: AI RMF Measure 2.3, ISO/IEC 42001 Annex A.6.2 (AI system lifecycle — operation and monitoring), enterprise risk category "Operational/Model Risk," SOC 2 CC8.1 (change management). Walk through why all four tags belong. The exact sub-control ID under A.6.2 should be verified against the published 42001 standard at write time. | Walkthrough — anchor for the integration point |
| The Manage trap | A risk register row that says "monitor for drift" with no metric, no threshold, no owner, no escalation. Not Manage. Avoiding Manage. | Brief mention |
| The certification trap | A startup pursues ISO 42001 certification with no NIST AI RMF substrate underneath. Passes audit on paper. Six months later their incidents don't get caught because the management system has no operational risk register feeding it. Motivates doing both. | Brief mention |
| The "human-rights impact" row with no SOC 2 home | "Potential disparate impact on credit-disadvantaged populations" maps cleanly to AI RMF Map and Manage, lands in ISO/IEC 42001 Annex A.5 (impact assessment on individuals and groups), has no natural home in SOC 2 or NIST SP 800-53. Shows where the AI-specific frameworks earn their keep. | Brief mention |

---

## What NOT to Cover

- **EU AI Act risk tiers, Article 11 documentation, conformity assessment** — Module 4. Reference once as "the legal layer that sits beside, not on top of, the NIST framework."
- **MITRE ATLAS threat modeling specifics** — Module 3. Mention only as "an adversary-tactics catalog that plugs into the Map and Manage functions."
- **The mechanics of building a risk register with impact × likelihood scoring, 4-band level cutoffs (Critical ≥ 15, High 10–14, etc.)** — implementation module. The scoring choice is one operationalization; NIST is intentionally agnostic.
- **NIST AI 600-1 GenAI Profile detail** — flag as a real resource; don't enumerate.
- **Risk-visualization mechanics (heat maps, executive summary tables)** — implementation module's notebook.

---

## Additional Notes

- **Analogies.** For the function quartet: Govern is the constitution. Map is the survey of the territory. Measure is the instruments on the dashboard. Manage is the driver. Without the constitution, no rule of law. Without the survey, you don't know where you are. Without instruments, you can't tell what's happening. Without a driver, the car doesn't go anywhere. For the framework landscape: NIST AI RMF, ISO 42001, ISO 31000, SOC 2, EU AI Act are *projections* of the same underlying risk territory onto different surfaces. Some projections are sharper on certain features. None of them is the territory.
- **Terminology.** Use the NIST verbs exactly: Govern, Map, Measure, Manage. Capitalize when referring to the function. Don't call them "stages" or "phases" — NIST is explicit they're not sequential. Use "complementary frameworks," "crosswalk," "rollup," not "competing standards."
- **Avoid:** suggesting ISO 42001 certification is required (it isn't — it's increasingly *expected* by enterprise buyers but not mandated). Avoid suggesting NIST AI RMF is mandatory in the US (voluntary). Avoid one-to-one mapping claims between AI RMF and ISO 42001 — the mappings are many-to-many.
- **A grounded line worth seeding:** "In every mature AI program I've seen, the same risk row gets read three times by three different audiences — the ML team via NIST AI RMF, the audit team via ISO 42001, the board via the enterprise risk register. The work is to make sure the *same row* satisfies all three readings. The crosswalk is the trick that lets that happen."
- **A throwaway humanity beat:** "The first time I tried to fit a fraud model into our existing risk register, the register had a column for 'system criticality' and another for 'data classification' and nowhere to put 'this model might drift in six weeks and we won't notice.' That's when you know you need a different tool."
- **A reflective question to drop somewhere near the end:** "Look at your team's last incident. Which of the four functions caught it? Which one *should* have caught it earlier? That gap is your roadmap."
- **A framing line worth seeding:** "Most programs talk about 'AI governance.' That's just one of the four functions. If you only build Govern, you have policy without practice. If you only build Manage, you have firefighting without strategy."
- **Connection to the implementation module.** Students will build an 18-row risk register covering all four functions for FinGuard AI — 15 base risks pre-filled, three GenAI-specific rows they author (hallucinated explanations, prompt-injection vulnerabilities, training-data poisoning). They'll then visualize with a heat map, grouped bar chart by category, and pie chart of risk levels, and produce an executive summary. After this module they should be able to predict the register's shape — rows tagged Govern, Map, Measure, Manage; categories Technical/Ethical/Legal/Operational; scoring as Impact × Likelihood with the four-band cutoffs.

---
