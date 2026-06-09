| Program Info | Title | | Key |
| :---- | :---- | :---- | :---- |
| ND | | | |
| Course | | | |
| Modular content sequence *(if modular build)* | Part X of Y | | |
| Production Tier | | | |
| **Build Team** | | **Production Requirements** | **Number of videos** |
| TCD | | Headshots + Slides | 11 |
| PgM | | Slides | 1 |
| Producer | | Slides + Demo | |
| Author name | | Demo | 17 |
| Author email | | Solution | 36 |
| | | Headshots + Demo | |
| | | Headshots + Slides + Demo | |
| | | Static graphics (not videos) | |

## Module/Video #: Module 1 Video 1

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

## Module/Video #: Module 2 Video 1

### Title: shap_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 2 Video 2

### Title: xai_audit_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 2 Video 3

### Title: xai_audit_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 3 Video 1

### Title: Understanding the NIST AI Risk Management Framework

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
## Module/Video #: Module 4 Video 1

### Title: risk_scoring_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 2

### Title: risk_assessment_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 3

### Title: risk_scoring

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 4

### Title: risk_assessment

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 5

### Title: risk_scoring

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 4 Video 6

### Title: risk_assessment

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 5 Video 1

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

## Module/Video #: Module 6 Video 1

### Title: threat_model_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 6 Video 2

### Title: threat_model_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 6 Video 3

### Title: threat_model

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 7 Video 1

### Title: Understanding Regulatory Compliance for AI and the EU AI Act

### Type (Production Requirements): Slides

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

## Module/Video #: Module 8 Video 1

### Title: eu_ai_act_classifier_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 2

### Title: compliance_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 3

### Title: eu_ai_act_classifier

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 4

### Title: compliance_plan

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 5

### Title: eu_ai_act_classifier

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 8 Video 6

### Title: compliance_plan

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 9 Video 1

### Title: Understanding the AI Policy Stack and Enforcement

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| Your company writes an AI Acceptable Use Policy. It looks fantastic. It bans pasting customer data into public LLMs and clearly lists sanctioned tools. But six months later, an engineer pastes a snippet of customer financial data into a public generative AI tool just to debug a regex. Why didn't the policy work? Because a policy without a binding technical control behind it is basically just a wish. And wishes do not show up in your security logs. | HEADSHOT |
| So, if a single perfect document is not enough, what do you actually need? You need a four-document stack. If you try to govern everything in one place, you end up with a contradicting mess nobody can navigate. Your stack needs the AUP for all employees, a Development Policy for your ML engineers, a Data Handling Policy for data owners, and a Procurement Policy for vendors. Each has a distinct audience and a specific binding mechanism. | 4-column layout. Column 1: AUP (Icon: Employees). Column 2: Development Policy (Icon: ML Engineers). Column 3: Data Handling Policy (Icon: Data Owners). Column 4: Procurement Policy (Icon: Vendors). [CLICK:] Reveal AUP (Employees); [CLICK:] Reveal Development Policy (ML Engineers); [CLICK:] Reveal Data Handling Policy (Data Owners); [CLICK:] Reveal Procurement Policy (Vendors) |
| Now, how do these four documents work together? The secret to a stack that works is the hand-off. Your AUP governs individual user behavior, like using public AI assistants. But it must explicitly name what it does not cover and where that issue goes. For instance, training data permissions get handed off to your Data Handling Policy. Without these explicit hand-offs, your policies will overlap and contradict each other. | Flowchart showing policy hand-offs. Node A on the left labeled AUP (Individual Behavior / Public AI). An arrow labeled Hand-off: Training Data Permissions points to Node B on the right labeled Data Handling Policy. [CLICK:] Show Node A (AUP); [CLICK:] Show Arrow (Hand-off); [CLICK:] Show Node B (Data Handling Policy) |
| Which brings us to the most important rule of AI governance: every single prohibited use needs a binding technical control. If your rule says, no customer data in public LLMs, but your enforcement is just trusting the employee handbook, you do not have a policy. You have a memo. Look at your current rules. If you cannot name the technical control that catches a violation in under thirty seconds, that rule is just decoration. | HEADSHOT |
| Let us trace an incident to see this in action. Consider an engineer trying to use an unsanctioned AI tool to debug a script containing sensitive financial data. Process controls, like annual training, will not physically stop this. You need technical controls. A preventive control, like a Data Loss Prevention tool or a browser-isolation proxy, physically blocks the request before it leaves your perimeter and logs the attempt. That is how you stop the breach. | Sequence diagram. Left: Engineer Node with Sensitive Data label. Right: Unsanctioned AI Tool Node. Middle: Preventive Control Node labeled DLP / Browser Proxy. An arrow goes from Engineer to Middle, but a red X blocks the path to the Right. A downward arrow from the Middle node points to a Log Database labeled Attempt Logged. [CLICK:] Show Engineer trying to send data to Unsanctioned AI Tool; [CLICK:] Insert Preventive Control (DLP/Proxy) in the middle; [CLICK:] Show Red X blocking the request and arrow logging the attempt |
| But you cannot just build a wall of no. A good policy must also guide employees on how to use AI safely. This means explicitly naming sanctioned tools that have contracts preventing data training. It also means giving your team simple verification steps. A great heuristic for employees is the Public Slack Channel Test. Ask yourself, would I post this prompt in a public company channel? If the answer is no, the AI tool is also no. | 2-column layout. Column 1: Sanctioned Tools (Icon: Green Check, Label: Contract prevents data training). Column 2: The Public Slack Channel Test (Icon: Chat bubble, Flow: Would I post this in public Slack? -> If No, then AI tool = No). [CLICK:] Reveal Sanctioned Tools column; [CLICK:] Reveal The Public Slack Channel Test column |
| Even with clear guidance, every policy generates exception requests. If you do not have a formal procedure, exceptions become ad-hoc emails. Those emails become tribal knowledge, and eventually, that tribal knowledge silently overwrites your policy. When was the last time you saw a temporary workaround become permanent just because nobody tracked it? You need a named workflow: Request, Security Triage, and formal Risk Acceptance by a named officer who signs off on the residual risk. | 3-step linear flow chart. Step 1: Request (Icon: Document). Arrow to Step 2: Security Triage (Icon: Shield). Arrow to Step 3: Risk Acceptance (Icon: Signature by Named Officer). [CLICK:] Show Step 1: Request; [CLICK:] Show Step 2: Security Triage; [CLICK:] Show Step 3: Risk Acceptance |
| And there is one final trap even with a formal process: the forgotten expiry date. Picture this: you grant an exception for a sales team to use an unsanctioned summarization tool just for one quarter. Without a hard expiry and re-review embedded in your control map, that three-month exception quietly becomes permanent shadow IT for half the organization. A single missing date can unravel your entire governance architecture. That is how policy drift happens, one forgotten expiry at a time. | Timeline diagram. Starts with Exception Granted node, arrow to a 3 Months duration, leading to a Hard Expiry & Re-Review node. A branching path below shows a Warning Icon labeled Missing Expiry leads to Permanent Shadow IT. [CLICK:] Show Exception Granted and 3-month timeline; [CLICK:] Show Hard Expiry and Re-Review node; [CLICK:] Show consequence branch for Missing Expiry becoming Permanent Shadow IT |

## Module/Video #: Module 10 Video 1

### Title: ai_policy_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 10 Video 2

### Title: ai_aup

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 10 Video 3

### Title: ai_aup

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 11 Video 1

### Title: Understanding AI Incident Response Playbook Design

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
## Module/Video #: Module 12 Video 1

### Title: incident_response_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 12 Video 2

### Title: incident_detection_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 12 Video 3

### Title: incident_response_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 12 Video 4

### Title: incident_response_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 12 Video 5

### Title: incident_detection_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 13 Video 1

### Title: Understanding AI Security Metrics and KRI Design

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| A CISO asks how your AI program is doing, and someone hands them a dashboard with forty-seven tiles, twelve colors, and three pie charts. After thirty seconds, they cannot tell whether anything is wrong. That dashboard is not a security program. It is a metrics museum. We need a small, actionable set of indicators that actually tell leadership if risks are managed. | Headshot |
| Let us get our vocabulary straight. A metric is just a number, like latency or accuracy. A Key Performance Indicator, or KPI, asks if your AI system is working as intended. But a Key Risk Indicator, a KRI, asks a different question: is a specific risk we are worried about actually materializing? The same number can be all three, depending on the conversation. | One shared number on the left ('Latency: 200ms') feeding three lenses. Lens 1: Metric (ruler icon, 'Just a number'). Lens 2: KPI (speedometer icon, 'Working as intended?'). Lens 3: KRI (warning-shield icon, 'Risk materializing?'). [CLICK:] Reveal KPI lens; [CLICK:] Reveal KRI lens |
| So, where do you find your KRIs? You do not pick them from a vendor catalog or default dashboard settings. Look at the dashboard your team uses today. For each tile, can you name the exact risk register row it derives from? If half the tiles fail that test, your metrics are just decoration. Every valid KRI traces directly back to your risk register. | Left: a Risk Register ledger with numbered rows. Right: dashboard tiles, each tied by a 'Direct Traceability' line back to a specific register row. [CLICK:] Untraceable tiles snap off and get a faded price-tag labeled 'Decoration', drifting away |
| To build an actionable KRI, you need six specific attributes. Missing even one turns your metric into a paperweight. You must define the exact input source, set clear thresholds, name a human owner, define an escalation path, choose a cadence, and write a board-facing narrative. Think of this like a recipe. If you leave out the baking powder, your cake will not rise. | A recipe card titled 'KRI Recipe' with 6 ingredients: Input Source, Thresholds, Human Owner, Escalation Path, Cadence, Board Narrative. [CLICK:] Reveal all 6 ingredients. [CLICK:] One ingredient is crossed out and a flat, un-risen cake icon appears labeled 'Will not rise' |
| Now, picking a number for your threshold is easy, but justifying it takes real work. A common mistake is basing green, amber, and red bands on gut feeling. Instead, anchor them in historical baselines or documented policy decisions. If your thresholds lack rationale, they lose all credibility the very first time they turn red. Why does this specific number matter to your business? | Horizontal threshold bar (Green, Amber, Red zones). [CLICK:] A 'gut feeling' thought-bubble over the boundaries is crossed out. [CLICK:] Two anchor icons drop onto the boundaries, labeled 'Historical Baseline' and 'Documented Policy' |
| Here is the thing: saying we will monitor this closely is not an escalation rule. Escalation means you know exactly who gets paged and what system changes happen when a threshold is breached. Does an amber state trigger a manual investigation? Does a red state force a hard change-freeze on your model? When was the last time a metric told your team exactly what to do? | Top node: 'Threshold Breached'. [CLICK:] Amber path -> a buzzing pager icon -> 'Manual Investigation'. [CLICK:] Red path -> a snowflake/freeze icon -> 'Hard Change-Freeze' on the model |
| Every KRI needs exactly one sentence that translates the raw metric into business meaning. Without it, the board sees a spike to eight percent and asks, So what? Your narrative is the answer. For an AI assistant, you might say, Has the assistant started refusing more than usual, and if so, is it policy drift or is someone probing for misuse? | Left: a metric gauge spiking to 8%, with a board-member icon and a 'So what?' speech bubble. A 'Translation' arrow points right. [CLICK:] Right: a Board Narrative card -> 'Policy drift, or someone probing for misuse?' |
| Check this out. A KRI is not a dashboard widget. It is a reproducible, unit-testable Python function. It ingests raw data and outputs a stable contract of four things: value, status, owner, and timestamp. This standard shape makes your KRIs tool-agnostic. Your dashboard is really just a thin presentation layer sitting on top of this audited code library. | Pipeline. Left: Raw Data. Middle: a Python function block (gear) with a green unit-test checkmark badge. Right: an 'Output Contract' card listing Value, Status, Owner, Timestamp. [CLICK:] Reveal the Output Contract. [CLICK:] A thin dashboard strip slides on top labeled 'Presentation layer only' |
| You also need to balance leading and lagging indicators. Lagging indicators tell you the damage is done, like incident counts or regulatory fines. Leading indicators tell you the conditions for risk are present right now, like a creeping feature drift score or an uptick in jailbreak attempts. You want both, but leading indicators actually give you the time to defend your system before disaster strikes. | Timeline with a central 'Risk Event' burst. Left (before): Leading Indicators -> a drift-score gauge and a jailbreak-attempt icon, with a clock labeled 'Time to defend'. Right (after): Lagging Indicators -> an incident-count tally and a gavel icon for fines. [CLICK:] Reveal Leading side; [CLICK:] Reveal Lagging side |
| Five is roughly the right number for a leadership dashboard. You cover the major risk categories without building a museum. A balanced portfolio includes subgroup false negative rates for fairness, drift scores for validity, jailbreak hit rates for adversarial misuse, vendor SLA breach rates for third-party risk, and threat model coverage. Notice how you mix system-level metrics with broad portfolio-level metrics. | A clean dashboard of exactly 5 tiles (callback: not the 47-tile museum). Tiles with icons: Fairness (scales, 'Subgroup FNR'), Validity (drift-arrow, 'Drift Score'), Adversarial (shield, 'Jailbreak Hit Rate'), Third-Party (handshake, 'Vendor SLA'), Coverage (grid-map, 'Threat Model'). [CLICK:] Reveal system-level tiles 1-3; [CLICK:] Reveal portfolio-level tiles 4-5 |
| Ultimately, the true test of your AI governance program is not how beautiful the dashboard looks on a monitor. The test is whether a red indicator wakes your team up at night with the exact context you need to stop a prompt-injection campaign. Five KRIs that you act on will always beat fifty metrics that you only admire. | Headshot |

## Module/Video #: Module 14 Video 1

### Title: kri_calculator_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 2

### Title: kri_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 3

### Title: kri_definitions

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 4

### Title: kri_calculator_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 5

### Title: kri_definitions

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 6

### Title: kri_calculator_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 15 Video 1

### Title: Understanding Third-Party AI Model Risk

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
## Module/Video #: Module 16 Video 1

### Title: vendor_governance_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 2

### Title: vendor_risk_scoring_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 3

### Title: vendor_risk_scoring_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 4

### Title: vendor_governance_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 5

### Title: vendor_risk_scoring_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 6

### Title: vendor_governance_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 17 Video 1

### Title: Understanding AI Transparency Documentation

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| Six months after launch, a regulator emails you. They want the technical documentation for your AI system under EU AI Act Article 11. You quickly forward your Model Card. They reply: 'This is one document. Article 11 references Annex IV. Where is the rest?' That is the exact moment many teams discover that having a Model Card is not the same as having transparency documentation. | HEADSHOT |
| So what are they actually looking for? Transparency documentation is a stack, much like an architect's drawing set. A structural drawing alone isn't enough for a building inspector; they need the whole set. For AI, you need four pieces. You have your Model Card describing the model itself, a Datasheet for the training data, a System Card for the deployed architecture, and an Impact Assessment for broader harms. | A vertical stack diagram labeled Transparency Documentation Stack. Top to bottom: Model Card (The Model), Datasheet (Training Data), System Card (Deployed Architecture), Impact Assessment (Broader Harms). [CLICK:] Reveal Model Card (The Model); [CLICK:] Reveal Datasheet (Training Data); [CLICK:] Reveal System Card (Deployed Architecture); [CLICK:] Reveal Impact Assessment (Broader Harms) |
| Now, here is where it gets interesting. You have to communicate the exact same technical truth to three very different audiences without contradiction. Your internal engineers need brutal honesty about residual risks. Your customers need clear integration guardrails and failure modes. And your regulators? They need formal statutory anchors mapping directly to the law. Have you ever tried explaining the exact same technical failure to a developer and a lawyer? | A central node labeled Technical Truth splitting into three branches. Branch 1: Internal Engineers (Hardhat icon) with text Residual Risks. Branch 2: Customers (User icon) with text Guardrails & Failure Modes. Branch 3: Regulators (Scales of Justice icon) with text Statutory Anchors. [CLICK:] Reveal Internal Engineers branch; [CLICK:] Reveal Customers branch; [CLICK:] Reveal Regulators branch |
| Let us look at your Model Card itself, using a code-completion model called CodeAssist-7B as an example. The card establishes identity, intended use, and limitations for your users. It clearly defines out-of-scope uses, explicitly stating this model is not for generating safety-critical medical firmware. It also breaks down performance metrics by subgroup to expose hidden fairness gaps, rather than just reporting top-line accuracy. | A mock document layout labeled CodeAssist-7B Model Card. Three highlighted sections. Section 1: Identity & Intended Use. Section 2: Out-of-Scope Uses (e.g., Medical Firmware). Section 3: Subgroup Performance Metrics (with a small bar chart icon highlighting Fairness Gaps). [CLICK:] Reveal Section 1 Identity & Intended Use; [CLICK:] Reveal Section 2 Out-of-Scope Uses; [CLICK:] Reveal Section 3 Subgroup Performance Metrics |
| But wait, what about security? This section is absolutely vital for your downstream deployers. You must document specific attack vectors and pair every single threat with an implemented mitigation, like an output filter. Critically, you also have to document the residual risk and the qualitative findings from your red-team exercises. Downstream users rely on this information to build safe systems. | A 3-column flow diagram. Column 1: Attack Vectors (Bug icon). Column 2: Mitigations (Shield icon, Label: e.g., Output Filter). Column 3: Residual Risk & Red-Team Findings (Clipboard icon). Arrows connect Column 1 to 2, and 2 to 3. [CLICK:] Reveal Attack Vectors; [CLICK:] Reveal Mitigations; [CLICK:] Reveal Residual Risk & Red-Team Findings |
| When you are documenting these security threats, vague terms like 'jailbreak' or 'data leak' create confusion. Instead, use the MITRE ATLAS framework as your Rosetta Stone. By using stable technique IDs like AML.T0051 for prompt injection, you provide an authoritative, unambiguous taxonomy. Even if a technique name changes in a future update, your ID remains a stable anchor for downstream threat modeling. | A translation table graphic. Left side: Vague Terms (Red cross icon) with labels Jailbreak, Data Leak. Right side: MITRE ATLAS (Green check icon) with stable IDs like AML.T0051 (Prompt Injection). An arrow points from left to right emphasizing standardization. [CLICK:] Reveal Left side Vague Terms; [CLICK:] Reveal Right side MITRE ATLAS Taxonomy |
| You might think it looks good to write 'no known vulnerabilities' on your Model Card, but actually, that is a red flag. A Model Card whose security section claims no known issues is usually from a team that simply did not try hard enough. Honest limitations build trust with sophisticated reviewers. Confident silence breaks it. Explicitly documenting patched vulnerabilities proves you rigorously tested the system. | Two contrasting Model Card security sections. Left: Claim: No Known Vulnerabilities with a large Red Flag icon. Right: Documented: Patched Vulnerabilities & Honest Limitations with a Shield Check icon and text Builds Trust & Proves Rigorous Testing. [CLICK:] Reveal Left side Red Flag; [CLICK:] Reveal Right side Documented Patched Vulnerabilities |
| So how does this tie back to that regulator's email? To satisfy compliance, you must map your transparency stack directly to statutory mandates using a crosswalk. Regulatory texts like the EU AI Act have specific requirements housed in annexes, like Annex IV. Your crosswalk proves exactly which paragraph of the law is satisfied by which specific section of your documentation. | A bipartite matching diagram (Crosswalk). Left side: Transparency Documentation (Model Card, System Card). Right side: EU AI Act Mandates (Article 11, Annex IV, Paragraph 2). Lines connect specific sections on the left to specific legal paragraphs on the right. [CLICK:] Reveal lines mapping documentation sections to statutory paragraphs |
| Check this out, though. No transparency stack is ever completely finished on day one. A mature compliance program uses a Gap Log to track what is missing, rather than papering over it. If your Model Card defers training data details, your Gap Log assigns that requirement to the Datasheet, names an owner, and sets a target date for completion. | A simple table diagram labeled Gap Log. Columns: Missing Requirement (e.g., Training Data Details), Assigned Document (e.g., Datasheet), Owner, Target Date. A single filled row demonstrates the example. [CLICK:] Reveal the Missing Requirement column; [CLICK:] Reveal the Assigned Document, Owner, and Target Date columns |
| Early in my career, I left the caveats section of a model card blank because I did not want to scare off a potential customer. Three months later, that customer integrated the model and hit exactly the catastrophic failure mode I had been afraid to document. When was the last time you withheld a known flaw just to make something look better? Transparency is about proving your model is understood. | HEADSHOT |

## Module/Video #: Module 18 Video 1

### Title: model_card_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 18 Video 2

### Title: model_card

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 18 Video 3

### Title: model_card

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 19 Video 1

### Title: Understanding Bias and Fairness Auditing for AI Governance

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| Your loan-approval model returns a demographic-parity ratio of 0.78. Is it launchable? An engineer says yes, it is the best model yet. A lawyer says absolutely not; the EEOC sets the floor at 0.80. A product manager says it depends on the accuracy cost to fix it. They are all right. But none of them is the AI Risk Officer. Your job is the interpretation layer: translating that 0.78 into a defensible launch decision. | Central node labeled '0.78 Demographic Parity' with three upward branches and one downward branch. Left branch: Gear icon labeled 'Engineer: Yes - Best Model'. Middle branch: Scales of justice icon labeled 'Lawyer: No - EEOC floor 0.80'. Right branch: Bar chart icon labeled 'PM: Depends - Accuracy cost'. Downward branch: Shield icon labeled 'AI Risk Officer: Interpretation Layer'. [CLICK:] Show central node '0.78'; [CLICK:] Reveal Engineer branch; [CLICK:] Reveal Lawyer branch; [CLICK:] Reveal Product Manager branch; [CLICK:] Reveal AI Risk Officer branch at the bottom. |
| Before fixing that 0.78, you need to know where bias originates. Production bias is rarely just bad data. Data bias encodes historical inequities into your labels. Algorithmic bias happens when optimization choices erase minority signals. Deployment bias pops up when your system is used in a context it was never designed for. Most failures are a messy mixture of all three. | A 3-step horizontal flow diagram representing the ML lifecycle. Box 1: 'Data Bias' with sub-label 'Historical inequities in labels'. Box 2: 'Algorithmic Bias' with sub-label 'Optimization erases minority signals'. Box 3: 'Deployment Bias' with sub-label 'Used in unintended context'. A bracket below all three boxes connects to a label 'Messy Mixture'. [CLICK:] Reveal Box 1 (Data Bias); [CLICK:] Reveal Box 2 (Algorithmic Bias); [CLICK:] Reveal Box 3 (Deployment Bias); [CLICK:] Reveal bottom bracket and 'Messy Mixture' label. |
| You might think, I will just remove protected attributes like race or gender from my inputs. Problem solved, right? Actually, this is a known failure mode called fairness through unawareness. Your model will simply find proxy variables, using a ZIP code to infer race, or a surname to guess socioeconomic class. The real work is mitigating these proxy effects, not pretending the attribute does not exist. | Diagram showing a list of inputs feeding into a central 'Model' box. The input 'Protected Attribute: Race/Gender' is crossed out with a red X. Two other inputs, 'ZIP Code' and 'Surname', have curved dashed arrows labeled 'Proxy' sneaking into a hidden 'Race/Class' node inside the model. A bold warning label reads 'Fairness through Unawareness'. [CLICK:] Show inputs with 'Protected Attribute' crossed out; [CLICK:] Reveal 'ZIP Code' and 'Surname' inputs; [CLICK:] Reveal dashed 'Proxy' arrows and the hidden node inside the model. |
| To detect those effects, you need three core metrics. Demographic Parity asks if different groups receive positive outcomes at the same rate, often anchoring to external regulations like that 0.80 floor. Equalized Odds and Equal Opportunity look at your error rates, specifically true positive and false positive rates. These are typically bound by internal firm-policy ceilings, often set tight around 0.10. | A 3-column comparative layout. Column 1: 'Demographic Parity' with label 'Equal positive outcome rates' and 'Floor: 0.80'. Column 2: 'Equal Opportunity' with label 'True Positive Rates'. Column 3: 'Equalized Odds' with label 'True & False Positive Rates' and 'Ceiling: 0.10'. [CLICK:] Reveal Column 1 (Demographic Parity); [CLICK:] Reveal Column 2 (Equal Opportunity); [CLICK:] Reveal Column 3 (Equalized Odds). |
| Now, a common mistake is starting an audit by just importing a black-box fairness library. Do not do that. You want to compute your metrics manually from foundational confusion-matrix primitives first. Calculate your true positive and false positive rates yourself. When you understand exactly how those rates interact, you never get confused later. Once you have built that intuition, you can use industry libraries like Fairlearn as a simple one-line cross-check to validate your math. | A two-step flowchart. Step 1: A 2x2 Confusion Matrix grid labeled TP, FP, TN, FN, with an arrow pointing to a clipboard icon labeled 'Manual Rate Calculation'. Step 2: A box labeled 'Fairlearn Library' with a green checkmark, acting as a cross-check validation pointing back to the manual calculation. [CLICK:] Show Confusion Matrix; [CLICK:] Reveal arrow and 'Manual Rate Calculation'; [CLICK:] Reveal 'Fairlearn Library' box and checkmark for validation. |
| Here is where it gets interesting. Mathematically, models generally cannot satisfy all three fairness metrics at the same time when base rates are unequal. This is the impossibility trilemma. Pushing one metric inside its policy bound almost always pushes another outside. You cannot pass every metric. You have to pick which one matters most. When was the last time you had to defend a trade-off like that? | A triangle diagram representing the Trilemma. The three vertices are labeled 'Demographic Parity', 'Equal Opportunity', and 'Equalized Odds'. In the center of the triangle, a node reads 'Base Rates Unequal'. Red arrows push outward from the center to the vertices, illustrating the tension and trade-offs between the corners. [CLICK:] Show triangle with the three metric vertices; [CLICK:] Reveal central text 'Base Rates Unequal'; [CLICK:] Reveal outward pushing arrows showing trade-offs. |
| Once you pick your metric, you have to mitigate the bias. You can intervene at the data stage, the training stage, or the output stage. A very common post-processing technique is applying separate decision thresholds for different demographic groups. But every intervention has a cost. Improving your fairness metric inherently trades off against overall model accuracy. You have to quantify that cost. What is the accuracy drop required to bring your worst metric inside policy bounds? | A line graph with two intersecting curves. X-axis: 'Fairness Intervention Strength'. Y-axis left: 'Fairness Metric' (line goes up). Y-axis right: 'Model Accuracy' (line goes down). Below the chart, three chevron arrows point right: 'Data', 'Training', 'Output (Per-group thresholds)'. [CLICK:] Show the three mitigation stages (Data, Training, Output); [CLICK:] Reveal the graph axes; [CLICK:] Reveal the intersecting Fairness and Accuracy lines. |
| This brings us back to your role. Producing the audit numbers is the machine learning engineer's job. Translating them into action is your job. Choosing which metric to prioritize depends on the population at risk, the harm if the model is wrong, and the regulatory environment. Have you ever seen a team optimize a metric they could not defend to a regulator? The room where fairness gets settled is the AI review board, not the engineering standup. Evidence is just numbers; the decision requires your human judgment. | Headshot |
| So what happens when that demographic-parity ratio is sitting at 0.78? A sub-policy metric does not automatically mean a no-go. Often, it results in a Conditional Launch memo. This memo details exact mitigation controls, like applying per-group thresholds. It outlines a strict ongoing monitoring cadence, perhaps 90-day reviews, and clear escalation paths if metrics slip. You are not just saying yes or no; you are defining the exact conditions under which the model is safe to operate. | A central document icon labeled 'Conditional Launch Memo'. Three callout boxes connect to it. Callout 1: 'Mitigation Controls (e.g., Thresholds)'. Callout 2: 'Monitoring Cadence (90-day reviews)'. Callout 3: 'Escalation Paths'. [CLICK:] Show Memo document icon; [CLICK:] Reveal Mitigation Controls; [CLICK:] Reveal Monitoring Cadence; [CLICK:] Reveal Escalation Paths. |
| And this framework is not just for traditional models. The mechanics of fairness auditing do not vanish when you switch to generative AI. Whether you are auditing a binary classifier for loans or a large language model acting as a resume screener, the core primitives transfer perfectly. Ultimately, fairness governance is about measuring and mitigating human impact, regardless of the underlying technical surface. That is how you turn abstract principles into defensible, real-world AI decisions. | A split-screen comparison. Left side: 'Traditional AI' with a decision tree icon and label 'Loan Approval'. Right side: 'Generative AI' with a chat bubble icon and label 'Resume Screener'. A large bracket encompasses both sides, pointing down to a single foundation box labeled 'Core Primitives & Human Impact'. [CLICK:] Show Traditional AI side; [CLICK:] Show Generative AI side; [CLICK:] Reveal the bracket and bottom foundation box. |

## Module/Video #: Module 20 Video 1

### Title: fairness_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 20 Video 2

### Title: fairness_audit_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 20 Video 3

### Title: fairness_audit_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 21 Video 1

### Title: Understanding Data Retention and Privacy Compliance for AI Systems

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
## Module/Video #: Module 22 Video 1

### Title: data_retention_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 2

### Title: deletion_workflow_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 3

### Title: data_retention_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 4

### Title: deletion_workflow_starter

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 5

### Title: deletion_workflow_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 6

### Title: data_retention_solution

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 23 Video 1

### Title: Understanding the AI Governance Operating Model

### Type (Production Requirements): Headshots + Slides

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| A CTO walks into an executive offsite and announces, 'We have AI governance. We have a policy, and a review board.' Sounds great, right? But six months later, two major product launches slip because nobody can approve them in time. The so-called board turned out to be a calendar invite nobody attended. The policy was an unopened PDF. That is not governance. That is the shape of governance with no operating model behind it. Governance isn't just a meeting. It's an authority structure that meets. | Headshot |
| How do you build a real authority structure? You need five pillars: Scope, Membership, Cadence, Reporting, and Decision Rights. That fifth pillar is what holds the roof up. Without decision rights, your operating model is purely decorative. When was the last time you sat in a meeting where everyone discussed an issue for an hour, but nobody actually made a call? | 5-pillar diagram supporting a roof labeled 'AI Governance'. Pillars labeled: 1. Scope, 2. Membership, 3. Cadence, 4. Reporting, 5. Decision Rights. Pillar 5 is visually distinct. [CLICK:] Reveal pillars 1-4; [CLICK:] Reveal pillar 5 (Decision Rights) with a glowing highlight. |
| That exact scenario is why most AI charters fail. They are heavy on scope but blank on decision rights. Without explicit rules, a board just talks. Months later, nobody knows if a system was actually approved. To fix this, you need brutal specificity. You must write down exactly who approves, who recommends, who is consulted, and who is informed. It turns a conversation into an actual decision. | Two contrasting flowcharts. Left: 'Without Decision Rights' showing a circle of people with speech bubbles and a question mark. Right: 'With Decision Rights' showing 4 distinct roles with icons: Approve (Checkmark), Recommend (Arrow), Consult (Chat), Inform (Broadcast). [CLICK:] Show the 'Without Decision Rights' loop; [CLICK:] Reveal the 'With Decision Rights' breakdown. |
| What exactly are they deciding? An effective operating model explicitly assigns accountability for five canonical AI decisions. First, launch approval: does this system go to production? Second, retraining sign-off: does this update ship? Third, vendor onboarding. Then you have reactive and proactive triggers. Incident escalation: when does an operational issue become a board-level problem? Finally, red-team commissioning: who orders adversarial testing, and who signs off on fixes? | 5-step horizontal list with icons. 1. Launch Approval (Rocket). 2. Retraining Sign-off (Recycle arrows). 3. Vendor Onboarding (Handshake). 4. Incident Escalation (Warning triangle). 5. Red-Team Commissioning (Target/Shield). [CLICK:] Reveal Launch Approval; [CLICK:] Reveal Retraining Sign-off; [CLICK:] Reveal Vendor Onboarding; [CLICK:] Reveal Incident Escalation; [CLICK:] Reveal Red-Team Commissioning. |
| To keep track of all this, you will use a RACI matrix. Think of this as the constitution of your operating model. But here is the golden rule you must follow: every single decision type must have exactly one Accountable owner. Just one. If you have zero accountable people, the decision stalls. If you have two, everyone assumes the other person is handling it. The accountability has to stop with one specific, named role. | A simplified RACI matrix grid. Rows: Launch, Retrain, Vendor. Columns: Board, Product Lead, Risk Officer. Cells filled with R, A, C, I. A bright red circle drawn around a single 'A' in the Launch row. [CLICK:] Reveal the RACI grid structure; [CLICK:] Highlight the single 'A' to emphasize the golden rule. |
| Now, you might wonder, should one central board own all these decisions? If a single AI review board handles everything across your organization, they become a massive bottleneck. A six-week queue forms, and your launches slip. But if you completely federate governance to individual business units, you end up with inconsistent, fragmented standards. The mature pattern is hybrid. You centralize high-stakes decisions, like high-risk launches, and you federate operational decisions, like standard retrains, right back to the business lines. | 3-column layout. Left: 'Centralized' (Single large node with many arrows pointing to it, labeled 'Bottleneck'). Right: 'Federated' (Disconnected small nodes, labeled 'Fragmented'). Center: 'Hybrid' (One central node connected to structured sub-nodes, labeled 'High-Stakes Centralized / Operational Federated'). [CLICK:] Show Centralized bottleneck; [CLICK:] Show Federated fragmentation; [CLICK:] Reveal Hybrid model in the center. |
| Speaking of high-stakes decisions, let us look at red-teaming. Proactive adversarial testing, like prompt-injection exercises, cannot be just a one-off event you do for a launch. It has to be strictly governed. The board must explicitly commission the test and mandate independent operation. And here is the best part: governance enforces the outcome. Any open critical findings must automatically block a new launch or retrain until that specific remediation is signed off. | Flowchart showing the Red-Team process. Node 1: 'Board Commissions Test'. Arrow to Node 2: 'Independent Execution'. Arrow splits based on 'Critical Findings?'. Yes points to 'Block Launch/Retrain' (Stop sign icon). No points to 'Proceed' (Checkmark icon). [CLICK:] Show Board Commissioning and Independent Execution; [CLICK:] Reveal the conditional split blocking launch if critical findings exist. |
| All these decisions must be visible. Your governance needs to be legible through structured outputs, like monthly board updates. These artifacts map directly to external standards like the NIST AI Risk Management Framework and ISO 42001. Above it all sits the principle of effective challenge, meaning your validation process is meaningfully independent from development. This is a gold-standard pattern you will see everywhere. | A mapping diagram. Left side: 'Structured Outputs' (document icons labeled Monthly Board Updates). Arrows pointing to Right side: 'External Standards' (badges labeled NIST AI RMF, ISO 42001). An overarching layer labeled 'Effective Challenge'. [CLICK:] Reveal Structured Outputs; [CLICK:] Draw mapping arrows to External Standards; [CLICK:] Reveal the 'Effective Challenge' overarching layer. |
| Even with all this in place, the first version of your operating model will have gaps. You will find decision bottlenecks or realize a policy only exists on paper. For example, maybe your incident escalation path relies on a chair who is asleep at 3 a.m. When you find these gaps, you update the model. You keep a formal Iteration Log to document how your governance evolves based on operational evidence, proving to auditors that it is a living system. | Circular iteration cycle diagram. Nodes: 'Deploy Model', 'Identify Gaps', 'Update Model'. In the center, a clipboard icon labeled 'Formal Iteration Log'. [CLICK:] Reveal the iteration cycle; [CLICK:] Show the 'Formal Iteration Log' in the center. |
| So, let me leave you with the ultimate test of your operating model. Picture your team's last AI launch. Walk back the decision chain. Who actually approved it? In what specific artifact is that approval recorded? If you cannot answer that question with a name, a date, and a log entry in under thirty seconds, you have governance ambition. You don't have an operating model. Now you know exactly how to build one that actually works. | Headshot |

## Module/Video #: Module 24 Video 1

### Title: governance_demo

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 24 Video 2

### Title: ai_governance_core

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 24 Video 3

### Title: ai_governance_core

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
