# AI Incident Response Playbook Simulation

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This lesson covers AI incident management, including incident playbook design, severity classification, threshold-based incident detection, escalation workflows, and post-incident review processes. Students learn to build comprehensive incident response frameworks for safety-critical AI systems using both structured Excel templates and Python-based monitoring logic.

## File Structure

```
06_ai-incident-response-playbook-simulation/
├── demo/
│   └── incident_response_demo.xlsx      # Filled-in instructor reference
├── exercises/
│   ├── starter/
│   │   ├── incident_detection_starter.ipynb      # Notebook with TODO placeholders
│   │   ├── incident_response_starter.xlsx        # Student starting file (with hints)
│   │   └── transitai_monitoring.png              # Generated visualization (starter output)
│   └── solution/
│       ├── incident_detection_solution.ipynb      # Completed notebook
│       ├── incident_response_solution.xlsx        # Completed solution
│       └── transitai_monitoring.png               # Generated visualization (solution output)
└── README.md
```

## Demo

**Scenario: RoutePilot AI** — A Series A logistics startup (3 cities, 500 active drivers, ~50,000 deliveries/day) building an AI-powered route optimization platform for delivery drivers.

The instructor walks through the workbook live, filling in incident response playbooks and severity classifications. The demo covers 3 sheets:

1. **Incident Playbook** — Build response plans for 3 incident types: route bias against certain neighborhoods (Bias), route accuracy degradation (Performance), and driver location data exposure (Security). For each incident, define severity level, detection method, initial response, and resolution steps.
2. **Severity Classification** — Review a 4-tier severity framework (S1 Critical through S4 Low) with response time SLAs ranging from < 15 minutes to < 24 hours.

## Exercise

**Scenario: TransitAI** — An urban transit company (15 metro areas, 2M+ daily passengers, 10,000+ vehicles) operating AI-powered autonomous route optimization and passenger communication for safety-critical transit operations.

### Task

**Part 1 — Incident Response (Excel)**

Students complete five governance deliverables across 5 sheets:

1. **Incident Playbook** — Review the 10 pre-filled incident types across 6 categories (Bias, Misuse, Performance, Security, Safety, Compliance — including adversarial manipulation, training data poisoning, unauthorized access, model hallucination, offensive chatbot responses) end-to-end. The starter ships these as worked examples; students confirm severity / detection / initial response / investigation / resolution / communication / post-resolution chains read as an incident commander would use them, and refine rationale annotations where their team's context differs.
2. **Severity Classification** — Review the pre-filled 4-tier severity framework (S1–S4) with escalation requirements and communication scope for each level.
3. **Reporting Workflow** — Review the 10-step incident reporting workflow from Detection through Knowledge Base Update. All 10 steps are pre-filled; students confirm responsible roles, timelines, and deliverables hold for their team's actual on-call structure.
4. **Post-Incident Review** — Review the 9-element blameless post-incident review template (Timeline, Root Cause, Impact, Response Effectiveness, Lessons Learned, Preventive Measures, Action Items, Communication Effectiveness, Follow-up Schedule). All 9 elements are pre-filled; students adapt where their team's existing PIR template differs.

**Part 2 — Incident Detection (Notebook)**

Using 100 hours of simulated TransitAI monitoring data with 8 injected anomalies, students implement threshold-based incident detection:

1. **Implement Detection Logic** — Complete the `detect_incidents()` function that compares 6 system metrics (`model_accuracy`, `response_latency_ms`, `bias_score`, `error_rate`, `uptime_pct`, `content_safety_score`) against warning and critical thresholds, respecting the threshold direction (above/below).
2. **Implement Escalation Logic** — Complete the `determine_escalation()` function that routes incidents to appropriate teams based on severity (S1–S4) and metric type (e.g., security metrics escalate to CISO).
3. **Implement Response Recommendations** — Complete the `recommend_response()` function that suggests specific response actions based on the affected metric and severity level.
4. **Visualization** (pre-provided, run and review) — 6-panel monitoring dashboard (one panel per metric) showing metric values over time with warning/critical threshold lines and flagged incidents.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the regulatory anchors used in the TransitAI scenario.

- **Transit regulators — FTA, NHTSA, NTSB.** For US ground transportation, the primary first-line regulators differ by mode. The **Federal Transit Administration (FTA)** is the primary regulator for rail transit and bus systems and runs the **State Safety Oversight (SSO) program** under [49 CFR Part 674](https://www.ecfr.gov/current/title-49/subtitle-B/chapter-VI/part-674) — this is where mandated incident-notification timeframes (e.g., 2-hour rail-transit notification) live. The **National Highway Traffic Safety Administration (NHTSA)** is the primary regulator for highway autonomous-driving systems and runs the [Standing General Order 2021-01](https://www.nhtsa.gov/laws-regulations/standing-general-order-crash-reporting) for ADS / Level-2 crash reporting. The **National Transportation Safety Board (NTSB)** is an independent investigative body that conducts post-incident investigations and issues safety recommendations; it is typically the recipient of incident reports rather than the source of operating regulations. The lesson's "NTSB / FTA" framing covers transit specifically; for fully-autonomous highway deployments, NHTSA is the closer first-line regulator.
- **California breach notification.** The breach-notification statute is **Cal. Civ. Code §1798.82**, which predates and operates alongside the CCPA / CPRA. The CCPA itself (codified at Cal. Civ. Code §1798.100 et seq.) provides a [private right of action under §1798.150](https://oag.ca.gov/privacy/ccpa) for breaches of *unencrypted personal information* but the underlying notification obligation flows from §1798.82. References to "CCPA breach notification" in the materials should be read as covering both the §1798.82 notification obligation and the §1798.150 private right of action.
