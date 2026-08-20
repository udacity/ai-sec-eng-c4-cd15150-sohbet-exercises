# Validation Audit — 23 Reviewer Items

Freshly revalidated against the current working tree on 2026-08-20. Scope is limited to the 23 items in `OUTSTANDING-FIXES-for-Sohbet.md` across `demo`, `exercises/starter`, and `exercises/solution`; the separate project repository was intentionally excluded.

**Reviewer-checklist outcome:** 23 resolved, 0 partially resolved, 0 not resolved.

**Requested-scope outcome:** good to go. Every named reviewer acceptance criterion passes in the current working tree.

Per the requested scope, the six broader follow-up findings from the previous audit are excluded from this report and do not affect these verdicts.

| Reviewer item of interest | Verdict | Current evidence |
|---|---|---|
| 1. Global — re-apply the M01–M04 README fixes from `7e9fdbe` | **RESOLVED** | All named README fixes are present: M01 line 51 uses the test-set median and line 63 restores the `InconsistentVersionWarning` note; M02 line 40 says owners are pre-assigned; M03 line 21 lists the seven sheets, line 39 identifies the three prefilled IDs, and line 64 documents `AML.T0048.000`; M04 lines 12/30/47/61 restore the two-High-Risk-system scope, four-of-five exercise scope, and Reference Notes. |
| 2. M02 — choose a coherent summary approach and repair starter formulas/rows 12 and 15 as one change | **RESOLVED** | Both workbooks consistently implement Approach B (15 base risks). Starter `Executive Summary!B4:B8`, `B11:B14`, and `B17:B20` use ranges ending at row 16. Starter `Risk Register!F12/G12/F15/G15 = 2`; reasoning is in comments; `H12/H15` and `I12/I15` are live formulas. Solution summary is `15 / C4 / H6 / M3 / L2`, categories `6/3/3/3`, and NIST functions `4/3/4/4`; `B4` explicitly scopes the summary to R001–R015. |
| 3. M02 — solution notebook cell 18 operational count (`5 Medium` → 3) | **RESOLVED** | `02.../exercises/solution/risk_scoring.ipynb`, human cell 18 / JSON index 17, says `Operational risks are moderate (3 of 15)`. The saved output and a fresh execution agree. |
| 4. M02 — demo notebook cell 11 add an R007 mitigation | **RESOLVED** | `02.../demo/risk_scoring_demo.ipynb`, human cell 11 / JSON index 10, contains a nonblank R007 mitigation. Fresh execution prints R007 with grounding, hallucination detection, and human-review controls. |
| 5. M02 — demo notebook cell 15 say four Impact-5 risks and list R007 | **RESOLVED** | Human cell 15 / JSON index 14 says four Impact-5 risks and lists R001, R003, R005, and R007. Its later `Immediate Priority` section now also includes all four Critical risks: R001, R002, R005, and R007. Fresh parsing confirms both sets. |
| 6. M04 — starter and solution classifier cell 3 say five risk categories | **RESOLVED** | Human cell 3 / JSON index 2 in both starter and solution says five tiers/categories. The starter explicitly lists Unacceptable, High-Risk, GPAI, Limited, and Minimal. |
| 7. M04 — solution `Compliance Matrix!I14:K14` fill the Article 73 row | **RESOLVED** | `04.../exercises/solution/compliance_plan.xlsx`: `I14` contains the Article 73 reporting workflow and all three deadlines—15-day default, 10 days for an incident involving death, and 2 days for widespread infringement; `J14 = DPO + Compliance`; `K14 = 2026-06-30`. Visual inspection confirmed the row is populated. |
| 8. M05 — solution `Exception Procedure!B3` restore starter wording | **RESOLVED** | Solution `Exception Procedure!B3` exactly matches starter `B3`: MNPI-Adjacent requests proceed through the full workflow with GC co-signature at Risk Acceptance. Solution `B4` and `C4` remain consistent. |
| 9. M08 — solution `Vendor Assessment!D5:E5` use a certification answer and transparency rating | **RESOLVED** | `D5 = None published` under Security Cert and `E5 = Low` under Model Transparency. The misplaced numeric values are gone; the remaining row values are coherently placed. |
| 10. M09 — solution `Scenario Brief!A7` correct Article 13 vs. Article 50 | **RESOLVED** | Solution `Scenario Brief!A7` exactly matches starter `A7`: Article 13 attaches only to high-risk systems and the procurement process is the binding driver. `Gap Log!C5` and `Article 11 Reference!C10` consistently place end-user disclosure under Article 50. |
| 11. M02 — demo workbook R004 must be the same risk as notebook R004 | **RESOLVED** | Demo workbook `Risk Register!A5:I5` defines R004 as Manage / Technical / incident-response gap / Chief Medical Officer / 4×3 = 12 / High. This matches demo notebook human cell 4 / JSON index 3. |
| 12. M07 — solution `Dashboard Mockup!C3` change `0.34` to `1.964` | **RESOLVED** | `Dashboard Mockup!C3 = 1.964` as a numeric literal; `D3 = Red` and `E3` defines red as greater than 0.25. The solution notebook’s saved output is `1.964 / red / KRI #2 PASS`; independent recomputation reproduced `1.963966...`. |
| 13. M11 — demo must archive TRIAL-001 and report 3 deleted + 1 archived | **RESOLVED** | Demo human cell 13 / JSON index 12 archives Clinical Trial Results; cells 15 and 17 count dispositions and deleted size from completed records only. Fresh execution reports 3 deleted, 1 archived, 16.5 MB deleted, and one affected/retraining model; archived TRIAL-001 is excluded from impact analysis. |
| 14. M11 — solution notebook cell 12 audit trail must say 7 deleted, not 9 | **RESOLVED** | Solution human cell 12 / JSON index 11 derives deleted, archived, and held counts from actual dispositions. Fresh execution and the saved audit output say 7 deleted, 1 archived, and 1 retained under legal hold. |
| 15. M11 — correct retention attributions in demo `E3` and solution `E6` | **RESOLVED** | Demo `Data Retention Policy!E3` correctly cites EU CTR 536/2014 Art. 58. Solution `Retention Policy!E6` correctly limits HIPAA’s six-year rule to Security-Rule documentation, states GDPR sets no fixed audit-log period, and labels seven years internal. |
| 16. M12 — README change eight sheets to nine and include Reference Notes | **RESOLVED** | `12.../README.md:21` says nine sheets and includes Reference Notes. Artifact inspection confirms demo, starter, and solution each contain exactly those nine named sheets. |
| 17. M10 — starter fairness notebook cell 4 add the promised assert | **RESOLVED** | Human cell 4 / JSON index 3 immediately asserts every `results` value is non-`None` and directs learners to implement `audit_one_subgroup()`. No stale saved traceback/output is present. |
| 18. M12 — Govern Crosswalk correct Govern 1.4/1.5 and A.10.2/A.10.3 | **RESOLVED** | Solution `B9` and `D9` consistently use Govern 1.5; solution `C6`, starter `C6/D6`, and README line 61 consistently use A.10.3 Suppliers. Demo and solution `B4` now map Decision Rights to Govern 2.3. Reference Notes agree. |
| 19. M01 — remove the instructor-facing SHAP line/heading | **RESOLVED** | Demo human cell 12 / JSON index 11 is headed simply `## 5. Limits of SHAP`. The “live on screen” sentence and “model the caveats” heading are absent; the four substantive limits remain. |
| 20. M01 — remove README Color Guide but retain the closing response sentence | **RESOLVED** | The current working-tree README has no Color Guide, and line 61 retains the `[Your response here]` sentence. |
| 21. M03 — update five ATLAS technique names from ML to AI in all three workbooks | **RESOLVED** | All 15 targeted workbook cells use the AI names in demo, starter, and solution: `B4 Evade AI Model`, `B5 Backdoor AI Model`, `B7 Exfiltration via AI Inference API`, `B8 Denial of AI Service`, and `B9 AI Model Inference API Access`. M03 README lines 27, 38, 39, and 65 now match; none of the five stale ML labels remains in the current working tree. |
| 22. M04 — remove “2026 refresh” wording from all three notebooks | **RESOLVED** | All three named notebooks have zero matches for `2026 refresh`, `EU AI Act 2026 framework`, or `added in 2026`; their targeted wording now attributes GPAI to Regulation (EU) 2024/1689. |
| 23. M04 — move GPAI between High-Risk and Limited in the Risk Tiers sheets | **RESOLVED** | Demo, starter, and solution `EU AI Act Risk Tiers` now order High-Risk at `A5`, GPAI at `A6`, Limited at `A7`, and Minimal at `A8`. |

## Verification performed

- Inspected the cited workbook sheets, cells, values, formulas, and sheet inventories with the bundled spreadsheet runtime.
- Freshly executed M02 demo and solution, M04 solution through its classification summary, and M11 demo and solution. All five executions completed successfully and produced the reviewer-relevant results recorded above.
- Parsed all 23 repository `.ipynb` files as JSON successfully.
- Tested all 30 repository `.xlsx` packages successfully; no ZIP/OOXML package corruption was detected.
- Ran staged and unstaged `git diff --check`; both passed.

No course source artifact was changed during this audit. This Markdown report is the only file updated.
