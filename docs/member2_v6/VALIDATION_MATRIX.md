# 팀원 2 V4 기준선과 Studio V6 검증 표

2026-10-31 KST. DONE은 해당 점검 업무를 실제 수행했다는 뜻이며 Studio V6 전체 합격을 의미하지 않는다. 실제 V6 입력이 없는 항목은 BLOCKED로 유지한다.

| 케이스 | 원문/계약상 기대 | 이번 실제 검사와 결과 | Studio V6 결과 | 통합 판정 |
|---|---|---|---|---|
| C001 | 정상 정합성, 부족 0→60 / 추가 60 EA, 견적 60,500 KRW | 저장된 실제 V4 원본을 새 Python 실행으로 재분석해 동일 결과. 3PDF 해시 일치, 예측 25필드 원문 텍스트 기계 대조 | 실제 V6 설정·Job·예측 없음 | V4 재현 DONE/PASS, V6 BLOCKED |
| C013 | PO1 발주/견적과 PO999 통보를 자동 연결하지 않음. NEEDS_REVIEW/BLOCKED, 계산값 null | 원본 PDF 3개/해시, 통보 PO999 확인. 기존 합성 차단 회귀 재실행 PASS | 실제 Native 예측 없음. 이전 #5 원본도 미확보 | 원문 확보 DONE, 실측 충돌 검증 BLOCKED |
| C017 | 원문의 2026년 11월 3일·8일·4일을 명확할 때만 ISO로 구조화 | PDF 원문/해시 확인. 기존 합성 ISO 입력 계산 PASS, 한국어 날짜가 Python 경계에 남으면 차단 회귀 PASS | 실제 정규화 결과 없음 | 원문 확보 DONE, 실제 추출 BLOCKED |
| C008 | PO R1=40/R2=60, 통보 R2=60만 변경. 주문별 중복 배정 금지 | PDF/해시 확인. 기존 합성 명시 매핑은 R1 유지/R2 변경, 부족 0/40, 견적 40,500 KRW 회귀 PASS | 실제 receipt 행 구조 미제공 | 명시 정규화 계약 DONE/PASS, 실제 통합 BLOCKED |

## 실행 방식별 분리

| 검증 방식 | 실제 실행/조회 | 결과 | 입증하지 못하는 범위 |
|---|---|---|---|
| 원격 GitHub | PR #11 HEAD f196c694… / PR #12 점검 HEAD 31fbdd12… / 해당 CI 재조회 | 모두 변경 없음, 각 CI success | Studio V6 계정/실행 |
| 기준 소스 pytest | 별도 Git archive + PYTHONPATH/import 경로 확인, Python 3.11.9 | 80 passed / 0 failed / 16.22초 | 실제 신규 추출 성능 |
| PR #12 소스 pytest | 현재 소스, Python 3.11.9 | 189 passed / 0 failed / 17.71초 | V6 실제 추론 |
| Ruff | 위 두 소스 각각 새로 실행 | 각각 PASS | 업무 데이터의 원문 정확도 |
| FakeClient / SDK loopback | 두 suite에 포함된 모의 계약 실행 | 현재 소스 FakeClient 18개, SDK HTTP 13개 포함 PASS | 실제 Upstage 네트워크 호출 |
| 기존 실제 Studio Web 예측 | V4 C001 Native 원본 재사용 | Python 재분석 0/60/60, 60,500.00 KRW | 새 V6 Studio Job 완료 |
| 원본 PDF 복원/무결성 | tar 목록, 57개 경로/유형/사전 해시, 무덮어쓰기 추출, C001 포함 60개 해시 | 모두 PASS | 사람 검수된 Gold |
| PDF 텍스트 대조 | 12PDF 원문 읽기, C001 실제 V4 25필드 문맥 대조 | MACHINE_TEXT_MATCH | 사람 라벨 승인, 빈 Studio Evidence가 검증됐다는 주장 |
| Studio V6 Web / live Agents API | 새 Studio 실행 0, live API 요청 0 | BLOCKED / NOT_RUN | V6 합격·API 성공 |

## C001 독립 산술과 실제 Python 출력

신뢰 입력은 재고 40, 고객 주문 100/납기 2026-11-05다. 원본 PDF와 실제 V4 예측의 기존 입고는 100/2026-11-03이므로 납기까지 총 140에서 주문 100을 충족해 부족 0이다. 변경 입고 2026-11-08은 고객 납기 후여서 재고 40만 사용하고 부족 60이 된다. 추가 부족량은 60-0=60, 대체 견적은 납기 전 2026-11-04에 60까지 공급하므로 60×1,000+운송비 500=60,500 KRW다.

2026-10-31 로컬 재생 출력은 `data/results/python_safety_v6/C001_v4_replay_20261031/analysis.json`이다. `status=OK`, `execution_status=COMPLETED`, `needs_review=false`, `external_action_taken=false`, `evidence_verified_against_pdf=false`를 확인했다. Native 원본 SHA-256은 `88387f8d6aee1421c9f628304c6b91811396b32da297d41b40e3d53c3d98dfea`이며 재생 사본과 같다. V6 결과와의 필드/계산 diff는 비교 대상이 없어 만들지 않았다.

## 아직 완료되지 않은 근거

Studio의 실제 V6 Agent/Config/저장 version·설정 JSON·각 실제 Job과 Native final/단계별 JSON이 없다. V4/V5 ID로 대신 채우지 않았다. PDF 원문 기계 대조표는 사람이 검수할 후보이며 Gold DRAFT나 전역 근거 검증 상태를 변경하지 않는다. 경고 생성 정책 합의·사람 검수·이전 core 수정의 통합 승인은 NEEDS_REVIEW다.

정확한 요청 목록과 수신 절차는 [GitHub와 Studio 인계](GITHUB_STUDIO_HANDOFF.md), 문제·담당·우선순위는 [문제 기록](ISSUE_REGISTER.md), 기계 증거는 CHECKPOINT.json·PDF_INTEGRITY.json·REGRESSION_RESULTS.json·EVIDENCE_TEXT_CHECKS.json을 확인한다.
