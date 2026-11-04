# 차단 항목과 다음 인계

| 항목 | 상태 | 확인 사실 / 해제 조건 | 담당 |
|---|---|---|---|
| 승인 기준선 | BLOCKED | 통합 저장소 PR #3 조회 HTTP 404. 정확한 접근 권한과 최신 HEAD·CI·동결 기록 확보 필요 | 구도훈·최유석 |
| 검수 XLSX | BLOCKED | 이번 작업에 원본 미확보. 실제 원본·시트·SHA·이력 수신 필요 | 김민주→최유석 |
| 핵심 PDF 사람 판단 | NOT_VERIFIED | C001/C013/C008/C017 원문 페이지 대조 및 실제 판단 기록 필요 | 김민주 |
| 운영 Native·화면 | NOT_VERIFIED | 최신 동일 사례 단일 운영 Job·Config/Step/File·원본 SHA 필요 | 구도훈 |
| Python 수치 | NOT_VERIFIED | 같은 Native 입력의 V6 입력/출력·코드 SHA 필요 | 윤현준 |
| Gold·평가 | NOT_MEASURED | 실제 승인 기록과 동결 Gold·적격 평가 필요 | 최유석 |
| 신규 HEAD 회귀 | NOT_RUN | 실행 환경에서 pytest·Ruff·inventory·PDF 검사 및 해당 SHA CI 필요 | 최유석 |
| Release | BLOCKED | 위 필수 증거와 최종 Gate 승인 필요 | 구도훈 |

## 인계 요청문 초안 — 미전송
구도훈님: C001 기존 실행 화면·Native·설정/Job/Step/File/PDF 해시와 QA 연결 근거를 부탁드립니다. 윤현준님: 동일 입력의 V6 계산·차단 원본과 코드 기준을 부탁드립니다. 최유석님: XLSX 비교·승인 Gold·평가 원본 및 정확한 HEAD CI를 부탁드립니다. 김민주 검수 기록은 실제 원문 판단 후에만 추가합니다. 신규 실행이나 승인 기록 자동 생성을 요청하는 것이 아닙니다.

이 준비본은 기반 차이로 최종 통합 가능한 상태가 아니다. 승인 기준선 접근 후 별도 이관 검토가 필요하며 main/기존 PR 병합이나 force push를 수행하지 않는다.
