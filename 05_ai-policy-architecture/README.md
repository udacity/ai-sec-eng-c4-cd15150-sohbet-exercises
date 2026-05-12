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

1. **Complete the prohibited-use table** — Two prohibitions are pre-filled as worked examples. Add three more (customer financial data in prompts, MNPI in prompts, model-file exfiltration, unsanctioned models in production code). For each, specify the rationale and the binding consequence.

**Part 3 — Acceptable Uses**

1. **List acceptable uses with verification guidance** — Two acceptable uses are pre-filled. Add three more, each with the verification step that confirms the use is in-policy.

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
