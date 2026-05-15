# AI Security Metrics and Dashboarding

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This module teaches students to design portfolio-level AI security KRIs that derive from a real risk register (not a vendor catalog), implement them as small unit-testable Python functions (the seed of a production `kri_calculator.py`), and produce a leadership-ready 5-KRI dashboard. Students learn the difference between a metric and a KRI, why threshold design matters as much as the metric itself, and that a board dashboard is a communication artifact while a KRI is a Python function.

## File Structure

```
07_ai-security-metrics-and-dashboarding/
├── demo/
│   ├── kri_demo.xlsx                           # Filled-in instructor reference (Aurora refusal-rate KRI)
│   ├── kri_calculator_demo.ipynb               # End-to-end demo notebook (1 KRI walkthrough)
│   └── data/
│       └── refusal_log.csv                     # 30-day Aurora monitoring log (turns, refusal-flag, session-id, model-version)
├── exercises/
│   ├── starter/
│   │   ├── kri_definitions.xlsx                # Student starting file (UdaciBank 5-KRI portfolio)
│   │   ├── kri_calculator_starter.ipynb        # Notebook with TODO placeholders (2 KRIs to implement)
│   │   └── data/                               # Synthetic monitoring-log fixtures
│   │       ├── fraud_predictions.csv           # Exercise fixture for KRI #1 (subgroup FNR delta)
│   │       └── credit_drift_features.csv       # Exercise fixture for KRI #2 (drift score)
│   └── solution/
│       ├── kri_definitions.xlsx                # Completed solution with Reasoning: annotations
│       ├── kri_calculator_solution.ipynb       # Fully implemented notebook with passing tests
│       └── kri_dashboard.png                   # Generated 5-KRI dashboard (notebook output)
└── README.md
```

Workbook sheets — exercise (5): Scenario Brief, KRI Definitions, Portfolio Inventory, Risk Register Crosswalk, Dashboard Mockup. The demo workbook uses the same 5-sheet pattern but is scoped to a 3-model B2B SaaS portfolio so it stays distinct from the exercise's UdaciBank inventory.

## Demo

**Scenario: Aurora Assistant** — A B2B SaaS company runs an LLM-powered customer-support assistant (Aurora Assistant) plus two supporting models (`SupportRouter-v2` intent classifier and `ChurnSignal-v3` account-health predictor). The risk register has one row that motivates the demo: *"Anomalous refusal-rate spikes on the assistant indicate either policy drift or attempted misuse — both warrant investigation."*

The instructor walks through deriving one KRI from that single row: **refusal rate on Aurora Assistant**, thresholds (green ≤ 3%, amber 3–7%, red > 7%), daily rolling-24h cadence, escalation Platform Lead → AI Review Board at amber → CRO + AppSec at red. The Excel workbook captures the KRI definition, anchors it against the 3-model portfolio inventory, and crosswalks it back to the source risk row; the demo notebook then implements the KRI as a small pandas function that consumes a synthetic 30-day LLM monitoring log (`refusal_log.csv` — turns, refusal-flag, session-id, model-version) and returns `{value, status, owner, timestamp}` — the seed pattern for a production `kri_calculator.py`.

## Exercise

**Scenario: UdaciBank** — A digital-only fintech with 10 production AI models in flight (fraud detection, credit decisioning, customer support, marketing personalization, transaction categorization, etc.). The CISO needs a portfolio-level governance system: two production-grade KRI functions plus three design-spec KRIs ready for follow-up engineering, plus a one-page dashboard the AI review board will use monthly.

### Task

**Part 1 — KRI Definitions (Excel)**

1. **Define 5 KRIs at portfolio level** — subgroup FNR delta, drift score, **jailbreak-classifier hit rate (LLM customer-support assistant — GenAI-native KRI distinct from the demo's refusal-rate signal)**, vendor SLA breach rate, % of production models with a current threat model. Two are pre-filled with full definitions (input source, threshold, owner, escalation, cadence).
2. **Complete the remaining 3 KRI definitions** — for each, name the input source, the green / amber / red thresholds, the monitoring cadence, the named owner, the escalation path, and the board-facing one-sentence interpretation.

**Part 2 — Portfolio Inventory + Risk Register Crosswalk (Excel)**

1. **Read the Portfolio Inventory** — 10 production models with risk tier and current-state monitoring posture (pre-filled).
2. **Crosswalk each KRI to the risk-register row(s) it derives from** — every KRI must trace back to a named risk. Two crosswalks are pre-filled; complete the remaining 3.

**Part 3 — Dashboard Mockup (Excel)**

1. **Lay out the dashboard** — for each of the 5 KRIs, provide a current value (placeholder for the 3 design-spec KRIs), a status band, the threshold reference, and the one-sentence narrative.

**Part 4 — KRI Calculator (Notebook)**

1. **Implement `compute_subgroup_fnr_delta()`** — takes a predictions+labels+subgroup DataFrame, returns `{value, status, owner, timestamp}`. Use the provided `fraud_predictions.csv` fixture.
2. **Implement `compute_drift_score()`** — takes a baseline-feature DataFrame and a current-feature DataFrame, returns `{value, status, owner, timestamp}` using a population-stability-index-style metric. Use the provided `credit_drift_features.csv` fixture.
3. **Run the provided unit tests** — both calculators must match the reference outputs.
4. **Render the 5-KRI dashboard** — bar chart of current values + threshold lines + status colors. Save as `kri_dashboard.png`.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |
