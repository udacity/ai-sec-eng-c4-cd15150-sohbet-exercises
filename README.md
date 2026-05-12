# Purpose of This Repo

This repo is the source of truth for all exercises in this course — AI Security Strategy, Risk, Governance, and Compliance (GRC).

> IMPORTANT!  Please remove these instructions before sharing this repo with learners.

## Folder Structure

The repo contains one folder per module. Each module folder is self-contained and reads as a standalone exercise, with its own `README.md`, demo materials, and starter/solution artifacts.

```bash
ai-sec-eng-c4-cd15150-sohbet-exercises/
├── README.md
├── LICENSE.md
├── CODEOWNERS
├── requirements.txt
├── Module_Dictionary_AI_Security_ND.xlsx
├── Exercise Creation Resources/
│   ├── Exercise Guidance.md
│   ├── Accessibility Standards.md
│   ├── Real-World Content Guidelines.md
│   └── Third Party Images and Datasets.md
├── 01_explainable-ai-xai-for-security-auditing/
├── 02_ai-risk-framework-implementation-nist-ai-rmf/
├── 03_ai-threat-modeling-mitre-atlas/
├── 04_regulatory-compliance-for-ai-eu-ai-act/
├── 05_ai-policy-architecture/
├── 06_ai-incident-response-playbook-simulation/
├── 07_ai-security-metrics-and-dashboarding/
├── 08_third-party-ai-model-risk-assessment/
├── 09_ai-transparency-documentation/
├── 10_ai-governance-for-bias-and-fairness-auditing/
├── 11_compliance-mapping-for-ai-systems-gdpr-cpra/
└── 12_ai-governance-operating-model/
```

Each module folder follows the same internal layout (specific file names vary — see the module's own `README.md` for details):

```bash
<module-name>/
├── README.md                  # Per-module overview, scenario, task, color guide
├── demo/                      # Instructor walkthrough materials
│   ├── *.xlsx                 # Filled-in instructor reference
│   ├── *.ipynb                # Demo notebook (modules with a Python component)
│   └── data/                  # Demo fixtures (when used)
└── exercises/
    ├── starter/               # Student-facing artifacts
    │   ├── *.xlsx             # Partially-filled workbook with [Your response here] markers
    │   ├── *.ipynb            # Notebook with TODO scaffolding
    │   └── data/              # Exercise fixtures (when used)
    └── solution/               # Completed reference
        ├── *.xlsx             # Fully-filled workbook with Reasoning: annotations
        ├── *.ipynb            # Fully implemented + executed notebook
        ├── *.png              # Generated visualizations (when produced)
        └── data/              # Solution fixtures (when used)
```

> ⚠️ **DO NOT NUMBER the exercise artifacts!**
> Our modular content may be used in more than one program where the order and number of exercises may differ from the order and number in the primary build.

## Resources for Building Exercises

The [Exercise Creation Resources](Exercise%20Creation%20Resources/) folder contains essential guidelines and standards for creating high-quality, accessible, and engaging exercises. These resources ensure consistency and help you follow best practices when developing course content.

### [Exercise Guidance.md](Exercise%20Creation%20Resources/Exercise%20Guidance.md)

Comprehensive guide covering exercise design principles, instruction writing, starter and solution code best practices, and requirements for solution videos and text. This is your primary resource for understanding what makes an effective exercise.

### [Accessibility Standards.md](Exercise%20Creation%20Resources/Accessibility%20Standards.md)

Details the WCAG 2.1 AA accessibility standards that all content must meet, including guidelines for headings, alt text, hyperlinks, color contrast, and avoiding images of text. Ensures exercises are accessible to all learners regardless of their abilities or use of assistive technology.

### [Real-World Content Guidelines.md](Exercise%20Creation%20Resources/Real-World%20Content%20Guidelines.md)

Guidelines for using real-world examples, company logos, trademarks, and references to people and organizations in exercises. Covers when it's appropriate to use actual brands versus creating fictitious examples and how to avoid legal and ethical issues.

### [Third Party Images and Datasets.md](Exercise%20Creation%20Resources/Third%20Party%20Images%20and%20Datasets.md)

Requirements for using third-party content including licensing requirements (Creative Commons, public domain), attribution standards, and approved sources for images, coding libraries, and datasets. Lists acceptable and unacceptable license types for commercial educational use.
