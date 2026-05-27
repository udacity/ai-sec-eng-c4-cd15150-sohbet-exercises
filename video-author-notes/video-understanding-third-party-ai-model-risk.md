# Video: Understanding Third-Party AI Model Risk
*Module 8.1 | Topic: Understanding Third-Party AI Model Risk*

---

## Opening Hook

> *"Your fraud detection model is a wrapper around a vendor's API. One Tuesday, the vendor pushes a model update. They don't tell you. Your false-positive rate doubles overnight, customer complaints flood in, and your risk team needs to write the post-mortem. The first question the board asks: 'whose model was making these decisions?' The honest answer is 'we don't actually know — it depends on which version was live this morning.' That is the AI supply-chain problem in one sentence. The model your customers experience is rarely the model your team built. It's a chain, and you own the whole chain whether you sourced it or not."*

The conceptual job here is to install two ideas: (1) third-party AI introduces a *different* shape of supply-chain risk than classical software vendors, and (2) the assessment categories and contractual levers have to be designed for that shape — copy-pasting your existing SOC 2 questionnaire does not work.

---

## Key Discussion Points

1. **The AI supply chain has more moving parts than software supply chain.** Classical software vendor risk: code provenance, library dependencies, infrastructure, access controls, breach history. AI vendor risk adds: training-data provenance, training-data licensing, model-update cadence, model behavior reproducibility, foundation-model dependencies underneath the vendor, fine-tuning portability, inference infrastructure, and the *behavioral surprise* problem — the model can change without code changes.

2. **Why "the model your customers experience is rarely the model your team built."** Three layers of indirection in a typical production stack: (1) foundation-model provider underneath your vendor (OpenAI, Anthropic, Google), (2) your vendor's fine-tune / RAG / scaffolding layer, (3) your own integration layer. Any layer can change without coordination. Behavior changes propagate downward through the stack and into your customers without anyone shipping code in your repo.

3. **The vendor assessment categories AI requires.** Most security questionnaires cover one or two of these. AI requires all of them:
   - **Security posture** — the classical surface. Access controls, encryption at rest and in transit, certifications (SOC 2, ISO 27001, FedRAMP if applicable).
   - **Data handling** — what data they collect from your prompts and inferences, retention policies, training-data use rights, deletion guarantees, geographic data residency.
   - **Model transparency** — what they'll tell you about training data, model architecture, evaluation methodology, known failure modes. Most vendors are vague here. Push.
   - **Adversarial robustness** — red-team history, security-evaluation results, prompt-injection defenses, jailbreak resistance.
   - **Financial stability** — can they survive the next 24 months? AI vendors burning cash on training compute have failure rates that classical SaaS doesn't.
   - **SLA quality** — uptime, latency, error budgets, model-update notification cadence (this last one is AI-specific and rarely in the boilerplate SLA).
   - **Exit strategy** — what does it look like to leave? Can you export your fine-tunes? Your embeddings? Your prompt library? Your conversation logs?
   - **AI model governance (the GenAI-specific 7th)** — training-data provenance, model-update notification commitments, fine-tuning portability, liability terms for vendor-side behavioral changes.

4. **Training-data provenance is the question every vendor will dodge.** "Where did your training data come from? What licenses? What permissions? Any litigation risk?" Most vendors will refuse to answer in detail. Their answer matters anyway, because IP claims and privacy claims against the vendor become *your* claims when you deployed their model.

5. **Model update notification — the contract clause nobody writes.** A standard SaaS contract says the vendor can update software with notice. An AI vendor that updates the *model* under the hood without telling you can silently change your customer's experience. The contractual lever: require notification of material model changes with a defined window — 30 days, 60 days, or whatever fits your release cadence — and require an option to pin to a prior version. Not all vendors will agree. The ones who will are the ones worth doing business with at enterprise scale.

6. **Shared infrastructure risk.** When you use a foundation-model API, your prompts and your competitors' prompts are processed on the same infrastructure, potentially by the same model instances. The provider's tenant isolation matters more than your typical SaaS evaluation accounts for. Ask about isolation architecture, not just encryption.

7. **The risk-scoring approach.** Score vendors across the categories on a 0–100 per-criterion scale, weight the criteria to reflect your industry's priorities (insurance prioritizes data handling and SLA; consumer-AI prioritizes content safety and reputation; healthcare prioritizes data handling and regulatory alignment), convert the weighted average to a 1–5 risk scale (1 = lowest risk, 5 = highest), and use that to classify vendors as Highly Recommended / Recommended / Acceptable with Monitoring / Not Recommended. The scoring scheme is your design choice — the discipline is documenting *why* the weights are what they are.

8. **The recommendation tiers as decisions.**
   - **Highly Recommended** — risk ≤ 1.5 + SLA compliant. Sign with standard contractual terms.
   - **Recommended** — risk ≤ 2.5 + SLA compliant. Sign with enhanced monitoring clauses.
   - **Acceptable with Monitoring** — risk ≤ 3.5. Sign with specific mitigating controls and quarterly review.
   - **Not Recommended** — risk > 3.5. Decline, or escalate to executive risk acceptance with documented residual.

9. **SLA compliance is operational, not just contractual.** A vendor with a 99.99% uptime SLA is not the same as a vendor *actually delivering* 99.99% uptime. Track 30-day rolling actual vs contractual. A vendor whose contractual SLA is great but whose actual SLA has been amber for three months is materially riskier than the contract suggests. KRIs from Module 7 connect directly here.

10. **The exit-strategy analysis nobody does.** Bucket vendors by switching cost. Low — you can rebuild in two weeks. Moderate — three to six months. High — it would take a multi-quarter project and customer comms. Concentrating production risk in High-switching-cost vendors is a strategic risk, not a procurement detail. Surface it at the board level.

11. **Sensitivity analysis as a sanity check.** Perturb a vendor's per-criterion scores by ±10 points and re-run the risk scoring. If the recommendation tier flips, your scoring is fragile and the decision is being driven by noise. If the tier holds, the recommendation is robust. Build this into your governance: any vendor near a tier boundary should have a sensitivity analysis in the file.

12. **Contractual levers for AI-specific risk.** Beyond standard SaaS terms:
    - Notification window for material model updates with right to pin to a prior version.
    - Right to audit (read-only) of training-data documentation.
    - Liability allocation for vendor-side model behavior changes that cause customer harm.
    - Indemnification for IP claims arising from vendor's training data.
    - Data residency and deletion guarantees, with audit rights.
    - Behavioral SLAs (e.g., bias-metric ceilings, jailbreak-resistance benchmarks) where the use case warrants and the vendor will accept them.
    - Termination assistance — what happens to your data, fine-tunes, and embeddings on exit.

13. **The regulatory anchors that quietly shape vendor risk.**
    - **EU AI Act provider/deployer roles** — buying a foundation model and embedding it makes *you* the provider of the integrated system in most cases. The vendor's GPAI obligations don't substitute for yours.
    - **GDPR processor / sub-processor structure** — Articles 28, 33, 44. If the vendor processes personal data on your behalf, you need a DPA and you inherit certain notification timelines.
    - **PCI DSS for payment data** — notification of acquirers / card brands, separate from GDPR's 72-hour Article 33 timeline.
    - **HIPAA Business Associate Agreement** — for healthcare data.
    - **Sector regulators** — for regulated industries, the vendor must fit your existing third-party risk regime (banking OCC guidance, FDA software-as-a-medical-device rules, etc.).

14. **The common failure modes.**
    - Copying the existing SaaS questionnaire and missing the AI-specific categories entirely.
    - Skipping the financial-stability check on hot AI vendors because "they just raised a Series C."
    - Trusting "we have SOC 2" as a substitute for AI-specific assessment.
    - Not tracking actual SLA performance vs contracted.
    - Not weighting the criteria — every dimension scored equally regardless of which dimension matters for the use case.
    - Sensitivity-fragile recommendations approved as final.
    - No exit-strategy analysis, leading to concentration risk.

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| CloudFirst Financial vendor evaluation (mirrors demo) | Financial services company evaluating two AI vendors (CloudVault AI, TitanScale AI) for fraud detection after a competitor's 6-hour vendor outage. Walk through five criteria, weighted scoring, simulated SLA data, side-by-side comparison, governance recommendation. Make the assessment categories concrete. | Walkthrough — anchor example |
| InsureLogic's five-vendor portfolio (mirrors exercise) | Insurance-technology company managing five AI vendor relationships (NovaMind API, CloudVault AI, TitanScale AI, DeepLens AI, SafeGuard AI). A vendor model update caused false claim denials, triggering a formal risk assessment. Walk through the seven risk dimensions including the GenAI-specific AI_Model_Governance dimension. | Walkthrough — second anchor |
| The silent model update | A vendor pushes a model update on a Tuesday morning. No notification. Your monitoring picks up the FPR spike at noon, customer support escalates by 2 p.m., post-mortem opens by 3. The contract has no notification clause. The vendor's position: "we updated our software per the SaaS agreement." Use this to motivate the contractual lever specifically. | Brief mention with timeline |
| The "SOC 2 is enough" trap | A vendor presents SOC 2 Type II as the assessment package. SOC 2 covers access controls and operations — it does not cover training-data provenance, model-update notification, or behavioral robustness. Use to motivate why the AI-specific categories aren't optional. | Brief mention |
| The exit-strategy bucket | Five vendors. One is Low switching cost (open API, portable embeddings). Three are Moderate. One is High (proprietary fine-tunes, no export path, six-month migration). The High-bucket vendor concentrates production risk that the per-vendor risk score doesn't capture. | Brief mention |
| The sensitivity-fragile recommendation | A vendor scored at 2.49 — landing in "Recommended." Perturb the scores by ±10 points; the recommendation flips to "Acceptable with Monitoring." The decision was driven by noise. Use to land the sensitivity-analysis discipline. | Brief mention |

---

## What NOT to Cover

- **Implementing the weighted-scoring Python function in detail** — implementation module.
- **The 30-day simulated SLA dashboard mechanics** — implementation module.
- **Specific vendor names or recent industry incidents** — risk of dating the video badly.
- **GDPR articles in depth** — Module 11. Touch as anchoring law only.
- **MITRE ATLAS attacks against vendor models** — Module 3.
- **EU AI Act Articles in depth** — Module 4. Mention only the provider/deployer routing point.
- **KRI design for vendor SLA monitoring** — Module 7. Reference the connection.
- **AWS Bedrock Guardrails / similar specifics** — overly product-specific. Bedrock Guardrails handles content-safety filtering, denied topics, contextual grounding for hallucinations, PII redaction, and harmful-output filters; demographic-bias detection in the fairness-metric sense (demographic parity, equalized odds) is a separate workload handled by Fairlearn or AIF360. Touch this only if a writer mistakenly conflates them.

---

## Additional Notes

- **Analogies.** AI vendor risk is to classical SaaS vendor risk what a multi-tier subcontracting chain is to a single-vendor relationship. A general contractor with subcontractors with sub-subcontractors — you own the building when it falls down, regardless of which layer of the chain made the mistake. Another: AI vendor assessment is like buying a car you've never seen, from a dealer who won't show you the engine, with the manufacturer reserving the right to swap the engine at any time without notification. The discipline of the assessment is closing those gaps with contractual levers.
- **Terminology.** "Third-party AI" and "AI vendor" — interchangeable. "Foundation-model provider" for the layer underneath your vendor. "AI supply chain" for the full stack. "Risk-weighted scoring" not "risk scoring" — emphasize the weighting. "Recommendation tier" not "rating."
- **Avoid:** treating AI vendor risk as a procurement-only problem; it's a security, legal, and product problem. Avoid romanticizing the questionnaire — questionnaires are the *artifact*; the assessment is the work. Avoid certainty about vendor-side behavior — every model-as-a-service vendor reserves the right to change behavior.
- **A grounded line worth seeding:** "Every AI program I've worked with has the same blind spot — the vendor assessment that was done at procurement and then never re-run. AI vendors aren't static. Your assessment shouldn't be either."
- **Another:** "The cheapest way to find out a vendor's exit cost is to ask them, on day one, what termination assistance looks like. Their answer tells you everything about what your second year is going to feel like."
- **A reflective beat:** "Pick the AI vendor your team is most dependent on. If they shipped a material model change tomorrow, would you know? In what timeframe? Through what channel? That answer is your vendor-monitoring posture." Place near the back third.
- **A throwaway humanity beat:** "I once approved a vendor on a beautiful SOC 2 report and a confident sales call. Six months later we discovered they were a thin wrapper on a foundation model whose terms of service explicitly retained training rights on customer prompts. We had given them production prompts containing customer PII. That's the conversation that taught me the AI-specific dimensions matter." Use sparingly.
- **Connection to the implementation module.** Students will complete vendor governance in Excel (assessment across five criteria, certifications, evidence, risk ratings, SLA performance vs contractual thresholds), and in Python score five vendors across seven dimensions (including the GenAI-specific AI_Model_Governance dimension), implement the weighted-scoring function with their own 0–100 to 1–5 conversion logic, implement the recommendation-classification function, run the model-update scenario analysis on the InsureLogic incident, bucket vendors by exit strategy, and stretch into sensitivity analysis. After this module they should be able to predict the seven dimensions, the recommendation thresholds, and why each contractual lever matters.

---
