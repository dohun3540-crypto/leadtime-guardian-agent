# C001 보관 계산 연결 확인

읽기 기준: c73a1fae95dfdf6d45eaa08b23e91d7fa31e968d.
읽은 파일: data/results/studio_runs/C001_20261030_v4/analysis/analysis.json, normalized_documents.json, run_metadata.json. studio_original.json은 목록만 확인했으며 이번에 내용을 읽지 않았다.

## 확인 사실
- analysis.json: SYN-C001, OK/COMPLETED, 부족량 0→60 및 추가 부족 60, 예상 비용 문자열 60500.00, supplier_risk=UNKNOWN, external_action_taken=false, evidence_verified_against_pdf=false.
- evidence_document_ids에는 PO-DOC/NOTICE-DOC/QUOTE-DOC가 모두 있다. 앞서 읽은 별도 local_calculation.NOT_STUDIO.json의 목록과 다르므로 두 파일을 같은 결과로 합치지 않는다. 공급자 위험도 역시 별도 샘플의 LOW와 달리 여기서는 UNKNOWN이다.
- normalized_documents.json: 세 문서가 있으며 quote 배열이 단일 객체로, 빈 값 일부가 null로 저장돼 있다. 세 문서의 warnings/evidence는 빈 배열이다. 이 파일을 Studio Normalize 노드의 Native 원본이라고 확정하지 않는다.
- run_metadata.json run_id는 job_gPmEYKzuJdBA6BmKhVnujs로 이전 execution_record.json의 job_id와 텍스트상 같다.
- config_version은 cfg_SZi6qfyZ6XFoNszpXQK5xQ 문자열이다. 숫자 버전으로 해석하지 않는다. 이전 실행 기록에는 동일 Config ID와 숫자 version 4가 별도로 적혀 있다.
- processed_at_utc: 2026-10-30T09:44:39.160438+00:00.
- export_sha256 선언: 88387f8d6aee1421c9f628304c6b91811396b32da297d41b40e3d53c3d98dfea. 현재 파일 바이트에서 재계산하지 않았고 어느 Export 바이트와 일치하는지 확인하지 않았다.
- studio_provenance는 user-supplied export; verify against native run history라고 명시한다. 이 선언을 서비스 원본 인증 완료로 바꾸지 않는다.

## 파일 식별
analysis.json Git blob: 4ae6cf3bf0a5f226fb89f14e6be191686cf839d4
normalized_documents.json Git blob: af90a4d3be04e116527f0a18894716733fccf23d
run_metadata.json Git blob: eaa5df3c8d54a1d67843722c726fe6edc9ad3f2a

## 실제 변경
위 보관 결과를 설명할 수 있도록 PRESENTER_STUDIO_DEMO_SCRIPT.md를 갱신했다. 기대 수치만 있는 단계에서 보관 파일 값의 출처를 보여주는 정적 설명 단계로 진전했다. 신규 실행·정확도·Gold 승인·완전 E2E는 입증하지 않았다.

## 남은 일
원본 export 바이트/해시 검증, Native 실행 이력·파일별 ID·QA 입력 연결, 최신 V6 결과와 적격 Gold 평가, 사람 검수 및 공동 리허설. 이번에는 테스트·유료 Job·운영 설정 변경·병합 없음.
