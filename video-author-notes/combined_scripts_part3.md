| Program Info | Title | | Key |
| :---- | :---- | :---- | :---- |
| ND | AI Security Engineer (nd909) | | |
| Course | cd15150 — AI Security Strategy, Risk, Governance, and Compliance (GRC) | | |
| Modular content sequence *(if modular build)* | Part 3 of 3 | | |
| Production Tier | | | |
| **Build Team** | | **Production Requirements** | **Number of videos** |
| TCD | Prachi Dawer | Headshots + Slides | 3 |
| PgM | Ye Li | Slides | - |
| Producer | | Slides + Demo | - |
| Author name | Sohbet Dovranov | Demo | 5 |
| Author email | sohbetdovranov@gmail.com | Solution | 5 |
| | | Headshots + Demo | - |
| | | Headshots + Slides + Demo | - |
| | | Static graphics (not videos) | - |
| | | **TOTAL videos** | **13** |

## Module/Video #: Module 18 Video 1

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

## Module/Video #: Module 19 Video 1

### Title: model_card_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 19 Video 2

### Title: model_card (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 20 Video 1

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

## Module/Video #: Module 21 Video 1

### Title: fairness_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 21 Video 2

### Title: fairness_audit_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 22 Video 1

### Title: Understanding Data Retention and Privacy Compliance for AI Systems

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 23 Video 1

### Title: data_retention_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 23 Video 2

### Title: deletion_workflow_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 23 Video 3

### Title: deletion_workflow_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 23 Video 4

### Title: data_retention_solution (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 24 Video 1

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

## Module/Video #: Module 25 Video 1

### Title: governance_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 25 Video 2

### Title: ai_governance_core (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
