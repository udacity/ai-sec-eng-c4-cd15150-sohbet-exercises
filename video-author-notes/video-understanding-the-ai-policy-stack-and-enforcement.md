# Video: Understanding the AI Policy Stack and Enforcement
*Module 5.1 | Topic: Understanding the AI Policy Stack and Enforcement*

---

## Opening Hook

> *"Your company writes an AI Acceptable Use Policy. It's a good document. It bans pasting customer data into ChatGPT, it sets sanctioned tools, it has a nice tone. Six months later, an engineer pastes a snippet of customer financial data into a public LLM to debug a regex. The policy is the same policy. The engineer read it on day one. So why didn't it work? Because a policy without a binding control behind it is a wish, and wishes don't show up in your DLP logs. And here's the second move I want to make: even a perfect AUP is one document in a four-document stack. If you don't see the stack, you write the same AUP four times and end up with a contradicting set of rules nobody can navigate."*

The conceptual job here is to install two ideas: (1) AI policy is not a single document but a *stack* of four documents with distinct audiences and binding mechanisms, and (2) the gap between "policy on paper" and "policy that works" is filled by enforcement and exception handling — which is where most programs quietly fail.

---

## Key Discussion Points

1. **Why a single AUP is not enough.** An Acceptable Use Policy aimed at employees governs the consumer-facing surface — pasting data into public GenAI, using sanctioned vs unsanctioned tools, prompts containing sensitive content. It does *not* govern ML teams shipping fine-tuned models, it does not govern what training data is permitted to be used, and it does not govern AI features purchased from vendors. Each of those audiences needs its own document.

2. **The four-document AI policy stack.**
   - **AI Acceptable Use Policy (AUP)** — governs *employee* use of GenAI. Audience: everyone with a corporate account. Binding mechanism: DLP rules, prompt firewall classifiers, browser controls, SSO admin disabling unsanctioned tools.
   - **AI Development Policy** — governs *engineering and ML teams* building or fine-tuning models. Audience: model developers, MLOps, data science. Binding mechanism: CI/CD gates, model-registry checks, mandatory model-card requirements before promotion to production.
   - **AI Data Handling Policy** — governs *what data is permitted to be used* for training, fine-tuning, retrieval-augmented generation, evaluation. Audience: data engineering, ML, legal. Binding mechanism: data-classification controls, lineage tracking, training-data inventory gates.
   - **AI Procurement / Vendor Policy** — governs *AI products and AI features purchased from vendors*. Audience: procurement, security, legal, business owners. Binding mechanism: vendor onboarding gate, AI-specific contractual riders, vendor assessment scorecards. Connects directly to Module 8.

3. **Distinct audience, distinct binding mechanism, distinct authority for exceptions.** That's the discipline of the stack. Each document answers: who reads this, what control technically enforces it, and who can grant an exception. If two documents have the same answers, you have one document with the wrong title.

4. **Out-of-scope hand-offs.** This is the move most policy stacks botch. Every policy must explicitly name what is *not* in scope and which sister policy covers it. "Use of vendor-purchased AI features is governed by the AI Procurement Policy." "Training-data sourcing is governed by the AI Data Handling Policy." Without these hand-offs, the policies *overlap and contradict*. Students should leave this module knowing that the hand-off paragraphs are the seams that hold the stack together.

5. **Policy enforcement mechanisms — three flavors.**
   - **Technical controls (preventive).** DLP that blocks the request before it leaves the perimeter. Browser controls. SSO admin disabling AI features. CI/CD gate that blocks the merge.
   - **Technical controls (detective).** Prompt-firewall classifier that flags after the fact. Model-registry audit that flags ungated promotions. Log review.
   - **Process controls.** Training, attestation, manager attestation on hire, periodic reattestation, mandatory review at promotion. Weakest of the three; the one programs over-rely on.
   
   Caveat to land precisely: many "detective" controls in real life are preventive controls with detective signaling (DLP blocks the request *and* logs it). The strict NIST 800-53 / ISO 27001 taxonomy distinguishes; in practice teams use "detective control" as shorthand for "binding technical control." Be honest about that.

6. **Every prohibited use needs a binding control.** This is the single most important insight in the module. A prohibition that does not have a corresponding detective or preventive control is *aspiration*. The Control Map is the artifact that forces this discipline — for every prohibited use, what catches it? If the answer is "we trust the employee handbook" the prohibition is unenforced.

7. **Exception handling — the part programs skip.** Every policy generates exception requests. The question is whether your policy has a *named procedure* for them: who can request, who triages, who has risk-acceptance authority, what artifact records the exception, what expiry date carries forward, how the exception is reviewed at renewal. Most policies have no procedure, so exceptions become ad hoc emails — and then become tribal knowledge — and then become the policy.

8. **Risk acceptance as a first-class concept.** Some exceptions will be denied. Some will be granted with controls. Some will be granted as pure risk acceptance — meaning the named risk owner signs that they are aware of the residual risk and accepting it. Risk acceptance is *not* "we'll just not enforce this." It's a documented, named acceptance with an owner, a scope, and a review cadence.

9. **The common failure modes — the patterns I want students to recognize.**
   - **The policy exists but no one knows about it.** Distribution gap.
   - **The policy exists but has no binding control.** Enforcement gap.
   - **The policy exists, has a control, but no exception procedure — so every real-world need becomes a one-off email.** Procedure gap.
   - **Exceptions accumulate with no review, eventually flipping the policy meaning entirely.** Drift.
   - **Multiple overlapping policies contradict each other.** Stack gap.

10. **The shape of an enforceable AUP.** Purpose, Scope (with explicit boundary statement naming the other three policies in the stack), Definitions, Roles and Responsibilities (AUP owner, enforcement owner, exception authority), Prohibited Uses (with tiered consequences — 1st / 2nd / 3rd offense — and the binding control for each), Acceptable Uses (with verification guidance), Exception Procedure (with named roles, timelines, artifacts), Control Map (linking every prohibition to a detective control), and a Policy Stack Reference.

11. **GenAI-specific prohibitions worth naming.** Pasting sensitive data into public LLMs. Submitting customer PII or financial data into prompts. Submitting material non-public information (MNPI) into prompts. Using AI coding assistants on regulated codebases without sanctioned tooling. Treating AI output as the *sole basis* for client-affecting decisions. AI-feature use embedded in third-party SaaS tools that haven't been assessed.

12. **The regulatory anchors that quietly back these prohibitions.** GDPR for personal data in prompts. SEC Reg S-P / GLBA for financial customer data. SOX for material financial information. Title VII / ECOA for employment and credit decisions. HIPAA for protected health information. MNPI under SEC Rule 10b-5 for insider-trading exposure on submitted text. The prohibitions are not arbitrary — they're derivatives of existing law.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| UdaciCorp's shadow GenAI sprawl (mirrors demo) | 2,000-person SaaS company: employees pasting customer data into public LLMs, ML teams shipping fine-tuned models without review, vendors selling AI add-ons nobody has assessed. Walk through which document in the stack would have caught each problem and how the four documents' enforcement mechanisms differ. | Walkthrough — anchor example |
| Tracing one incident through the stack | A shadow-GenAI incident: an engineer uses an unsanctioned LLM to debug, pastes a snippet of MNPI into the prompt, the LLM logs the prompt, the prompt becomes discoverable in litigation. Which policy would have caught it? AUP. What control would have stopped it? Prompt firewall classifier blocking MNPI patterns. Where would the exception procedure have routed a legitimate need? Through the AUP exception authority, with risk acceptance documented. | Walkthrough — second anchor, makes the stack mechanics concrete |
| UdaciFinancial's investment-management AUP (mirrors exercise) | 5,000-person investment-management firm; AUP must cover employee public GenAI, developer AI-coding-assistant use on regulated codebases, prompt content involving MNPI or customer financial data. Note that "GLBA" is shorthand for GLBA + SEC Reg S-P implementation for SEC-registered investment advisers. | Walkthrough — third anchor |
| The exception that became the policy | An exception granted in month 3 to allow a sales team to use an unsanctioned summarization tool, "just for a quarter." No expiry tracking. Twelve months later, the entire sales org is using it; the AUP has been silently overwritten by accreted exceptions. Use to motivate the expiry and review cadence in the exception procedure. | Brief mention |
| The "we trust the handbook" prohibition | A prohibition on pasting customer data into public LLMs with no DLP rule, no prompt firewall, no SSO control. Six months later the security team has no idea whether anyone is complying. | Brief mention |
| The detective vs preventive control nuance | Walk through one prohibition mapped to a control that is preventive (blocks) and detective (logs). Use to land the taxonomy caveat honestly. | Brief mention |

---

## What NOT to Cover

- **Drafting the actual policy text section by section** — implementation module's deliverable.
- **Writing the consequence ladder for a specific prohibition** — implementation exercise (rows 3–5 of Prohibited Uses).
- **Mapping AUP rules to specific DLP product configurations** — too vendor-specific. Stay at the conceptual control type level.
- **EU AI Act Article 50 disclosure requirements** — Module 4.
- **Third-party AI vendor risk assessment scoring** — Module 8.
- **Incident response when a policy violation has occurred** — Module 6.
- **Specific GDPR articles in detail** — Module 11. Touch lightly here as anchoring law only.

---

## Additional Notes

- **Analogies.** The four-document stack is like the difference between an HR handbook, an engineering standards doc, a data classification policy, and a vendor security questionnaire. They overlap, they reference each other, but they have distinct audiences and binding controls. Try to use one of those four documents for all four jobs and you get the same mess that single-AUP organizations have today. For enforcement: a policy without a control is like a "Wet Floor" sign on a floor that doesn't get cleaned — the sign is the *appearance* of safety, not the substance of it.
- **Terminology.** "AUP" (Acceptable Use Policy), "AI Development Policy," "AI Data Handling Policy," "AI Procurement Policy" — use these exact names, capitalized. "Prohibited use" vs "acceptable use" — both technical terms, don't paraphrase. "Exception" specifically (not "waiver" or "carve-out") — exception is the standard governance term.
- **Avoid:** treating the AUP as the whole stack. Avoid suggesting policy is sufficient without controls. Avoid romanticizing process controls (training, attestation) as primary enforcement — they're necessary but weak. Avoid implying that exception procedures are bureaucratic overhead — they're the *opposite*; they're how you keep the policy enforceable in the face of real business need.
- **A grounded line worth seeding:** "Every mature program I've worked with has the same story: the AUP was easy to write. The AUP was hard to *enforce*. The thing that turned policy into practice was the Control Map and the exception procedure — and both of those got skipped on the first draft."
- **Another:** "If you can't tell me, for any line of your AUP, which technical control catches a violation, that line is decoration."
- **A reflective beat:** "Look at your current AI AUP. For each prohibited use, what's the detective control? If you can't name one in under thirty seconds, you don't have a policy — you have a memo." Place this around the enforcement section.
- **A throwaway humanity beat:** "The moment that taught me this lesson was an exception request for an unsanctioned summarization tool, granted for a quarter, that I forgot to put an expiry on. Two years later, half the org was using it. That's how policy drift happens — one forgotten expiry at a time."
- **Connection to the implementation module.** Students will draft an AI AUP for UdaciFinancial (5,000-person investment-management firm). They'll complete Purpose / Scope / Definitions with the explicit boundary to the other three policies, fill in three more rows of Prohibited Uses with consequence ladders, three Acceptable Uses with verification guidance, three remaining steps of the Exception Procedure, and complete the Control Map linking every prohibition to a detective control. After this conceptual module they should be able to predict the shape of the deliverable — and *why* each section is in it.

---
