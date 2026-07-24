# Compliance Mapping for AI Systems (GDPR/CPRA)

> **Maintainer note:** When importing this content into the classroom, omit the H1 above — the classroom adds its own page title.

This lesson covers data retention policies and privacy compliance, with a focus on GDPR Article 17 (right to erasure). Students learn to implement automated deletion workflows, assess model-data lineage impact, select appropriate deletion methods, and generate audit trails for compliance documentation.

## File Structure

```
11_compliance-mapping-for-ai-systems-gdpr-cpra/
├── demo/
│   ├── data_retention_demo.xlsx      # Filled-in instructor reference
│   └── deletion_workflow_demo.ipynb           # Notebook walkthrough for deletion workflows
├── exercises/
│   ├── starter/
│   │   ├── data_retention_starter.xlsx        # Student starting file (with hints)
│   │   └── deletion_workflow_starter.ipynb    # Notebook with TODO placeholders
│   └── solution/
│       ├── data_retention_solution.xlsx        # Completed solution
│       └── deletion_workflow_solution.ipynb    # Completed notebook
└── README.md
```

## Demo

**Scenario: PharmaSafe AI** — A pharmaceutical company managing clinical trial data subject to GDPR and FDA retention requirements.

The instructor walks through data retention policy concepts live, filling in retention schedules and privacy controls. The notebook demonstrates a single GDPR right-to-be-forgotten request for one clinical trial participant (SUBJ-5001): inventorying 4 data records, checking model-data lineage across 2 production models (Adverse Event Detector, Signal Detection), executing deletions with method selection (secure erase for sensitive data, standard delete otherwise), and generating a chronological audit trail and compliance summary.

## Exercise

**Scenario: HealthBridge AI** — A healthcare AI company processing patient data across multiple models and data stores, triggered by a patient's right-to-be-forgotten request.

### Task

**Part 1 — Data Retention Policy (Excel)**

1. **Retention Policy** — Define retention periods, legal bases, deletion triggers, and archival rules for the 12 data categories.
2. **Deletion Workflow** — Complete the 10-step GDPR erasure-request workflow, from request intake through deletion certification.
3. **Retraining Triggers** — Document the retraining triggers that map deleted data to the models trained on it.
4. **Audit Trail Requirements** — Specify the 8 audit event types with their required fields, retention, and access controls.

**Part 2 — Deletion Workflow (Notebook)**

Data is provided inline: 11 records across 2 subjects (9 for SUBJ-10001, 2 for SUBJ-10002), a model-data lineage map for 6 production models (Clinical Summary Model, Diagnosis Predictor, Risk Stratification, Treatment Recommender, Query Intent Classifier, Adverse Event Detector), and pre-built deletion request processing infrastructure.

1. **Deletion Method Selection** — Implement a function that chooses the appropriate method (Secure Erase, Cryptographic Erasure, Standard Delete, or Archival) based on data sensitivity, storage type (cloud vs. database), and record type (consent records → archival).
2. **Model Impact Assessment** — Implement a function that cross-references deleted data types against each model's training data dependencies and determines retraining priority (HIGH / MEDIUM / LOW) based on model impact level and production status.
3. **Deletion Pipeline Integration** — Complete two TODO sections within the `process_deletion_request()` function: execute deletion for each record using the method selector, and assess model impact using the impact assessment function.
4. **Run Three Scenarios** — Process deletion requests for: (a) a patient with extensive data and training dependencies, (b) a patient with limited records, and (c) a non-existent subject — observing how the pipeline handles each case.
5. **Model Lineage Impact Report** — Review the model-data impact matrix showing affected models, overlap data types, retraining requirements, and priority levels.
6. **Audit Trail** — Review the chronological audit log documenting all deletion events for regulatory compliance.

### Color Guide

| Color | Cell Text | Meaning |
|-------|-----------|---------|
| Light blue | Pre-filled data | Pre-filled content — do not modify |
| Pink | Contains `[Your response here]` prompts | Your work area — fill these cells |
| Yellow | Contains reference text (read-only) | Reference material — do not edit |
| Green | Scenario description | Scenario brief context |


## Reference Notes

A few specification details for learners cross-referencing the GDPR citations used in this lesson.

- **Article 6 lawful bases — six total.** GDPR Article 6(1) lists six lawful bases for processing personal data: (a) consent, (b) contract, (c) legal obligation, (d) vital interests, (e) public task, and (f) legitimate interest. Where the materials list four bases as a quick reference, the full statutory list is the six above. See [GDPR Article 6](https://gdpr-info.eu/art-6-gdpr/).
- **Deletion response timeline.** The default response window for a data-subject request (including erasure under Art. 17) is **one month** under [Art. 12(3)](https://gdpr-info.eu/art-12-gdpr/), extendable by up to two further months for complex / numerous requests with notice to the data subject. Article 33 (72-hour breach notification to the supervisory authority) and Article 34 (breach communication to data subjects) cover personal-data breach incidents, which is a separate workflow from a routine deletion request. Where a deletion request escalates to the supervisory authority, the route is through [Art. 77](https://gdpr-info.eu/art-77-gdpr/) (right to lodge a complaint).
- **Article 5(1)(f) — integrity and confidentiality.** The integrity / confidentiality principle is at Art. 5(1)(f); subsection notation in references should follow the §1(letter) form used elsewhere in the workbook.
- Citation anchors: the 25-year clinical-trial archiving period stems from EU CTR 536/2014 Art. 58 (ICH-GCP E6(R3) defers to applicable regulatory requirements); HIPAA's six-year rule (45 CFR 164.316) covers Security-Rule documentation; GDPR sets no fixed audit-log period — longer retention (e.g., 7 years) is an internal standard.
- Where a record carries a mandatory-retention hold (e.g., FDA/EMA safety data), GDPR Art. 17(3)(b) permits retention: archive and restrict access rather than erase — the exercise workflow demonstrates this path. The compliance summary's per-disposition counts (deleted / archived / legal hold) are the authoritative tally.
- The deletion workflow documents five retraining triggers.
