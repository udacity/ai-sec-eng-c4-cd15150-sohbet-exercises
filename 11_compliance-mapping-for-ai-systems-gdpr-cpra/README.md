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

1. **Retention Schedule** — Define data categories, retention periods, legal bases, and deletion triggers for each data type.
2. **Privacy Controls** — Map data processing activities to GDPR articles, specify lawful bases, and document technical and organizational measures.

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
