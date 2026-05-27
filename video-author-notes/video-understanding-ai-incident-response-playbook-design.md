# Video: Understanding AI Incident Response Playbook Design
*Module 6.1 | Topic: Understanding AI Incident Response Playbook Design*

---

## Opening Hook

> *"Three a.m. The on-call engineer's phone goes off. The accuracy of a model that decides whether ambulances reroute around traffic just dropped seven points in twenty minutes. There's no IP address to block, no service to restart, no familiar runbook. The engineer has thirty minutes to figure out what's happening before the next dispatch cycle. What playbook does she open? If the answer is 'we'll figure it out,' your AI incident response posture is the same as your security posture was in 2002 — improvised. The job of this module is to install what the playbook *should* be, before you need it at 3 a.m."*

The conceptual job here is to make AI incidents feel structurally different from classical security incidents — three archetypes instead of one, severity that's defined by impact on affected populations rather than CIA loss, and a playbook structure that an incident commander can actually use in the first hour.

---

## Key Discussion Points

1. **The three AI incident archetypes — what they look like in production.**
   - **Bias incidents** — the model is making systematically worse decisions for a protected subgroup. May be a sudden drift, may be a long-running pattern that finally got noticed. Detection: subgroup-metric monitoring, complaint volume, fairness-metric breach. Examples: a hiring screen suddenly down-ranks female applicants; a fraud detector starts flagging transactions from certain ZIP codes; a chatbot becomes hostile to users in a specific dialect.
   - **Performance incidents** — the model is degrading on its core task. Accuracy drops, latency spikes, error rates climb, drift exceeds threshold. Detection: KPI monitoring, drift detection. Examples: a route-optimization model loses accuracy when winter weather changes traffic patterns; a recommender's relevance collapses after a backend feature store schema change; a classifier's precision drops because the labeled-data pipeline broke silently.
   - **Security incidents** — adversarial manipulation, exfiltration, unauthorized access, model theft, training-data poisoning, prompt injection. Detection: ATLAS-anchored monitoring, anomalous query patterns, content-safety classifiers. Examples: a chatbot is jailbroken into issuing unauthorized refunds; an adversary exfiltrates training-data membership through repeated inference queries; a vendor model gets quietly updated and starts behaving differently.

2. **Why this taxonomy matters operationally.** Each archetype has different *detection channels*, different *initial responders*, different *escalation paths*, and different *resolution playbooks*. A bias incident escalates to the AI Risk Officer and Legal; a security incident escalates to CISO and SecOps; a performance incident escalates to the ML platform team and product. A single "AI incident" playbook that doesn't differentiate by archetype will route everything through the same on-call person — and that on-call person can't possibly own all three.

3. **Severity classification — design, not borrow.** Classical security severity (S1–S4) is usually defined by CIA loss and blast radius. AI severity has to capture *additional* dimensions: scope of affected population, irreversibility of decisions made, regulatory disclosure obligations triggered, harm to specific individuals or groups. The standard shape:
   - **S1 Critical** — immediate, severe, and broad harm. Safety-critical malfunction. Regulatory reporting obligations triggered. Response time SLA: < 15 minutes to acknowledgment, full incident commander engaged.
   - **S2 High** — material harm or risk to a meaningful population. Response SLA: < 1 hour.
   - **S3 Medium** — measurable harm or risk to a limited population, or material drift. Response SLA: < 4 hours.
   - **S4 Low** — known issue, contained, monitored. Response SLA: < 24 hours.

4. **Response-time SLAs are not aspirational.** They are *contracts* with the incident commander, the executive team, and the regulator. The 15-minute SLA on S1 is what determines whether your engineering org can actually respond when a safety-critical AI system goes wrong. If your S1 SLA is theoretical, downgrade the severity definition or upgrade the on-call posture.

5. **The same playbook skeleton scales from Series A to enterprise.** The skeleton — detection method, initial response, investigation, resolution steps, communication, post-resolution actions — is the same whether you're 50 people or 50,000. What scales is the *headcount and rigor* in each cell. Series A: incident commander is the CTO, communication is a Slack channel, post-incident review is an hour of conversation. Enterprise: incident commander is a dedicated role, communication is a multi-tier comms plan, post-incident review is a structured nine-element artifact. Same playbook, different fill.

6. **The playbook as a *contract* an incident commander can read at 3 a.m.** One playbook entry per (incident type, severity). For each entry: how the incident is detected, the initial response in the first 15 minutes, the investigation steps, the resolution steps, the communication plan, the post-resolution actions. The incident commander should be able to open the playbook on a phone and execute it without scrolling for forty minutes.

7. **The reporting workflow.** From detection through knowledge-base update, what are the standard steps? Typically a ten-step shape: detect → classify severity → notify on-call → engage IC → investigate → contain → resolve → notify stakeholders → blameless post-incident review → knowledge base update. The last two are the steps everyone skips. They're the steps that turn an incident into organizational learning.

8. **Blameless post-incident review — the nine elements.** Timeline, root cause, impact, response effectiveness, lessons learned, preventive measures, action items, communication effectiveness, follow-up schedule. The word *blameless* is doing real work — the goal is system improvement, not accountability theater. If the PIR culture punishes the engineer who took the call, you'll have nobody on call next quarter.

9. **The handoff to monitoring and detection logic.** Playbooks live or die by whether the detection pipeline can actually surface an incident in time. Threshold-based detection on key metrics (accuracy, latency, bias score, error rate, content-safety score, uptime) with warning and critical thresholds, threshold direction (above vs below), and an escalation router that picks the right team based on severity and metric type. Setting up the *conceptual* point here so the implementation module's detection notebook lands cleanly.

10. **Regulatory anchors that determine incident SLAs.**
    - **EU AI Act Article 73** — 15-day default, 2 days for widespread infringement, 10 days for incidents involving death.
    - **FTA / NHTSA / NTSB** for transit — FTA's State Safety Oversight under 49 CFR Part 674 sets mandated rail-transit incident-notification timeframes (e.g., 2-hour rail transit notification). NHTSA's Standing General Order 2021-01 governs ADS / Level-2 autonomous crash reporting.
    - **California breach notification** — Cal. Civ. Code §1798.82, with CCPA §1798.150 providing a private right of action for unencrypted-PII breaches.
    - **GDPR Article 33** — 72-hour notification to the supervisory authority for personal-data breaches.
    - **HIPAA breach notification rule** (45 CFR §§ 164.400–414) — notify affected individuals without unreasonable delay and no later than 60 days from discovery; HHS notification is contemporaneous for breaches affecting 500+ individuals and annual for smaller breaches.
    - **Sector regulators** add more layers (SEC, FDA, HHS, financial regulators).
    
    These deadlines shape your severity SLAs. If you have a regulator that requires 2-hour notification, your S1 SLA needs to be measured in minutes, not hours.

11. **Common failure modes I want students to recognize.**
    - The "we'll know it when we see it" detection posture — no thresholds, no anomaly monitoring.
    - The single AI-incident playbook with no archetype differentiation.
    - The severity framework borrowed from cyber that doesn't capture affected-population scope.
    - The SLA that nobody could meet if they tried.
    - The post-incident review that turns into a blame session and nobody volunteers for on-call.
    - The knowledge base that doesn't actually get updated, so the same incident repeats six months later.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| RoutePilot AI logistics startup (mirrors demo) | Series A logistics startup, 3 cities, 500 active drivers, ~50,000 deliveries/day. Three incident types — route bias against certain neighborhoods (Bias), route accuracy degradation (Performance), driver location data exposure (Security). Walk through each: detection method, initial response, severity assignment, escalation path. Make the archetype differentiation concrete. | Walkthrough — anchor example |
| TransitAI safety-critical transit (mirrors exercise) | Urban transit, 15 metro areas, 2M+ daily passengers, 10,000+ vehicles. Safety-critical category — the regulatory anchors shift (FTA's 49 CFR Part 674, the 2-hour rail-transit notification). 10-incident playbook spanning six categories — Bias, Misuse, Performance, Security, Safety, Compliance — with examples including adversarial manipulation, training-data poisoning, unauthorized access, model hallucination, and offensive chatbot responses. Use to show how safety-criticality compresses the SLA window and how the same playbook skeleton has to scale across very different incident shapes. | Walkthrough — second anchor |
| The S1 incident clock | A safety-critical AI fails. The 2-hour FTA notification clock starts ticking at the moment of *operational awareness* — not the moment ops gets to the email. How does the on-call engineer trigger the regulatory reporting workflow before the clock burns? | Brief mention with timeline pressure |
| The blameless PIR that wasn't blameless | A team writes a PIR that quietly names the engineer who took the call as the proximate cause. Next quarter, nobody volunteers for the on-call rotation. The PIR culture *is* the on-call culture. | Brief mention |
| The cross-archetype incident | A "performance" incident on closer look is actually a bias incident — the accuracy drop is concentrated on a specific subgroup. The single-archetype playbook routes it to the ML platform team; the AI Risk Officer doesn't get looped in until day three. Use to show why initial classification matters. | Brief mention |

---

## What NOT to Cover

- **The Python detection code in detail** — implementation module's `detect_incidents()`, `determine_escalation()`, `recommend_response()` functions.
- **Specific threshold values for each metric** — implementation deliverable. Set up the *concept* of warning + critical thresholds with direction.
- **The full 10-incident TransitAI playbook content** — implementation exercise. The conceptual module sets up *why* the playbook has the shape it does.
- **MITRE ATLAS technique IDs in detail** — Module 3. Reference once: "security-archetype incidents will be ATLAS-anchored."
- **EU AI Act Article 73 in depth** — Module 4. Mention as a key SLA-shaping anchor; don't re-cover the tier structure.
- **GDPR Article 33 and CPRA breach mechanics** — Module 11. Mention as one of the SLA-shaping anchors.
- **KRI design for proactive monitoring** — Module 7 covers the proactive side; this module is reactive. Make the handoff clean.

---

## Additional Notes

- **Analogies.** AI incident response is to AI engineering what fire drills are to building management — the part everyone agrees is necessary, and the part everyone is happy to skip until the alarm goes off. The three archetypes are like the three types of medical emergency — cardiac, trauma, neurological — same general infrastructure, different specialty responders, different drugs in the kit.
- **Terminology.** "Archetype" is the deliberate word — it's stronger than "category" and signals that these are *pattern types* you'll recognize in the wild. Use "severity" (not "priority" or "level") to align with classical SEV nomenclature. "Incident commander" is the standard role. "Blameless post-incident review" — say the full phrase; the word *blameless* does work.
- **Avoid:** treating AI incidents as a subspecies of cyber incidents — they overlap but the bias and performance archetypes have no clean cyber parallel. Avoid borrowing severity definitions wholesale from the existing security org without redesigning for AI-specific dimensions. Avoid romanticizing the playbook as a document — it's a *contract* the IC uses operationally.
- **A grounded line worth seeding:** "Every safety-critical AI program I've worked on has had the same Day 1 conversation: 'we have an incident response process.' What they meant was: they had a cyber incident response process. What they didn't have was a playbook that knew the difference between a bias incident and a security incident. That's the work this module is about."
- **Another:** "The best playbook in the world is useless if the on-call engineer has to scroll past forty pages of intro to find the first step. Write the playbook for 3 a.m., not for the AI review board."
- **A reflective beat:** "Imagine your model fails right now, in the worst plausible way. What's the first thing your on-call would do? Now look at your existing incident response process and tell me whether it would actually route them there. The delta is your roadmap." Place near the back half.
- **A throwaway humanity beat:** "I once watched a team spend the first ninety minutes of an incident arguing about whether it was a security incident or a bias incident, because the playbook had different paths and they couldn't agree. The model kept making bad decisions while they debated. After that, we wrote the classification rules first."
- **Connection to the implementation module.** Students will complete a 10-incident playbook for TransitAI in Excel (severity, detection, initial response, investigation, resolution, communication, post-resolution actions per incident, the 4-tier severity framework, the 10-step reporting workflow, the 9-element blameless PIR template), and then implement threshold-based detection in a Python notebook (`detect_incidents()` comparing six metrics against warning + critical thresholds, `determine_escalation()` routing by severity and metric type, `recommend_response()` action suggestions, and a 6-panel monitoring dashboard). After this module they should be able to predict the playbook's columns, the severity framework's escalation rules, and the detection function's signature.

---
