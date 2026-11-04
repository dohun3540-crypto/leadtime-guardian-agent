# 김민주 발표·Gold 인계 준비

상태: DRAFT / BASELINE_BLOCKED. 최종 완료 보고가 아니다.

## 실제 기준
- 사용자 지정 수정 저장소: oxy znewl 표기를 사용하지 않는 정확한 주소 https://github.com/oxyznewl/leadtime-guardian-agent-upstage-kmj
- 준비용 기반 브랜치: feat/qa-ground-truth-evaluation. 이전 원격 조회 HEAD: a925103077173b37d1cefcd6a9576ae644dc2040. 이번 커밋의 실제 parent는 GitHub 커밋 기록으로 확인한다.
- 요구 기준: dohun3540-crypto/integration_finished_workforlast PR #3 최신 HEAD.
- 실제 PR 조회 결과: HTTP 404. 부재인지 권한 문제인지 확정하지 않는다. 문서 기재 80fb5814d6053fc592c627ea70ba30e1a2b6f451을 최신 검증값으로 사용하지 않는다.
- 따라서 이 브랜치는 PR #3 기반 작업이 아닌 격리된 발표 준비 초안이다. 통합 전 승인 기준선에서 문서만 선택적으로 이관해야 한다.

## 범위
새 데이터 검증 도구, 엔진, PDF, Gold DRAFT, 보관 Native, 운영 Studio 설정은 수정하지 않는다. 이 폴더에 준비 문서만 추가한다. 사람 검수·승인 기록을 대신 작성하지 않는다.

## 검증
pytest / tests/qa / Ruff / inventory / PDF 무결성·의미 검사는 이번 작업에서 NOT_RUN. 로컬 코드 실행 도구를 사용하지 않았다. 신규 Studio 실행 없음. 새 HEAD CI는 별도 확인 전 NOT_VERIFIED. 과거 문서의 861/95/37 및 PDF 60/60을 이번 결과로 재사용하지 않는다.

## 출처
첨부 2026.11.03 공용 작업 방식, GitHub/Studio 김민주 상세 TASK 및 실행 프롬프트, 통합 최종검증 문서. 아래 수치는 전부 이 문서의 요구 조건이며 실측값이 아니다.
