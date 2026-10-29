# One-week roadmap (KST)
Internal freeze: **2026-11-10 17:00**. University updated notice: external final deadline appears **2026-11-11 13:00**; verify in LMS/OT.
| KST dates | WBS | Dependency | Person-hours |
|---|---|---|---:|
| 10/29 | W01 requirements, schemas; W02 deterministic engine | none | 8 |
| 10/30 | W03 synthetic docs and labels; W04 Studio OT and access | W01 | 8 |
| 10/31 | W05 human source review; W06 Studio prompts | W03 W04 | 8 |
| 11/01 | W07 one-page workflow and demo storyboard; W08 invalid data guards | W05 | 6 |
| 11/02 | W09 training; W10 first 12 Studio docs | W04 W06 | 8 |
| 11/03 | W11 individual Mission 1, W12 extraction error review | W10 | 5 |
| 11/04 | W13 remaining 48 docs; W14 Studio/Python adapter | W10 W08 | 10 |
| 11/05 | W15 quote/email draft; W16 conflict tests | W14 | 8 |
| 11/06 | W17 team Mission 2; W18 CI and regression tests | W13 W15 | 5 |
| 11/07-08 | W19 fix failure cases; W20 optional evidence trail | W17 | 8 |
| 11/09 | W21 office hours, demo video, PDF slides, config export | W19 | 8 |
| 11/10 | W22 freeze/audit, backups | W21 | 5 |
| 11/11 | W23 final upload and confirmation | W22 | 2 |

Approximate team total: **89 person-hours**, not a guarantee. Roles: (1) lead/backend & schemas, (2) Studio prompts/workflow, (3) data/labels/evaluation, (4) demos/submission. One developer starts; up to four parallelize when available. ChatGPT can author specs, code, tests, synthetic PDFs; user/team must validate ground truth, access Studio, export actual settings, and submit LMS deliverables.

Dependencies: valid schemas → source labels → Studio test → output adapter → final demo/exports. If blocked by Studio access, prioritize local B calculations and dataset. If behind by Nov 6, remove C optimization/UI and complete essential documents, results, and final submission. Mission 1 Nov 3, Mission 2 Nov 6, office hours Nov 9; confirm exact mission hours and grading rules at OT.
