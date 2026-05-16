# AI Policy Architecture

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students how to design one layer of an organization's AI policy stack — the AI Acceptable Use Policy (AUP) — with prohibited uses, acceptable uses, an exception procedure, and a control mapping that ties every prohibition to a detective control. The module frames the AUP as one document in a four-document stack (AUP, AI development policy, AI data-handling policy, AI procurement policy) and trains students to hand off out-of-scope cases cleanly to the other three.

## File Structure

```
05_ai-policy-architecture/
├── demo/
│   └── ai_policy_demo.xlsx                     # Filled-in instructor reference (full policy stack walkthrough)
├── exercises/
│   ├── starter/
│   │   └── ai_aup.xlsx                         # Student starting file (UdaciFinancial AUP, partial fill)
│   └── solution/
│       └── ai_aup.xlsx                         # Completed solution with Reasoning: annotations
└── README.md
```

Each workbook contains seven sheets: Scenario Brief, AUP Body, Prohibited Uses, Acceptable Uses, Exception Procedure, Control Map, Policy Stack Reference.

## Demo

**Scenario: UdaciCorp** — A 2,000-person enterprise (SaaS, mixed industry) with growing shadow GenAI use: employees pasting customer data into public LLMs, ML teams shipping fine-tuned models without review, vendors selling AI add-ons that nobody has assessed. Security and Legal need a complete AI policy architecture within 30 days.

The instructor walks the full AI policy stack live — the four documents (AUP, AI development policy, AI data-handling policy, AI procurement policy), each with its distinct audience and binding enforcement mechanism (DLP for AUP, CI/CD gates for the development policy, data-classification controls for the data-handling policy, vendor onboarding for the procurement policy). The walkthrough then traces a single shadow-GenAI incident through the stack to show which policy would have caught it, and where exception handling and risk acceptance plug into each document. The Control Map sheet anchors every prohibited use to a specific detective control, and the Policy Stack Reference sheet lays out the four documents side-by-side so students see how out-of-scope cases hand off across the stack.

## Exercise

**Scenario: UdaciFinancial** — A 5,000-person investment-management firm with an AI policy stack outline approved by the AI review board. You have been assigned the AUP layer. The AUP must address (a) employee use of public GenAI for work, (b) developer use of AI coding assistants on regulated codebases, and (c) prompt content involving customer financial data or material non-public information (MNPI). It must hand off cleanly to the other three policies in the stack.

### Task

**Part 1 — AUP Body**

1. **Purpose, Scope, Definitions** — Write the three opening sections, including an explicit boundary statement that names the other three policies in the stack.
2. **Roles and Responsibilities** — Name the AUP owner, the enforcement owner, and the exception-approval authority.

**Part 2 — Prohibited Uses**

1. **Complete the prohibited-use table** — Two prohibitions are pre-filled as worked examples (rows 1–2). Three more rows are scaffolded by category — AI-coding-assistant misuse on regulated codebases, embedded-AI-feature misuse in third-party tools, and AI-as-sole-basis for client-affecting decisions — and you supply the rationale + tiered consequence ladder (1st / 2nd / 3rd offense) for each.

**Part 3 — Acceptable Uses**

1. **List acceptable uses with verification guidance** — Two acceptable uses are pre-filled. Three more rows are scaffolded by use category — sanctioned-LLM retrieval over public corpus, AI-features-inside-sanctioned-tools, and sanctioned-LLM for internal content drafting — and you supply the verification step that confirms each use is in-policy.

**Part 4 — Exception Procedure**

1. **Complete the exception workflow** — Define each step (request, triage, risk-acceptance, approval, expiry) with named role, timeline, and artifact. Two steps are pre-filled.

**Part 5 — Control Map**

1. **Map each prohibition to a detective control** — For every prohibition in the Prohibited Uses sheet, name the detective control that catches it (DLP rule, prompt-firewall classifier, code-scanner check, model-registry gate, etc.). Two mappings are pre-filled.

**Part 6 — Policy Stack Reference (read-only)**

1. **Read the four-document stack overview** — Confirm your AUP cross-references the other three policies correctly for out-of-scope cases.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the regulatory anchors and control taxonomy used in this lesson.

- **Detective vs preventive controls.** Several entries on the Control Map sheet describe controls that operate primarily as **preventive** (blocking) — DLP that blocks the request before it leaves the perimeter, a CI/CD gate that blocks merge when policy compliance is missing, an SSO admin disabling AI features. In a strict NIST SP 800-53 / ISO 27001 control-type taxonomy these are *preventive controls with detective signaling* rather than purely detective controls. The Control Map column header is kept as "Detective Control" for consistency with how the policy team frames the binding-control linkage; the underlying point is that every prohibition needs a technical control behind it (whether detective, preventive, or both). Where the lesson uses "detective control" as shorthand for "binding technical control," that's the working definition.
- **GLBA vs SEC Reg S-P for investment-management firms.** GLBA (Gramm-Leach-Bliley) is the federal statute governing safeguarding of customer financial information. For SEC-registered investment advisers and broker-dealers, the operative implementation is **SEC Regulation S-P** (17 CFR Part 248), which the SEC modernized in May 2024 to add a 30-day breach-notification requirement. References in the lesson to "GLBA" for the UdaciFinancial scenario should be read as covering both the underlying GLBA obligation and the SEC Reg S-P implementation that applies to investment-management firms specifically. See [SEC Regulation S-P](https://www.sec.gov/rules-regulations/2024/06/s7-05-23).
- **MNPI under Rule 10b-5.** Material non-public information is the central concept under SEC Rule 10b-5 / 10b5-1 enforcement of insider trading under the Securities Exchange Act of 1934. The prohibition on submitting MNPI into AI prompts is a derivative of the broader insider-trading framework, not a standalone AI rule. See [17 CFR 240.10b5-1](https://www.law.cornell.edu/cfr/text/17/240.10b5-1).
- **GDPR DPO role (Articles 37-39).** The Data Protection Officer is a defined role under [GDPR Articles 37-39](https://gdpr-info.eu/art-37-gdpr/). DPO designation is mandatory for organizations engaging in large-scale processing of special-category data or systematic monitoring at scale; a 5,000-person investment-management firm operating in the EU and processing customer financial data would commonly designate a DPO. The DPO is an internal compliance role rather than an enforcement recipient — DPO involvement on a policy violation is internal-process best practice, not a GDPR-mandated escalation.
