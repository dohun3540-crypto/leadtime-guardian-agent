# Studio ↔ Python ↔ LMS integration handoff

최신 Python 계약과 상태: [V6 통합 인계](PYTHON_SAFETY_V6_HANDOFF.md). 외부 예측은 엄격한 JSON 파싱 → `documents_from_export` → `analyze_studio_documents` 경로로 처리한다. 아래 4번의 저수준 Adapter+엔진 직접 호출은 전체 검증 경계를 대체하지 않는다. C013 실제 결과는 미제공으로 BLOCKED이며, 제공된 설정 v5를 실행 결과로 취급하면 안 된다.

1. Studio Large: verify account access and create the real document workflow (Parse → Classify → type-specific Extract → Merge/Match → Validate/Instruct). The Studio UI and exact native node links must be tested by a teammate.
2. Output normalized JSON using configs/schemas/document_extraction.schema.json. For delivery notices include po_id, revised_delivery, items with product_id and receipt_id when multiple receipts match.
3. Human team members verify PDF originals vs gold labels separately. Run C001 normal, C013 wrong PO (must block), C017 Korean date. Then expand to 20 cases / 60 PDFs. Record predictions, errors, run_id, versions and metrics. Never supply gold labels as Studio predictions.
4. To handoff a predicted case to code: load strict JSON, documents_from_export(raw, expected_job_id=actual_job_id), then analyze_studio_documents(base_case, documents, schema). Require OK + COMPLETED + needs_review=false before consuming calculations. Base case contains trusted inventory/orders/inbound/quotes. The provenance sidecar preserves supplied evidence; it does not verify original PDF text.
5. Console: verify actual Agents API endpoint, response JSON, workspace permissions and quota. Do not expose API keys. Native Studio workflow export is not the same as any GitHub JSON Schema.
6. LMS: read course and submission specifications, submit individual/team missions and final artifacts. 10/30 team schedule: final upload before 2026-11-10 17:00 KST. Team should aim earlier.
7. Required for real demo: one actual normal flow and one actual conflicting PO blocked flow; screenshot/export native Studio config; Studio prediction JSON; human checked labels; source PDF; video; one-page design; slides.

Deferred: full cost optimization, multi-agent autonomy, live procurement, ERP and production deployment.
