# 팀원 2 개인 Work 실행 보고

2026-11-01 KST. GitHub·Python·PDF 준비 작업은 실제 재검사했다. 운영 Studio 후보의 신원·설정·실제 예측과 새 공용 문서는 확보되지 않았으므로 전체 통합 완료를 선언하지 않는다. 다음 실행을 위해 Studio용 프롬프트, 우선 4개 케이스 PDF 12개, 기존 문서 스키마와 입력 해시를 별도 다운로드 묶음으로 준비한다.

## 가 실제 확인한 GitHub와 입력 자료

| 대상 | 확인 결과 |
|---|---|
| PR #11 / feat/specs-data-engine-20261029 | 원격 HEAD `f196c694917f2d9e5f4ec228c752bd3f2a4eb882`, open Draft, 변경 파일 143개 |
| PR #12 / codex/teammate-python-safety-v6 | 점검 시작 HEAD `7897641b75042d02bb29bce9e37a557bf4c7354e`, open Draft, 변경 파일 49개 |
| PR #12 시작 HEAD CI | run 41081152861 completed/success 재조회. 이번 기록 커밋의 CI와 별개 |
| main | `e36250074eed33db7951c4d58d8678e07b333a58`, 원본 PDF/Native 설정/실행 자료 없음 |
| leadtime-guardian-agent.copy | 새로 보이는 원격 브랜치지만 HEAD는 PR #11과 같은 f196c694…로 추가 자료 없음 |
| 사용자 재제공 main ZIP | SHA-256 `8ad48f0e4ccdb91ff4c8b2fbc6e769a74bf287b463bfbc4feee53357225ef963`, 파일 21개. 이전 ZIP과 같은 바이트이며 새 DOCX·PDF·운영 결과 없음 |
| 새 공용 현황/협업 DOCX·팀원2 상세 TASK·전체파일 목록.zip | 확인한 다운로드/카카오톡 폴더와 원격 브랜치 Git tree에 없음. 읽었다고 표시하지 않음 |
| 기존 첨부 | 이전 V6 통합검증 DOCX와 GitHub/Studio 점검 TXT는 앞선 작업에서 읽은 자료. 이번에는 기존 Studio TXT와 최신 저장소 인계를 재확인 |

사용자가 GitHub와 ZIP을 기준으로 보라고 안내하여 현재 원격 네 브랜치와 재첨부 ZIP을 확인했다. 서로 다른 commit tree는 main·기준·팀원2 세 개이며, DOCX와 새 운영 Native 결과는 없었다. 저장소 부재/권한 오류로 해석하지 않는다. 실제 원격 읽기는 성공했다.

## 나 이번에 직접 실행한 검사

Python 3.11.9, pytest 9.2.0, Ruff 0.17.3, jsonschema 4.26.0, OpenAI SDK 2.54.0, httpx 0.28.1을 확인하고 `python -m pip check`를 실행해 PASS를 확인했다. requirements-agents.txt와 requirements-dev.txt의 기존 환경을 재사용했다.

| 범위 | 실제 명령/작업 | 결과 |
|---|---|---|
| 기준 f196 소스 | raw Git archive를 격리하고 PYTHONPATH/실제 import 파일 확인 후 `python -m pytest -q` | 80 passed, 0 failed, 18.17초 |
| 기준 f196 소스 | `python -m ruff check .` | PASS |
| 현재 789 소스 | `python -m pytest -q` | 189 passed, 0 failed, 19.20초 |
| 현재 789 소스 | `python -m ruff check .` | PASS |
| 원본 PDF | 케이스별 manifest를 다시 읽고 60개 실제 파일 SHA-256 대조 | 60/60 PASS, 재생성·덮어쓰기 0 |
| 기존 V4 C001 Native | strict JSON → documents_from_export → analyze_studio_documents → 기존 엔진 | OK/COMPLETED, 0/60/60 EA, 60,500.00 KRW |
| API 사전 검사 | C001 기존 PDF 3개와 알려진 V4 Agent로 `--preflight` 실행 | SDK 있음, 키 없음, 네트워크 요청 0 |
| 신규 Studio Web / live Agents API | 실행하지 않음 | 0건 / NOT_RUN |

현재 189개에는 FakeClient 18개와 SDK loopback HTTP 13개가 포함된다. 이들은 실제 Upstage 추론이 아니다. 이번 재검사에서 신규 결함이 발견되지 않아 core·Adapter·테스트를 추가 수정하지 않았다. 과거 80/189개 수를 새 실행으로 대신 쓰지 않았으며 로그를 이번 폴더에 저장했다.

V4 재생 원본 SHA-256은 `88387f8d6aee1421c9f628304c6b91811396b32da297d41b40e3d53c3d98dfea`다. 원본·신뢰 입력을 변경하지 않았고 evidence_verified_against_pdf=false, external_action_taken=false다. 이 결과를 운영 V6의 성공으로 사용하지 않는다.

## 다 운영 후보와 QA Sandbox 식별자 분리

| 구분 | Agent / Config / 버전 | Job·Step | 판정 |
|---|---|---|---|
| 기존 V4 실제 C001 | agt_bXRXFSAgFmBayPjZF7VqRQ / cfg_SZi6qfyZ6XFoNszpXQK5xQ / 4 | job_gPmEYKzuJdBA6BmKhVnujs / 63f6a860-7c86-5036-b32d-6eae38ca7677 | 저장된 실제 기준선 |
| 과거 사용자 V5 export | 위와 같은 원본 Agent / cfg_o645qH9hDUgVnkrjw7Vets / 5 | 실행 원본 미확보 | 설정 파일만 확인. 새 QA Sandbox와 동일하다고 단정하지 않음 |
| 새 공지의 독립 QA Sandbox #5 | 파일·실제 ID 미제공 | 미확인 | 팀원 1 소유. 운영 후보와 분리, BLOCKED |
| 팀원 2 운영 최신 후보 | 실제 Agent/Config/저장 버전 미제공 | 실제 Job·Step 미확인 | BLOCKED |
| Python 안전성 V6 | Studio 설정 ID가 아닌 이전 개발 작업명 | 새 Job 없음 | PR #12의 Python 변경 묶음 |

새 공유 JSON이 독립 QA Sandbox #5라는 사용자 공지를 작업 기준으로 적용한다. 과거 V5 export의 숫자 5만으로 새 Sandbox를 식별할 수 없다. 파일을 확보하면 Native 내부 ID와 화면·워크스페이스로 대조해야 한다. 현재는 운영/Sandbox 간 실제 설정 diff도 BLOCKED다.

## 라 Studio 실행 프롬프트와 입력 묶음

이 폴더의 `STUDIO_AI_PROMPT.txt`가 이번 검사 상태와 실제 입력 해시를 반영한 Studio 전용 지시서다. 개인 Work 프롬프트 전체를 Studio에 넣지 않는다.

다운로드 묶음은 우선 순서 C001 → C013 → C017 → C008의 원본 PDF 12개, input_manifest.json, 기존 document_extraction.schema.json, 별도 python_inputs의 신뢰 기준 입력 4개, Studio 원본 회수 체크리스트를 포함한다. Gold DRAFT·expected·sample 예측은 넣지 않는다. 문서 스키마와 신뢰 입력은 참고 계약이고 실제 Studio 예측이 아니다. input_manifest의 순서는 제출 계획이며 실제 업로드/Job 실행 기록이 아니다.

## 마 Studio에서 받아야 할 원본

1. 팀원 2 운영 후보와 팀원 1 Sandbox를 구분하는 실제 이름·워크스페이스·Agent ID·Config ID·저장 버전·시각·확인 화면.
2. 운영 후보의 변경 전후 Native 설정 export 원본과 SHA-256. 수정 권한이 없으면 접근 오류와 필요한 담당자 조치.
3. C001 우선 실제 Job ID·Step ID/이름/상태·실행/완료 또는 실패 시각, 원본 final JSON, 가능하면 Parse/Classify/각 Extract/Merge/Instruct 단계 원본.
4. 실제 제출한 PDF 이름·개수·순서·파일 ID·SHA-256 및 해시 출처. manifest 계획과 실제 제출 이력을 별도 표시.
5. C001 Python 검사가 끝난 뒤 C013 → C017 → C008의 같은 패키지. 실패 케이스도 실제 오류·실패 단계·원본을 보존.

자료 수신 후 새 출력 폴더에서 strict parser와 업무 경계를 적용한다. Job/Config/입력 해시를 대조하고 구조·타입·식별자·필수값·수량·날짜·가격·warnings·evidence 문제를 구분한다. C013 PO999를 고치거나 경고를 제거해 통과시키지 않는다. C017은 연도 추측 금지, C008은 명시 receipt 행 보존이 기준이다. 실제 예측이 없으므로 이번에 후보 필드 diff나 Native 실행 결과 폴더를 만들지 않았다.

## 바 변경·보존과 상태

새 문서·이번 검사 로그·V4 재생 수신 기록·Studio 프롬프트를 기존 전용 브랜치/PR #12에 추가한다. main·PR #11·운영 V4·타인 설정·PDF·DRAFT·기존 계산/Adapter 코드는 바꾸지 않는다. 기존 로컬 deliverables ZIP도 보존한다. 신규 기능이나 의존성은 추가하지 않았다.

| 상태 | 해당 항목 |
|---|---|
| DONE | 원격 재조회, 기존 구현·호출자/회귀 검사, 60PDF 해시, 실제 V4 재생, 최신 Studio 지시서·입력 묶음 작성 |
| BLOCKED | 새 공용 문서·Sandbox 원본 확보, 운영 후보 실제 ID/Native 설정/실제 예측, 운영→Python 신규 통합 및 운영/Sandbox diff |
| NEEDS_REVIEW | 팀원 3의 PDF/Gold 사람 검수, 실제 경고 정책 합의, 독립 QA·최종 통합 승인 |
| NOT_RUN | 새 Studio Job, live Agents API, Cross-Agent 실측, 최종 시연·제출 |

## 사 팀 공유 초안과 다음 행동

복사 전달용 초안은 `TEAM_SHARE_DRAFT.txt`에 있다. 이 점검에서 팀 채팅·메일에 실제 발송하지 않는다.

다음 행동은 ① 아래 입력 묶음과 STUDIO_AI_PROMPT를 운영 Studio AI에 전달해 실제 후보 ID·저장 설정 확인, ② C001 3PDF 한 Job의 Native 원본·입력 해시·Job/Step을 개인 Work로 회수, ③ Python 검사 뒤 C013/C017/C008 및 팀원 1 독립 QA·팀원 3 검수 결과를 같은 계약으로 교환하는 순서다.

전체 완료는 실제 운영 입력부터 Python·독립 QA·원문/Gold 검수·회귀·시연·제출 자료가 연결됐을 때만 판정한다.
