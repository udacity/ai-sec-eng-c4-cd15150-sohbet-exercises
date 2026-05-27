# Video: Understanding Regulatory Compliance for AI and the EU AI Act
*Module 4.1 | Topic: Understanding Regulatory Compliance for AI and the EU AI Act*

---

## Opening Hook

> *"Until a couple of years ago, AI safety and AI security lived inside engineering. You wrote a paper, you ran a benchmark, you tweeted about it. Now there's a Regulation with an Article number that says, in writing, what your model must do before you put it on the EU market — and there's a number with a euro sign and 'million' attached to what happens if you ship it without doing so. The thing that used to be a technical discipline is now also a legal one. That changes who's in the room. A product manager walks into the AI review board with what they think is a perfectly reasonable feature: an emotion-recognition module that detects whether a customer is frustrated. They've shipped this kind of thing before. Under the EU AI Act, that feature lands in two prohibited categories at once if deployed in the wrong setting. The team has six weeks to launch. The lawyer just walked in. The room has gone quiet."*

The conceptual job here is to install three things: (1) why AI compliance is now a legal regime with teeth, (2) how the EU AI Act's risk-tier structure works as a classification system, and (3) what High-Risk classification actually obligates an organization to *produce*. The Act is the centerpiece, but it sits in a broader landscape students need to feel.

---

## Key Discussion Points

1. **The regulatory landscape, briefly.** The EU AI Act (Regulation (EU) 2024/1689, in force from 1 August 2024) is the headline. Around it: US Executive Orders on AI, sector-specific regulators stepping into the AI lane (CFPB on fair lending, FTC on AI claims, EEOC on hiring AI), state laws (NYC LL-144 for hiring AI, Colorado AI Act), and parallel regimes in the UK, Canada, China, Singapore. The EU AI Act is the *most structured* example, not the *only* example.

2. **"AI security" is not just "cybersecurity for AI."** The full legal stack includes data protection (GDPR), product safety (EU MDR for medical devices), fairness and non-discrimination (ECOA, Title VII, EU non-discrimination directives), consumer protection (FTC Act §5, EU UCPD), sector regulation, and the new AI-specific regimes on top. The job is *integration*, not picking one. Sets up Modules 11 (GDPR/CPRA) and 6 (incident response) too.

3. **Provider vs Deployer — the role distinction.** A *Provider* is the entity that places the system on the market under its own name. A *Deployer* (the new term for what was "User") is the entity using the system in a professional capacity. The two roles have *different* obligations. Get this terminology straight — students will see both.

4. **Extraterritorial reach.** The EU AI Act applies to any AI system *placed on the EU market* or whose *outputs are used in the EU*, regardless of where the provider is. A US AI company with no EU office can still be in scope. This is the part that makes US students sit up.

5. **The Brussels Effect.** Like GDPR before it, the EU AI Act is likely to set de facto global norms. Many multinationals build to the strictest applicable standard once the EU bar is in place. Plant briefly; don't oversell.

6. **Risk-based, not technology-based.** The Act doesn't say "if you use a transformer, do X." It says "if your AI system creates *this category of risk*, do Y." The *use case* drives the obligation. This anchors everything that follows.

7. **The five tiers.** Unacceptable (prohibited), High-Risk, General-Purpose AI / GPAI (Articles 51–55 — the layer for foundation models), Limited Risk (transparency obligations under Article 50), Minimal Risk.

8. **Unacceptable Risk — what's flatly prohibited (Article 5).** Don't read the list as a list. Pick categories and tell the story:
   - Subliminal manipulation causing harm
   - Exploiting vulnerabilities of specific groups (age, disability, socioeconomic situation)
   - Social scoring by public authorities (and by private actors in certain contexts)
   - Real-time remote biometric identification in public spaces by law enforcement (with carved exceptions)
   - Emotion recognition in workplaces and educational institutions
   - Biometric categorization to infer protected characteristics
   - Untargeted facial-image scraping for facial-recognition databases
   - Predictive policing of natural persons based solely on profiling

9. **High-Risk — the big middle (Article 6 + Annex I + Annex III).** Two routes:
   - **Annex I**: AI that is also a regulated product under existing EU product-safety legislation (medical devices under MDR/IVDR, machinery, toys, etc.). The AI inherits high-risk status from the underlying product regime.
   - **Annex III**: eight specific use-case areas — biometrics, critical infrastructure, education, employment, essential services (credit, insurance), law enforcement, migration, justice and democratic processes.
   
   Most engineering and governance work in the Act lives in this tier.

10. **GPAI — the foundation-model layer (Articles 51–55).** Catches OpenAI's GPT models, Anthropic's Claude, Google's Gemini, Meta's Llama. Provider obligations under Articles 53 / 55 became applicable on 2 August 2025. Models with "systemic risk" (very large training compute thresholds) have additional obligations under Article 55. When you *integrate* a GPAI model into your own system, your obligations depend on how you're using it — and a GPAI integration can elevate your own system's risk tier if the use case is High-Risk.

11. **Limited Risk — the transparency tier (Article 50).** Users must be informed when interacting with an AI (chatbot disclosure), when content is AI-generated (deepfake labeling), when biometric or emotion-recognition systems are in use (where not prohibited outright). These are transparency requirements, not heavy compliance, but they apply broadly.

12. **Minimal Risk — the rest.** Spam filters, AI-enabled video games, basic recommenders. No specific obligations beyond general law. The Commission encourages voluntary codes of conduct. This tier exists to make clear the Act doesn't try to regulate every AI system.

13. **The classification decision tree.**
    - Is it on the Article 5 prohibited list? → Unacceptable.
    - Is it a GPAI model in itself? → GPAI tier.
    - Does it fall under Annex I or Annex III conditions? → High-Risk.
    - Does it interact with people, generate content, or use biometrics under Article 50? → Limited Risk.
    - None of the above? → Minimal.
    - And: a system can be in multiple tiers simultaneously.

14. **Classification pitfalls that bite real teams.**
    - "The model is just a tool" — the Act looks at the system *as deployed*.
    - "We're US-only" — outputs used in the EU put you in scope.
    - Missing GPAI entirely and treating a foundation-model integration as Limited Risk. This is the silent classification error the exercise is built around.
    - "Internal-only" — the Act distinguishes by use case and impact, not internal vs external.

15. **High-Risk obligations — the engineering deliverables.** Walk a handful narratively; don't list. The shape is:
    - Article 9 — Risk management system across the lifecycle
    - Article 10 — Data and data governance (training, validation, testing data; bias detection and mitigation)
    - Article 11 — Technical documentation (Annex IV as the content spec)
    - Article 12 — Record-keeping and logging
    - Article 13 — Transparency and information to deployers
    - Article 14 — Human oversight
    - Article 15 — Accuracy, robustness, cybersecurity
    - Article 17 — Quality management system
    - Article 50 — User-facing transparency
    - Article 72 — Post-market monitoring (a *system*, not a report)
    - Article 73 — Serious-incident reporting (15-day general default; 2 days for widespread infringement; 10 days for incidents involving the death of a person)
    - Articles 43–47 — Conformity assessment and CE marking

16. **Article 11 deep cut.** Article 11 requires technical documentation drawn up *before placing on market or putting into service*. The content is defined by Annex IV — nine sections covering general description, system characteristics, monitoring approach, training data, risk management measures, conformity assessment evidence, post-market monitoring plan. Annex IV is the *recipe*. Article 11 is the *requirement that you cook it*.

17. **"Your Model Card doesn't satisfy Annex IV alone."** Critical because this is the bridge to Module 9. A Model Card covers parts of Annex IV — typically intended use, performance, fairness, security considerations. It does *not* cover the full risk management system (Article 9), data governance (Article 10), quality management system (Article 17), conformity assessment evidence (Article 43). The Article 11 stack is *collective* — Model Card plus Datasheet plus System Card plus impact assessment plus QMS docs.

18. **Article 10 vs Article 15 — where bias-prevention obligations live.** Article 10(2)(f)–(g) is the *training-data* bias examination and mitigation requirement. Article 15 is the *runtime* accuracy, robustness, and cybersecurity requirement. Both touch fairness in different ways.

19. **Article 13 vs Article 50 — disclosure to whom.** Article 13 is provider-to-deployer transparency. Article 50 is user-facing transparency. Both can apply to the same system.

20. **Conformity assessment — what it means in practice.** For most Annex III High-Risk systems, conformity assessment is *internal* (provider self-attests against the requirements, signs the EU Declaration of Conformity, affixes the CE marking). For some categories — biometric identification under Annex III, and Annex I products requiring third-party assessment under existing product law — conformity assessment requires a *Notified Body*. The gate between "we built it" and "we can place it on the EU market."

---

## Examples to Include

| Example | Description | Level of Detail |
|---------|-------------|-----------------|
| TalentScope's HR recruitment AI (mirrors exercise) | A video-analysis hiring tool with an 8% gender-bias finding. Under Annex III §4 (employment), this is High-Risk. Apply the decision tree out loud. Walk the Article 11 stack TalentScope would need to produce — general description, training data details (with the bias finding under Article 10), risk management (Article 9), human oversight (Article 14 — the recruiter's role in confirming or overriding), accuracy and robustness testing (Article 15). The point: each Annex IV section is a deliverable with a named owner. | Deep dive — primary anchor |
| AutoPilot Logistics' AssistGPT (mirrors demo) | A logistics company integrating a foundation model into its dispatcher console for natural-language operations queries. The integration is GPAI-tier on its own. The underlying use case (logistics queries) is not Annex III, so the integrated system itself is *not* High-Risk — but GPAI provider obligations attach upstream. Makes the GPAI layer concrete. | Walkthrough — second anchor |
| The HR AI in scope of multiple regimes | One system, three regulators interested: the EU AI Act under Annex III §4, EEOC / Title VII on the US side, NYC LL-144 if used in NYC hires. Same model, three regimes, three obligation sets. Makes the multi-regime reality visible. | Brief mention |
| The workplace emotion-recognition feature from the hook | Reinforce the Article 5 prohibition. "We'll just remove the emotion module" remediation works. "We'll deploy it anyway" path does not. | Brief mention |
| A clinical decision-support system | Both Annex III §5 (essential services / health) *and* Annex I (regulated medical device under MDR). Same High-Risk obligations, two statutory anchors. Shows routing matters when an auditor asks "which Annex are you under?" | Brief mention |
| The chatbot with Article 50 obligations | An LLM customer-service bot — minimal risk in most senses, *but* Article 50 still requires users be told they're interacting with AI. Even "low risk" carries obligations. | Brief mention |
| The Article 73 incident clock | A High-Risk system experiences a serious malfunction. The 15-day clock starts from the moment the provider becomes aware. How does the on-call engineer escalate to the compliance team fast enough that the 15 days isn't half-burned before legal hears? | Brief mention with the deadlines stated |
| The conformity-assessment failure mode | A team ships technical documentation and CE marking but skips the *quality management system* under Article 17. Six months later an audit finds the documentation has no version control, no review log, no signoff trail. The whole conformity claim crumbles. Motivates the QMS. | Brief mention |

---

## What NOT to Cover

- **The full text of every Article 5 prohibition** — narrative, not list.
- **GPAI Article 51–55 obligations in deep detail** — covered briefly; leave full unpacking for follow-up work.
- **Bias and fairness auditing techniques** — Module 10. Reference TalentScope's 8% gender-bias finding only as the *trigger* for High-Risk classification.
- **MITRE ATLAS threat modeling** — Module 3.
- **Model Card mechanics line by line** — Module 9 unpacks the artifact.
- **Incident response playbook design** — Module 6. Article 73 deadlines should be mentioned; the playbook itself is Module 6's work.
- **Post-market monitoring KRI design** — Module 7.
- **Fundamental Rights Impact Assessment (FRIA)** — touch lightly; it's a deployer obligation and the exercise is from a provider perspective.
- **Specific fines** — they exist (up to €35M or 7% of global turnover for the worst violations) but they move with adjustments and dating the video badly is a risk. Make the structural point that the fines have teeth, not the precise number.

---

## Additional Notes

- **Analogies.** AI compliance now is what data privacy was in the late 1990s — a discipline practiced informally by some, mostly aspirational, no shared bar — until GDPR landed in 2018 and the world changed in two years. The EU AI Act is the GDPR moment for AI. For the risk tiers: think building zoning. Unacceptable Risk is land you cannot build on. High-Risk is land that requires permits, inspections, structural engineering, fire-marshal sign-off. GPAI is a separate planning regime for the foundations of the building. Limited Risk is land with light disclosure rules (post a sign). Minimal Risk is unrestricted. The same property can sit in multiple zones, and you have to satisfy each zone's rules. For Article 11: a building permit set. The permit set is not the building; it's the *documentation* that proves the building was designed and constructed against code.
- **Terminology.** "EU Artificial Intelligence Act" spelled out on first mention, then "EU AI Act" or "the AI Act." "Regulation (EU) 2024/1689" used once for credibility. "Provider" and "Deployer" defined on first use. Article numbers stable — lean on them ("Article 11," "Annex IV," "Article 73"). Use Annex citations as the *content* anchor and Article citations as the *obligation* anchor.
- **A precise nuance worth landing.** When materials cite "Article 11 §1(a)–(h)," that's pedagogical shorthand. Article 11(1) is a single paragraph saying "draw up technical documentation containing, at a minimum, the elements in Annex IV." The topical sections (a)–(h) are *Annex IV* sections 1–9. Sloppy citation in compliance writing gets a program flagged.
- **Another precise nuance.** GPAI was in the original 2024 Regulation, not a later amendment. Substantive provider obligations applicable from 2 August 2025; the broader High-Risk regime becomes generally applicable 2 August 2026. Don't fuzz the timeline — regulators don't.
- **Avoid:** treating the EU AI Act as the only AI regulation that exists. Avoid giving legal advice. Avoid suggesting the Article 5 prohibitions are vague or aspirational — they are prohibitions. Avoid treating Annex III as exhaustive — the list is updateable by Commission delegated acts.
- **A reflective beat to seed:** "Think about the most consequential decision your AI system makes today. If a regulator asked you to defend that decision in writing, with the specific Article of the relevant regulation cited, could you? That's the gap this module closes." And another for late in the module: "If a Notified Body walked into your office tomorrow and asked to see your Annex IV documentation for a system you ship today, what would they find? That answer is your compliance roadmap."
- **A framing line worth seeding:** "The classification step is the entire compliance program in microcosm. Get it wrong and every downstream control is calibrated to the wrong risk."
- **Connection to the implementation module.** Students will build a compliance matrix in Excel — risk-tier classification, applicable Articles including Article 73, current control status (Implemented / Partial / Gap), remediation actions. They'll also write a Python rule-based classifier covering all five tiers including GPAI for six test systems (HR recruitment, healthcare diagnosis, GPAI integrator, biometric finance, social scoring, inventory optimization). After this module they should be able to predict the classifier's signal logic (biometric flag, fundamental-rights-impact flag, safety-criticality flag, social-scoring flag, foundation-model-integration flag) and understand that the matrix will look like a roadmap, not a checklist.

---
