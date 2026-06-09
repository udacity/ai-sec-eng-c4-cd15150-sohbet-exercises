| Program Info | Title | | Key |
| :---- | :---- | :---- | :---- |
| ND | AI Security Engineer (nd909) | | |
| Course | cd15150 — AI Security Strategy, Risk, Governance, and Compliance (GRC) | | |
| Modular content sequence *(if modular build)* | Part 2 of 3 | | |
| Production Tier | | | |
| **Build Team** | | **Production Requirements** | **Number of videos** |
| TCD | Prachi Dawer | Headshots + Slides | 2 |
| PgM | Ye Li | Slides | - |
| Producer | | Slides + Demo | - |
| Author name | Sohbet Dovranov | Demo | 6 |
| Author email | sohbetdovranov@gmail.com | Solution | 7 |
| | | Headshots + Demo | - |
| | | Headshots + Slides + Demo | - |
| | | Static graphics (not videos) | - |
| | | **TOTAL videos** | **15** |

## Module/Video #: Module 10 Video 1

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

## Module/Video #: Module 11 Video 1

### Title: ai_policy_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 11 Video 2

### Title: ai_aup (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 12 Video 1

### Title: Understanding AI Incident Response Playbook Design

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 13 Video 1

### Title: incident_response_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 13 Video 2

### Title: incident_response_solution (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 13 Video 3

### Title: incident_detection_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 14 Video 1

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

## Module/Video #: Module 15 Video 1

### Title: kri_calculator_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 15 Video 2

### Title: kri_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 15 Video 3

### Title: kri_definitions (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 15 Video 4

### Title: kri_calculator_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 16 Video 1

### Title: Understanding Third-Party AI Model Risk

### Type (Production Requirements): **REUSE FROM DATA GOV**

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 17 Video 1

### Title: vendor_governance_demo (Excel)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 17 Video 2

### Title: vendor_risk_scoring_demo (Notebook)

### Type (Production Requirements): Demo

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 17 Video 3

### Title: vendor_risk_scoring_solution (Notebook)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |

## Module/Video #: Module 17 Video 4

### Title: vendor_governance_solution (Excel)

### Type (Production Requirements): Solution

| Script *(one row per slide)* | Guidance for Complex Visuals |
| :---- | :---- |
| | |
| | |
| | |
| | |
| | |
