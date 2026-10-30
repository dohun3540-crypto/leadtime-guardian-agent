# B+C3 implementation status (2026-10-30 KST)

최신 상태는 [Python 안전성 V6 보고서](PYTHON_SAFETY_V6_HANDOFF.md)를 기준으로 한다. 실제 C001 v4 예측의 Python 재분석 PASS, pytest 189개/Ruff PASS. C013 실제 v5 결과 미제공으로 BLOCKED, 라이브 Agents API와 PDF 근거 검증은 NOT_RUN이다. 아래 내용은 이전 개발 기록이며 실제 Studio 실행·확장 데이터 부재 항목은 최신 상태를 설명하지 않는다.

---

## Source code delivered in PR #11 (unmerged)
- B: deterministic lead-time calculations, multi-order deadline allocation, quote draft with capacity and shipping charged once.
- C1: baseline vs revised ETA, per-order and case-level additional shortage.
- C2: normalized documents checked for PO/SKU/ETA conflicts and ambiguous receipts; unsafe cases are blocked.
- C3: multiple partial inbound receipts per PO/SKU; quantities never reused.
- Studio extraction adapter and local regression tests; run CI and review before merge.

## Not yet done
- 20-case/60-PDF package described in earlier local work is **not in this Git branch**; do not confuse local files with committed files.
- Upstage Studio real agent runs, actual agent config export, Studio predictions and field-level PDF source verification.
- Authentication, persistent database, production UI, ERP sync and email/purchase actions.
- Studio API transport requires real API request/response and account permission; credentials must stay outside Git.

**Safety:** evidence_document_ids tracks document references only. evidence_verified_against_pdf=false until human verification. Cost output is a greedy quote estimate, not globally optimal.

**Deadline:** final submission 2026-11-10 17:00 KST per the 10/30 team timetable; confirm LMS details.
