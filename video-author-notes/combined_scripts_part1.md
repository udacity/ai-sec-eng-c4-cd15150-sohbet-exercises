| Program Info | Title | | Key |
| :---- | :---- | :---- | :---- |
| ND | AI Security Engineer (nd909) | | |
| Course | cd15150 — AI Security Strategy, Risk, Governance, and Compliance (GRC) | | |
| Modular content sequence *(if modular build)* | Part 1 of 3 | | |
| Production Tier | | | |
| **Build Team** | | **Production Requirements** | **Number of videos** |
| TCD | Prachi Dawer | Headshots + Slides | 4 |
| PgM | Ye Li | Slides | - |
| Producer | | Slides + Demo | - |
| Author name | Sohbet Dovranov | Demo | 6 |
| Author email | sohbetdovranov@gmail.com | Solution | 6 |
| | | Headshots + Demo | - |
| | | Headshots + Slides + Demo | - |
| | | Static graphics (not videos) | - |
| | | **TOTAL videos** | **16** |

## Module/Video #: Module 1 Video 1

### Title: Course Introduction — AI Security GRC

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| A model is sitting in production right now at some company, quietly approving loans, flagging transactions, or screening job applicants. It works. Until the day a regulator, a journalist, or a rejected customer asks one simple question: why did it make that decision, and who signed off on letting it? Welcome to the part of AI security that does not live in the code. This is the course on strategy, risk, governance, and compliance. | HEADSHOT. Animated lower-third title fades in on the last line: 'AI Security: Strategy · Risk · Governance · Compliance'. |
| Here is the shift you are about to make. Up to now in this program, the work has been about building and attacking AI systems. This course is about the layer that sits above all of that: deciding whether a system is safe to ship, proving it to people who are not engineers, and staying on the right side of the law while you do it. This is the work that turns a clever model into a trustworthy product. | HEADSHOT. Text overlay animates a hand-off: 'Build & Secure the AI' fades out, 'Govern · Assess · Defend the Decision' fades in over the speaker's shoulder. |
| Think about the role you are stepping into. For these modules, you are not the model builder. You are the person leadership turns to and asks, can we safely launch this? You are the one who has to translate a confusing technical reality into a clear, defensible recommendation. That is the job of an AI risk and governance lead, and it is one of the fastest-growing seats in the room. | HEADSHOT. Animated lower-third name-tag overlay reveals: 'Your role: AI Risk & Governance Lead'. |
| So what will you actually be able to do? First, you will master the frameworks that give your judgments authority. You will use Explainable AI to audit why a model made a call, run threat modeling with MITRE ATLAS, operationalize the NIST AI Risk Management Framework, and classify a system under the EU AI Act. These are the reference points auditors and regulators already speak. | HEADSHOT. Four keyword chips pop in over the shoulder, one per framework as it is named: 'Explainable AI', 'MITRE ATLAS', 'NIST AI RMF', 'EU AI Act'. |
| Then you will turn frameworks into day-to-day practice. You will write enforceable AI policies, run an incident response drill for an AI-specific breach, design the security metrics that actually wake a team up at night, assess third-party model vendors, document a model card, audit for bias and fairness, map your privacy obligations, and design the operating model that holds it all together. | HEADSHOT. An animated checklist overlay ticks items on as they are spoken: Policies · Incident Response · Security Metrics · Vendor Risk · Model Cards · Bias & Fairness · Privacy · Operating Model. |
| Here is how the learning works. Every concept you meet in these videos, you then put your hands on. You will work through guided demos and then build the real artifacts yourself in workbooks and notebooks: risk registers, threat models, KRI dashboards, model cards. The goal is not to memorize definitions. It is to produce the evidence a real governance review demands. | HEADSHOT. Two-word overlay animates left-to-right: 'Watch the concept' transitions into 'Build the artifact'. |
| It all comes together in your project. You will take on Operation HealthGuard, a full governance review of an AI model that predicts patient diabetes risk. Acting as the lead AI Risk Officer, you will assess it from every angle and produce the portfolio that decides its fate: a risk register, a model card, and a metrics dashboard. Your verdict determines whether it launches. | HEADSHOT. Project title overlay 'Operation HealthGuard' animates in; three deliverable tags reveal in sequence — 'Risk Register', 'Model Card', 'Metrics Dashboard' — then a final 'Launch Decision' stamp. |
| So let me leave you with the question this whole course is built to answer. The next time a high-stakes AI system lands on your desk and someone asks whether the company can safely stand behind it, will you be guessing, or will you have the evidence? By the end of these modules, you will be the person in the room who can answer with confidence. Let us get started. | HEADSHOT. Closing reflective-question overlay fades up: 'Guessing — or evidence?' then resolves to 'Let''s get started.' |

## Module/Video #: Module 2 Video 1

### Title: Understanding Explainable AI (XAI) for Security Auditing

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| A bank declines a loan. The applicant calls, and the rep reads, "Declined by model." Multiply that by four hundred times a day, and you have a regulator showing up with a subpoena. But consider this: two analysts can look at the exact same SHAP plot and reach opposite conclusions. One screams bias, the other sees a valid risk signal. The disagreement happens upstream of the math. Explainability tools cannot resolve what discrimination actually means. | HEADSHOT |
| You might think a simple decision tree solves this opacity. It does not. A four-hundred-feature tree with categorical encodings is still functionally a black box. The real issue is the system around it. If your on-call engineer cannot trace a prediction back through the feature store and caching layers, you have a lineage failure. Most explainability failures are system lineage failures, not just complex math. | Horizontal system flow diagram. Left: 'Prediction Output'. Arrows pointing back right-to-left through 'Model (400-Feature Tree)', 'Caching Layer', and 'Feature Store'. A red dashed box around the whole flow labeled 'Lineage Failure'. [CLICK:] Reveal the Model node; [CLICK:] Reveal arrows pointing back to Caching Layer and Feature Store; [CLICK:] Highlight with red dashed box labeled Lineage Failure |
| Why does this matter? Because compliance requires meaningful information. Under regulations like ECOA, you must provide specific reasons for adverse actions. "The model says no" is not a legal defense. Furthermore, explainability is a key detective control for security. If you cannot explain a model's benign decisions, how will you detect an adversary manipulating your system into systematically misclassifying inputs? | Two-column layout. Column 1: 'Compliance (ECOA)' with an icon of a legal document and label 'Specific reasons for adverse action'. Column 2: 'Security Detective Control' with an icon of a magnifying glass over a gear and label 'Detect adversarial manipulation'. [CLICK:] Reveal Compliance column; [CLICK:] Reveal Security column |
| When was the last time you had to defend a model's decision to someone who did not trust it? You quickly learn one chart does not satisfy everyone. We have four audiences here. Your model risk team wants global behavior. Regulators need a defensible explanation for a single decision. The declined applicant wants an actionable reason code. And your on-call engineer just wants to know which feature drifted. | 2x2 grid of audience profiles with icons and labels. Top-Left: 'Model Risk Team' pointing to 'Global Behavior'. Top-Right: 'Regulator' pointing to 'Single Decision Defense'. Bottom-Left: 'Applicant' pointing to 'Actionable Reason Code'. Bottom-Right: 'On-Call Engineer' pointing to 'Feature Drift'. [CLICK:] Reveal Model Risk Team; [CLICK:] Reveal Regulator; [CLICK:] Reveal Applicant; [CLICK:] Reveal On-Call Engineer |
| To serve these audiences, you must separate global and local feature importance. Global importance tells you the model's average behavior across a population. Local importance answers why this one specific prediction happened. As an auditor, your findings usually live in the tension where a local decision drastically deviates from the global average. | Two side-by-side bar charts. Left chart: 'Global Importance' showing average bar heights for Features A, B, C. Right chart: 'Local Importance (Single Prediction)' showing Feature C with a massive spike. A warning icon between them labeled 'Deviation = Audit Finding'. [CLICK:] Reveal Global Importance chart; [CLICK:] Reveal Local Importance chart; [CLICK:] Show warning icon labeled Deviation |
| This is where SHAP comes in. You do not need the game theory math, just the intuition: for a given prediction, SHAP calculates how much each feature pushed the outcome away from the model's average. It gives you signed contributions. Maybe income pushed approval up ten percent, while late payments pushed it down five. They sum perfectly to the difference between the baseline and your final prediction. | Waterfall chart. Starting baseline at 50%. A green bar going up (+10%) labeled 'Income'. A red bar going down (-5%) labeled 'Late Payments'. A final dotted line ending at 55% labeled 'Final Prediction'. [CLICK:] Show baseline; [CLICK:] Reveal +10% Income bar; [CLICK:] Reveal -5% Late Payments bar; [CLICK:] Show Final Prediction line |
| You might wonder about LIME, another popular tool. LIME fits a simple local model around your prediction. It is fast, but stochastic. Run it twice, and your feature rankings might randomly shuffle. SHAP is mathematically consistent. Run it twice, and the list stays locked in place. For regulator-facing audits where defensibility is paramount, stochastic outputs are a massive liability. | Side-by-side comparison table. Left column: 'LIME' with arrows showing shifting feature ranks and label 'Stochastic / Random Shuffle'. Right column: 'SHAP' with a padlock icon over static feature ranks and label 'Mathematically Consistent / Locked'. Bottom banner: 'Stochastic = Audit Liability'. [CLICK:] Reveal LIME column; [CLICK:] Reveal SHAP column; [CLICK:] Reveal bottom banner |
| Let us look at hunting for hidden bias, specifically proxy-variable leakage. This happens when your model uses an innocent feature, like a ZIP code, as a stand-in for a protected class. Spot this by comparing local to global importance. If a feature has a low global average but an aggressively high local contribution on flagged cases, you have a red flag. | Bar chart comparison. X-axis: Features (Income, Age, ZIP Code). Y-axis: Contribution Score. Blue bars for 'Global Average' showing ZIP Code is low. Red dots for 'Local Contribution' showing ZIP Code dot is aggressively high. A red circle highlighting the ZIP code gap labeled 'Proxy-Variable Leakage'. [CLICK:] Show Global Average bars; [CLICK:] Overlay Local Contribution dots; [CLICK:] Reveal red circle on ZIP code gap |
| Once you suspect a proxy variable, how do you prove it? You run a counterfactual ablation. Take your declined case and replace that suspect ZIP code with the baseline training median. Re-score the model. If the decision abruptly flips from decline to approve, you have a definitive audit finding. You have proven the proxy drove the adverse outcome. | Flow chart. Node 1: 'Declined Case (Suspect ZIP)'. Arrow to Node 2: 'Replace ZIP with Training Median'. Arrow to Node 3: 'Re-score Model'. Arrow to Node 4: 'Result: Approve'. A large label over the final arrow reads 'Decision Flip = Proven Proxy'. [CLICK:] Reveal Node 1 and Node 2; [CLICK:] Reveal Node 3; [CLICK:] Reveal Node 4 and Decision Flip label |
| Before writing that finding, consider this: if asked to defend a SHAP plot, could you also defend what it does not say? First, correlation is not causation. A high SHAP value means a feature moved the model, not that it caused the real-world outcome. Second, SHAP is highly sensitive to your background dataset. Swap reference data, and your explanation shifts. Finally, rare features in imbalanced datasets can look artificially massive. | Three-column list with warning icons. Column 1: 'Correlation ≠ Causation' (Link broken icon). Column 2: 'Background Sensitivity' (Database icon with shifting arrows). Column 3: 'Rare Feature Exaggeration' (Magnifying glass over a tiny dot appearing huge). [CLICK:] Reveal Correlation ≠ Causation; [CLICK:] Reveal Background Sensitivity; [CLICK:] Reveal Rare Feature Exaggeration |
| Ultimately, raw plots are not an audit report. The interpretation layer is your actual deliverable. Your memo must synthesize local and global findings, prove the proxy through ablation, and explicitly state technical caveats. The plot is just evidence; the narrative is what governance acts on. Explainable AI is a powerful lens, but making sure a model is fair always rests with the human at the end of the API. | HEADSHOT |

## Module/Video #: Module 3 Video 1

### Title: shap_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 3 Video 2

### Title: xai_audit_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 1

### Title: Understanding the NIST AI Risk Management Framework

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 5 Video 1

### Title: risk_scoring_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 5 Video 2

### Title: risk_assessment_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 5 Video 3

### Title: risk_scoring (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 5 Video 4

### Title: risk_assessment (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 6 Video 1

### Title: Understanding AI Threat Modeling with MITRE ATLAS

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| Somebody jailbreaks your customer-support chatbot into issuing a refund it shouldn't. Your security team writes up the incident. Two months later, three other companies independently discover the exact same trick. But they are describing it in three entirely different ways with no shared vocabulary. That is a massive problem. Without a common language, how do defensive communities actually learn from each other? | 3-column layout representing different companies. Column 1: Company A labeled 'Prompt Hack'. Column 2: Company B labeled 'Chatbot Bypass'. Column 3: Company C labeled 'LLM Exploit'. [CLICK:] A large red 'X' appears over the three columns with a bold label: 'No Shared Vocabulary'. Click to show the red 'X' and 'No Shared Vocabulary'. |
| That naming problem is exactly what MITRE ATLAS exists to solve. ATLAS stands for Adversarial Threat Landscape for AI Systems. It is a curated, standardized knowledge base of how attackers actually behave against live AI systems. If you have ever used the MITRE ATT&CK framework for enterprise security, you will find this has the exact same shape, just mapped specifically to AI. | Central node labeled 'MITRE ATLAS'. [CLICK:] The node expands downward to reveal the full acronym: 'Adversarial Threat Landscape for AI Systems'. [CLICK:] Two branching nodes appear from the center: 'Curated Knowledge Base' and 'Maps to MITRE ATT&CK'. Click to expand the acronym; click to show the two descriptive branches. |
| So, how does this framework organize threats? It uses TTPs, which stands for Tactics, Techniques, and Procedures. A Tactic is the overarching goal the adversary wants to achieve, like extracting data. A Technique is exactly how they achieve it, such as injecting malicious prompts. Finally, a Procedure is the documented, real-world instance of this happening to a live production system. | A 3-level pyramid diagram. Top level: 'Tactic' with a small label '(Goal: Extract Data)'. [CLICK:] Middle level: 'Technique' with a small label '(Method: Prompt Injection)'. [CLICK:] Bottom level: 'Procedure' with a small label '(Real-world Incident)'. Click to reveal Technique; click to reveal Procedure. |
| Now, you do not need to memorize the whole catalog. You really just want to focus on what hits incident reports, like LLM Prompt Injection, known as AML.T0051. Notice that ID. You should always anchor your risk registers to the ID, not the name. Framework maintainers occasionally update technique names as technology evolves, but that ID remains stable over time. | Two overlapping boxes. Box 1 (faded): 'Name: LLM Prompt Injection'. Box 2 (bold, highlighted): 'ID: AML.T0051'. [CLICK:] A lock icon appears next to the ID with the label 'Stable over time', while a circular refresh icon appears next to the Name. Click to highlight the ID stability versus Name variability. |
| You might wonder when to use ATLAS compared to other frameworks like STRIDE-ML or LINDDUN. A common mistake is debating which one is best. They do not compete; they answer different questions at different stages. STRIDE-ML and LINDDUN act as architectural blueprints reviewed for security and privacy flaws before code ships. ATLAS is your fire marshal's report after deployment. | A horizontal timeline. Point 1: 'Before Deployment' branching to 'STRIDE-ML' and 'LINDDUN' with a blueprint icon. [CLICK:] Point 2: 'After Deployment' branching to 'MITRE ATLAS' with a fire marshal clipboard icon. Click to reveal the 'After Deployment' stage with ATLAS. |
| But here is the thing: a TTP is just a label. Its reality depends entirely on your specific architecture. Take AML.T0015, Evade AI Model. For a text-based chatbot, evasion looks like an adversarial text string bypassing a content filter. For a face-matching pipeline, evasion looks like a generative deepfake mask held up to a camera. Same ID, entirely different threat landscape. | Split screen layout with a central header: 'ID: AML.T0015 (Evade AI Model)'. Left side: 'Text Chatbot' pointing to an icon of a text bubble bypassing a digital shield. [CLICK:] Right side: 'Face-Matching' pointing to an icon of a deepfake mask held to a camera. Click to reveal the Face-Matching example. |
| So what does this mean for your daily work? ATLAS is an input, not an output. Your output is a scoped threat model row. You start with the ID, but then you must write the architectural scoping. Why does this threat matter to your system? Next, you score Likelihood and Impact to determine the Risk Level, and finally, map a specific mitigation. | A horizontal flowchart representing columns in a table. Node 1: 'ATLAS ID'. [CLICK:] Node 2: 'Architectural Scoping'. [CLICK:] Node 3: 'Likelihood + Impact = Risk Level'. [CLICK:] Node 4: 'Specific Mitigation'. Click to reveal each subsequent column in the threat model row. |
| Let us look at a high-autonomy feature: a chatbot with a new self-serve refund tool. Because it lives on a public web widget, the Likelihood of prompt injection is a five out of five. And since the LLM can autonomously invoke the refund tool to disburse company funds, the Impact of Financial Loss is a four out of five. That is a critical risk. | A 2-column equation layout. Left column: 'Public Web Widget' pointing to 'Likelihood: 5/5'. [CLICK:] Right column: 'Autonomous Refund Tool' pointing to 'Impact: 4/5 (Financial Loss)'. [CLICK:] Below both, a large bold red box appears labeled 'Risk Level: CRITICAL'. Click to reveal the Impact score; click to reveal the Critical risk level. |
| ATLAS will not tell you how to fix that vulnerability; that requires your architectural controls. We mitigate by layering defenses. You might put an input classifier before the prompt hits the model, and a server-side allowlist locking the refund tool to specific order IDs. Suddenly, your residual risk drops from critical to low, because the financial blast radius is bounded by code. | A linear flow diagram: 'User Input' -> 'AI Model' -> 'Refund Tool'. [CLICK:] A shield icon labeled 'Input Classifier' inserts itself between User Input and AI Model. [CLICK:] A lock icon labeled 'Server-Side Allowlist' inserts itself between AI Model and Refund Tool. [CLICK:] A green badge appears below reading 'Residual Risk: LOW'. Click to insert the Input Classifier; click to insert the Allowlist; click to show the dropped risk. |
| The biggest mistake teams make is treating a threat modeling framework like an exhaustive homework checklist. It is a vocabulary. You do not model every technique in the catalog; you identify the five that actually apply to the thing you are building. When was the last time you reviewed a risk register and realized it was missing the adversary's perspective entirely? | Headshot |
| Ultimately, your design-time findings and your runtime ATLAS findings converge into a single, well-owned risk register. This translates technical vulnerabilities into bounded business risks. By standardizing how you talk about threats, you give your leadership the exact clarity they need to make confident launch decisions. You are no longer just reacting to attacks; you are anticipating them with a shared language. | A funnel diagram. Top inputs: 'Design-time Findings' and 'Runtime ATLAS Findings'. [CLICK:] The funnel outputs to a single document icon labeled 'Single Risk Register'. [CLICK:] An arrow points from the register to a target icon labeled 'Bounded Business Risk & Confident Launch Decisions'. Click to show the funnel output; click to show the business outcome. |

## Module/Video #: Module 7 Video 1

### Title: threat_model_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 7 Video 2

### Title: threat_model (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 1

### Title: Understanding Regulatory Compliance for AI and the EU AI Act

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| Until recently, AI safety and security lived mostly inside engineering. You wrote a paper, you ran a benchmark, you tweeted about it. Now, there is a legal regulation stating exactly what your model must do before hitting the European market, backed by massive fines. Picture a product manager pitching an emotion-recognition module to detect frustrated users. Under the EU AI Act, that feature lands in prohibited categories if deployed in the wrong setting. The legal team steps in, and suddenly, your launch is dead. | HEADSHOT |
| This regulation, the EU AI Act, operates with serious extraterritorial reach. It sets up two main roles: the Provider who builds the system, and the Deployer who uses it professionally. You might think, my company is based entirely in the United States, so this does not apply to us. But if your AI system's outputs are used in the EU, you are in scope. Much like we saw with data privacy, this sets a global baseline. | Diagram with two labeled nodes: 'Provider (Builds AI)' and 'Deployer (Uses AI Professionally)'. An arrow points from a 'United States' icon to an 'European Union' icon labeled 'Outputs used in EU = In Scope'. [CLICK:] A shield icon appears labeled 'Global Baseline'. |
| So how does this actually work? The Act uses a risk-based framework. It does not regulate specific technologies like transformers; it regulates the use case. Think of it like city zoning. Some land is unrestricted, some requires basic permits, and some is strictly prohibited to build on. Your system gets classified into one of four risk tiers, and a single system can sit in multiple zones simultaneously depending on its features. | A 4-tier pyramid diagram representing the risk levels (Unacceptable, High, Limited, Minimal). Next to it, three 'City Zoning' icons: a green house (unrestricted), a yellow office (permits), and a red factory with a slash (prohibited). [CLICK:] An arrow points from a single 'AI System' node to multiple tiers on the pyramid, labeled 'Context-dependent'. |
| Let us look at the top tier: Unacceptable Risk. Article 5 defines AI practices that are flatly prohibited. This includes social scoring, untargeted facial-image scraping, and deploying emotion recognition in workplaces or schools. There is no compliance checklist for these. The mandate is simply that you must not deploy them. Remember that emotion-recognition feature your product manager wanted? That falls right here. | A large red stop sign icon labeled 'Unacceptable Risk (Article 5)'. Next to it, a 3-item list with 'X' icons: 'Social Scoring', 'Untargeted Facial Scraping', 'Emotion Recognition (Work/School)'. [CLICK:] A text label appears: 'No Checklist. Do Not Deploy.' |
| Next down is High-Risk, where most engineering and governance work lives. This is triggered by use cases listed in Annex III. If your system makes employment decisions, processes biometrics, or manages critical infrastructure, it lands here. For example, if you build an AI applicant screening tool and find an eight percent gender bias, you immediately trigger Annex III employment rules. Have you ever had to defend a model's output to someone who did not trust it? That is exactly the kind of scrutiny High-Risk systems face. | An orange warning triangle labeled 'High-Risk (Annex III)'. Three branching nodes: 'Employment Decisions', 'Biometrics', 'Critical Infrastructure'. [CLICK:] An example box appears under Employment: 'Applicant Screening Tool -> Scrutiny for Bias'. |
| If your system is High-Risk, a standard Model Card is not going to cut it anymore. Article 11 requires a massive stack of technical documentation drawn up before your system hits the market. You need a full risk management system, data governance proofs, human oversight designs, and a post-market monitoring plan. This is a heavy engineering lift, and each requirement has a named owner. | A 4-part block diagram representing a documentation stack (Article 11). Blocks labeled: 'Risk Management System', 'Data Governance Proofs', 'Human Oversight Designs', 'Post-Market Monitoring Plan'. [CLICK:] A user icon appears next to each block labeled 'Named Owner'. |
| Running alongside these four tiers is a separate track for General-Purpose AI, or GPAI. This covers foundation models. Say you integrate a large language model API into a dispatcher console for natural language queries. Even if the logistics query itself is not High-Risk, that GPAI deployment attaches specific upstream obligations. You have to handle transparency, copyright disclosure, and systemic risk evaluations. | A central node labeled 'Foundation Model (GPAI)'. An arrow points to a 'Dispatcher Console' node. [CLICK:] Three requirement tags attach to the GPAI node: 'Transparency', 'Copyright Disclosure', 'Systemic Risk Evals'. |
| Below that, we find Limited and Minimal Risk. Limited Risk is primarily about transparency. If users interact with a chatbot, they must be informed they are talking to an AI. Minimal Risk catches the rest, like spam filters or internal supply chain optimizers. These systems have no mandatory requirements, though voluntary codes of conduct are highly encouraged. | A two-column layout. Column 1: 'Limited Risk', showing a chatbot icon and a label 'Transparency: Must inform user'. Column 2: 'Minimal Risk', showing a spam filter icon and a label 'No mandatory requirements'. [CLICK:] A ribbon icon appears under Minimal Risk labeled 'Voluntary Codes of Conduct'. |
| Here is where it gets interesting: the exact same underlying technology can fall into entirely different risk tiers based on its context. An AI camera system optimizing delivery routes might be Minimal risk. But take that same AI camera and use it to monitor warehouse worker safety? You just triggered biometric and employment clauses, making it High-Risk. Context is everything. | A decision tree starting with an 'AI Camera System' node. It splits into two paths. Path A (top): 'Optimize Delivery Routes' leads to a green box 'Minimal Risk'. Path B (bottom): 'Monitor Worker Safety' leads to an orange box 'High-Risk (Biometrics/Employment)'. [CLICK:] A central label appears between the paths: 'Context is Everything'. |
| This classification dictates your operational reality. Take the Article 73 incident clock. If a High-Risk system malfunctions, a 15-day reporting clock starts the moment your company becomes aware. How fast can your on-call engineer escalate to the legal team? If your internal communication is slow, those 15 days are half-burned before the right people even know there is a problem. | A timeline with a stopwatch icon labeled 'Article 73 Incident Clock'. A starting point 'Awareness of Malfunction'. An endpoint '15 Days: Report Due'. [CLICK:] An escalation path appears below the timeline: 'On-call Engineer -> Legal Team', with a warning icon showing 'Slow internal comms burn time'. |
| The classification step is your entire compliance program in microcosm. Get it wrong, and every downstream engineering control is calibrated to the wrong risk. If an auditor walked into your office tomorrow and asked to see your documentation for a system you ship, what would they find? Your ability to map a system's features to its regulatory tier is the blueprint for your technical security roadmap. | HEADSHOT |

## Module/Video #: Module 9 Video 1

### Title: eu_ai_act_classifier_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 9 Video 2

### Title: compliance_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 9 Video 3

### Title: eu_ai_act_classifier (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 9 Video 4

### Title: compliance_plan (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
