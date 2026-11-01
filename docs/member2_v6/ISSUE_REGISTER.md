# 팀원 2 Studio V6 통합 점검 문제 기록

점검일: 2026-10-31 KST. 현재 GitHub에서 검증된 것은 V4 실제 예측과 Python 코드다. Studio의 **V6 개선 후보**는 실제 ID·설정·예측이 없어 통합 완료로 승격할 수 없다. 앞선 PR #12의 **Python 안전성 V6**는 개발 작업명이므로 Studio 설정 버전과 구분한다.

기준 PR #11의 최신 HEAD는 `f196c694917f2d9e5f4ec228c752bd3f2a4eb882`, CI [41037193907](https://github.com/dohun3540-crypto/leadtime-guardian-agent/actions/runs/41037193907) 성공이다. 재사용한 PR #12의 점검 대상 HEAD는 `31fbdd128a01f4e805173f7f16d0864b5f718762`, CI [41075850428](https://github.com/dohun3540-crypto/leadtime-guardian-agent/actions/runs/41075850428) 성공이다. 이번 문서 커밋의 CI와 구분한다.

| 번호 | 우선 | 문제와 확인된 원인 | 해결 또는 완료 조건 | 담당 | 근거 | 상태 |
|---|---|---|---|---|---|---|
| M2-01 | P0 | main Git tree에 C001 PDF/manifest가 없음. 저장소 전체 부재와 혼동 가능 | PR #11 브랜치에서 필수 파일 23개 존재와 읽기 접근 확인. 원격 변경 파일 143개 확인 | GitHub/Python | CHECKPOINT.json | DONE |
| M2-02 | P0 | C002-C020 PDF가 개별 Git 파일 대신 tar.xz에 보관됨 | tar 목록 선확인, 경로·타입·57개 전체 해시 사전 확인 후 `tar -xJkf`로 무덮어쓰기 복원. C001 포함 60개 manifest 일치 | GitHub/Python | PDF_INTEGRITY.json | DONE |
| M2-03 | P0 | Studio V6 실제 Agent/Config/저장 버전 미확인 | Studio 화면에서 실제 ID·워크스페이스·저장 시각 확인, 원본 설정 export 필요. V4 또는 제공된 V5 ID를 재사용하지 않음 | 팀원 2 / Studio | GITHUB_STUDIO_HANDOFF.md 요청 목록 | BLOCKED |
| M2-04 | P0 | V6 C001 실제 Job/Native 예측 없음 | 같은 C001 3PDF를 한 Job으로 실행하고 Native 최종·단계별 JSON과 입력 해시 전달 | 팀원 2 / Studio | VALIDATION_MATRIX.md | BLOCKED |
| M2-05 | P0 | V6 Python 계약·V4/V6 차이를 검사할 실제 입력 없음 | 원본 그대로 `loads_strict → documents_from_export → analyze_studio_documents` 실행. 실패 필드/형태를 기록하고 정답값으로 보정하지 않음 | GitHub/Python, Studio | CHECKPOINT.json / 실제 V6 산출물 없음 | BLOCKED |
| M2-06 | P1 | C013 실제 PO 불일치 출력 미전달 | 원본 PDF의 PO999는 확인. 실제 V6 PO999 유지·BLOCKED·NEEDS_REVIEW와 null 계산값을 검증해야 함. 기존 #5 Job ID는 요청서의 참고값이며 원본 미확보 | 팀원 2 / Studio | EVIDENCE_TEXT_CHECKS.json, 합성 회귀 | BLOCKED |
| M2-07 | P1 | C017 한국어 날짜의 실제 V6 정규화 미검증 | PDF에 연도 포함 날짜를 확인. 실제 예측과 대응해 검사하고, Python 경계에서는 비 ISO 날짜/모호한 날짜를 자동 보정하지 않음 | 팀원 2 / Studio | EVIDENCE_TEXT_CHECKS.json / 합성 ISO 회귀 | BLOCKED |
| M2-08 | P1 | C008 receipt별 40/60과 합산 행을 혼동할 가능성 | 원본 PO R1=40/R2=60, 통보 R2=60 확인. 현재 PR #12는 명시 receipt_id 정규화 입력 지원, 합산 행 추측은 차단. 실제 V6 출력은 미확보 | 팀원 2 / Studio, GitHub/Python | PDF 원문, 기존 C008 회귀 | BLOCKED |
| M2-09 | P1 | 전달 Evidence 없음과 필드값 없음이 혼동될 수 있음 | C001 V4의 25필드를 원문 텍스트와 기계 대조. Studio Evidence 빈 배열 유지. 사람 검수 전 PDF 검증 플래그 false, 경고 완화 없음 | 팀원 2 / 통합 검토자, 팀원 3 / 라벨 협력 | EVIDENCE_REVIEW.md | NEEDS_REVIEW |
| M2-10 | P2 | 과거 C001 manifest의 studio_executed=false, 로컬 기계 검사 0-run과 실제 실행 기록이 함께 있음 | 생성 시점 metadata와 2026-10-30 V4 실제 실행을 구분. 원본 manifest·역사 로그는 그대로 두고 최신 WORK_HANDOFF와 검증 표에서 범위를 명시 | GitHub/Python | GITHUB_STUDIO_HANDOFF.md | DONE |
| M2-11 | P2 | 새로 제공된 main ZIP에 PDF/V6 자료가 있을 가능성 | main `e3625007…`의 21개 파일과 원본 바이트 일치. PDF·V6 export·V6 예측 모두 없음. 기준 자료 대체에 사용하지 않음 | GitHub/Python | ZIP_COMPARISON.json | DONE |
| M2-12 | P1 | Python 테스트/CI 성공이 Studio V6 성공으로 오인될 위험 | 두 소스에서 테스트를 새로 실행: 기준 80개, PR #12 189개, Ruff 각각 통과. 새 Studio 실행과 live API 요청은 0건 | GitHub/Python | REGRESSION_RESULTS.json, 실제 검사 로그 | DONE |
| M2-13 | P1 | 이전 PR #12에서 core engine/adapter도 최소 안전성 수정됨 | 이번 점검에서는 추가 변경 없음. 이전 예외는 비 KRW 견적 차단·공통 blocked 응답·중복 통보/날짜/수량 충돌 검사에 한정. 배분/견적 알고리즘 유지, 기존/확장 회귀 PASS. 팀 통합 시 해당 diff 검토 필요 | 통합 검토자 | PYTHON_SAFETY_V6_HANDOFF.md, PR #12 | NEEDS_REVIEW |

## 이번에 실제 수행한 범위

첨부 TXT와 DOCX를 읽고 최신 원격 HEAD·CI·파일 목록을 재조회했다. DOCX는 다른 프로세스가 열어 두어 공유 읽기 스트림으로 본문을 읽었으며 원본을 수정하지 않았다. ZIP도 압축 목록과 바이트만 비교했다.

`python -m pip install -r requirements-agents.txt`를 다시 실행했다. Python 3.11.9에서 기준 소스는 `git -c core.autocrlf=false archive f196c694…`로 `.venv/checks/` 아래에 격리하고 PYTHONPATH 및 실제 import 경로를 확인한 뒤 검사했다. 기준 소스의 pytest 80개는 **16.22초**, 현재 Python 소스의 pytest 189개는 **17.71초**, Ruff는 각각 PASS다. 추가 코드/새 테스트는 필요하지 않았고 기존 테스트 109개 증가분을 다시 확인했다.

기존 실제 C001 V4 Native를 새 출력 디렉터리 `data/results/python_safety_v6/C001_v4_replay_20261031/`에서 재분석해 0/60/60 EA와 60,500.00 KRW를 확인했다. 이는 새 Studio Job이 아니다. V6용 실제 결과 디렉터리는 만들지 않았다.

PDF 57개는 로컬에서만 복원했다. 개별 원본을 중복 커밋하지 않고 기존 tar.xz를 GitHub 전달 원본으로 유지한다. 로컬 `.git/info/exclude`에 복원 PDF 경로만 추가했으며 공유 `.gitignore`는 바꾸지 않았다. C001 PDF·기존 Studio V4·DRAFT 라벨·계산 코드의 이번 수정은 없다.

## 남은 통합 판정

GitHub/Python 측 접근·원본 복원·회귀 점검은 DONE이다. Studio V6 실측 검증은 BLOCKED이며, 근거·라벨의 사람 검수와 이전 core 수정 승격은 NEEDS_REVIEW다. 실제 자료가 들어오기 전에는 이 상태를 PASS로 바꾸지 않는다.
