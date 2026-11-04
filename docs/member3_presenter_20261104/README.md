# 김민주 발표·Gold 인계 준비

상태: DRAFT / BASELINE_BLOCKED. 최종 완료 보고가 아니다.

## 실제 기준
- 사용자 지정 수정 저장소: https://github.com/oxyznewl/leadtime-guardian-agent-upstage-kmj
- 준비용 기반 브랜치: feat/qa-ground-truth-evaluation. 이전 원격 조회 HEAD: a925103077173b37d1cefcd6a9576ae644dc2040.
- 요구 기준: dohun3540-crypto/integration_finished_workforlast PR #3 최신 HEAD.
- 이전 실제 PR 조회: HTTP 404. 부재인지 권한 문제인지 확정하지 않는다. 문서 기재 80fb5814d6053fc592c627ea70ba30e1a2b6f451을 최신 검증값으로 사용하지 않는다.
- 본 브랜치는 PR #3 기반 작업이 아닌 격리된 발표 준비 초안이다. 통합 전 승인 기준선에서 문서만 선택적으로 이관해야 한다.

## 읽는 순서
1. NEXT_ACTIONS_FOR_MINJU.md: 사람이 직접 할 최소 확인과 인계.
2. C001_TEXT_PRECHECK.md: 보관 TXT 세 개의 확인값·Git blob SHA·해석 한계.
3. HUMAN_REVIEW_WORKSHEET.csv: 실제 PDF 대조용 미승인 작업지.
4. PRESENTER_STUDIO_DEMO_SCRIPT.md 및 C001_C013_C008_C017_DEMO_STORY.md: 정적 시연 초안.
5. PRESENTATION_DATA_FACT_CHECK.md / DEMO_EVIDENCE_TABLE.csv / PRESENTATION_FAQ_DRAFT.md.
6. ORIGINAL_MISSING.md / PRESENTER_GOLD_REVIEW_LOG.md / BLOCKERS_AND_OWNERS.md.

## 범위와 검증
새 검증 도구·엔진·PDF·Gold DRAFT·보관 Native·운영 Studio 설정은 수정하지 않는다. 이 폴더 문서만 변경한다. 사람 검수·승인 기록을 대신 작성하지 않는다.

이번 추가 작업은 1b04e8dddf4b6ee50da81802106147ae6949724f의 보관 C001 TXT 세 파일을 읽은 결과다. PDF 시각 검수와 원본 SHA-256 검증은 미수행. Git blob SHA와 PDF SHA-256을 구분한다. 정확도·최신 E2E는 미측정/미검증.

pytest / tests/qa / Ruff / inventory / PDF 무결성·의미 검사는 이번 작업에서 NOT_RUN. 신규 Studio 실행 없음. 새 HEAD CI는 별도 확인 전 NOT_VERIFIED. 과거 문서의 861/95/37 및 PDF 60/60을 이번 결과로 재사용하지 않는다.

## 출처
첨부 2026.11.03 공용 작업 방식, GitHub/Studio 김민주 상세 TASK 및 실행 프롬프트, 통합 최종검증 문서. 보관 TXT 출처는 C001_TEXT_PRECHECK.md에 고정했다. 문서의 수락 조건과 실제 실행값을 구분한다.
