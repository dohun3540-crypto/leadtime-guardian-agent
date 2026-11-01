# 팀원 2 GitHub와 Studio V6 인계

2026-10-31 KST. GitHub 기준 자료와 Python 실행 환경은 준비됐다. 다음 단계는 Studio 담당자가 실제 V6 식별자와 변경되지 않은 실행 자료를 전달하는 것이다. 전달된 설정 V5와 Python 작업명 V6는 Studio 개선 후보 V6의 실측 증거가 아니다.

## 정확한 접근 대상과 확보한 파일

저장소는 `dohun3540-crypto/leadtime-guardian-agent`이며 원격 읽기를 확인했다. main `e36250074eed33db7951c4d58d8678e07b333a58`에는 C001 PDF/manifest가 없지만, 기준 [PR #11](https://github.com/dohun3540-crypto/leadtime-guardian-agent/pull/11)의 `feat/specs-data-engine-20261029` HEAD `f196c694917f2d9e5f4ec228c752bd3f2a4eb882`에는 모두 있다. private 저장소의 HTTP 404를 별도로 재현하지 않고 Git tree의 경로 존재 여부와 원격 접근으로 원인을 구분했다.

기존 [PR #12](https://github.com/dohun3540-crypto/leadtime-guardian-agent/pull/12)는 이 기준 HEAD에서 분리된 `codex/teammate-python-safety-v6` 브랜치다. 원격 두 HEAD 모두 이전 작업 이후 바뀌지 않아 같은 전용 브랜치를 재사용했다. 이번 추가 변경은 문서·검증 기록·V4 로컬 재생 결과에 한정한다.

| 자료 | 위치 | 확인 상태 |
|---|---|---|
| C001 원본 PDF 3개 | `data/cases/SYN-C001/SYN-C001_purchase_order.pdf`, `SYN-C001_delivery_notice.pdf`, `SYN-C001_quotation.pdf` | manifest SHA-256 3개 일치, 미재생성 |
| C002-C020 원본 PDF 57개 | `data/cases/SYN-C002-C020_DRAFT_PDFs.tar.xz` | 로컬 원경로 복원, 모든 manifest SHA-256 일치 |
| C008/C013/C017 입력 | 각 `data/cases/SYN-C###/manifest.json`, `trusted_base_case.json` | 기준 Git tree와 로컬 파일 존재 |
| 실제 V4 설정 | `configs/studio_native/config_v4.export.json` | 원본 유지 |
| 실제 V4 C001 실행 자료 | `data/results/studio_runs/C001_20261030_v4/`의 README, execution_record, instruct_original, 단계별 출력 | 저장된 실제 예측, 임의 수정 없음 |
| Python 계약/실행기/테스트 | `CHECKPOINT.json`의 required_files 23개 | 실제 파일 검사 완료 |
| 사용자 제공 설정 V5 | `configs/studio_native/config_v5.user-supplied.export.json` | cfg_o645qH9hDUgVnkrjw7Vets / version 5. 후보 V6 증거로 사용 불가 |
| 사용자 제공 main ZIP | leadtime-guardian-agent-main.zip | main 원본 21파일과 일치, PDF/V6 결과 없음 |

브랜치를 받은 새 환경에서는 먼저 `tar -tf data/cases/SYN-C002-C020_DRAFT_PDFs.tar.xz`로 목록을 확인한다. 경로·유형·manifest와 해시를 검사하고 기존 파일이 없을 때 `tar -xJkf data/cases/SYN-C002-C020_DRAFT_PDFs.tar.xz`로 복원한다. `-k`는 기존 파일을 덮어쓰지 않는다. 이번에는 57개 모두 사전 검사 후 복원했으며 60개 전체 해시는 `PDF_INTEGRITY.json`에 있다. PDF 생성기나 DRAFT 수정은 필요 없다.

## 실행 식별자를 섞지 않는 계약

| 구분 | Agent | Config 및 저장 버전 | Job | 증거의 의미 |
|---|---|---|---|---|
| 기존 실제 C001 V4 | agt_bXRXFSAgFmBayPjZF7VqRQ | cfg_SZi6qfyZ6XFoNszpXQK5xQ / 4 | job_gPmEYKzuJdBA6BmKhVnujs | 저장된 Studio Web 실행 성공 |
| 사용자 제공 V5 | 위 원본 Agent ID가 설정에 기록됨 | cfg_o645qH9hDUgVnkrjw7Vets / 5 | 실행 자료 미제공 | 설정 export만 확인 |
| Studio V6 개선 후보 | 미확인 | 미확인 | 미확인 | BLOCKED |
| Python 안전성 V6 | Studio Agent가 아님 | 엔진 출력 1.1.0 유지 | 새 Job 없음 | PR #12의 코드 작업명 |

V4 Job을 V6 Job으로 기록하거나 저장 설정 이름만으로 버전을 확정하지 않는다. 라이브 Agents API 키는 현재 환경에 없으며, 새 API 호출도 하지 않았다. Studio Web 실행은 담당자가 별도로 진행할 수 있지만 이 점검에서는 Studio 계정·워크스페이스·화면에 접속하지 않았다.

## Studio 담당자에게 전달할 요청문

아래는 복사해 전달할 요청 목록이다. 이 점검에서 제3자에게 메시지를 발송하지 않았다.

1. **V6 신원과 저장 설정:** 실제 Agent ID, Config ID, 저장 version, 워크플로우 이름, 워크스페이스, 저장 시각과 확인 화면. V6 Native 설정 export 원본 JSON 및 SHA-256.
2. **C001 우선 실행:** 기존 C001 발주서·통보서·견적서 PDF를 한 Job에 넣는다. 정확한 파일명·SHA-256·제출 순서, Job ID, 실행/완료 시각, 실패 시 실패 단계를 기록한다. 추출/계산값을 수동 수정하지 않는다.
3. **실제 다운로드 원본:** 케이스별 Native 최종 JSON과 Parse/Classify/각 Extract/Merge/Instruct 단계별 JSON, 원본 파일 ID/이름과 페이지 metadata. 다운로드 성공과 실행 완료를 별도 표시한다. 완료된 C001 다음 C013 → C017 → C008 순서로 같은 패키지를 전달한다.

기존 C013 #5의 `job_GvFUbjuLiPjNdBySNdH4kV`는 이전 요청에 적힌 참고 ID이며 이번 점검에서 관측한 실행이 아니다. 해당 다운로드를 확보해도 V6로 재명명하지 않고 실제 Config/Job에 맞춰 별도 비교한다. API 키·토큰·쿠키는 전달 목록에 포함하지 않는다.

## Python 수신과 차이 검증 절차

외부 입력은 `loads_strict → documents_from_export(raw, expected_job_id=actual_job_id) → analyze_studio_documents → 기존 엔진` 순서다. `content` 내부 JSON도 엄격하게 읽는다. 문서 배열/정규화 wrapper는 계산 계약이고, 그 자체가 실제 실행 완료의 증거는 아니다. Native metadata와 실행 기록을 함께 확인한다.

`status=OK`, `execution_status=COMPLETED`, `needs_review=false`를 모두 확인하기 전에는 계산값을 소비하지 않는다. 실패 시 NEEDS_REVIEW/BLOCKED, 부족량·금액 null, 추천·영향 배열 비어 있음이 계약이다. 기존 경고 차단 정책을 유지하며 원문 ID·수량·날짜를 정답으로 바꾸지 않는다.

실제 V6 자료를 받은 후 아래 명령의 `<...>`를 관측한 값으로만 채운다. 아래는 실행 예시 템플릿이며 아직 실행한 명령이 아니다.

```powershell
.\.venv\Scripts\python scripts/analyze_studio_export.py --export <ACTUAL_V6_NATIVE_FINAL_JSON> --base data/cases/SYN-C001/trusted_base_case.json --output <NEW_EMPTY_OUTPUT_DIRECTORY> --run-id <ACTUAL_V6_JOB_ID> --config-version <ACTUAL_V6_CONFIG_ID_AND_VERSION> --prompt-version member2-studio-v6
```

raw bytes와 SHA-256, 원본 final/단계 출력, 정규화 documents, 분석·오류, provenance를 보존한다. 실제 V6 자료가 있을 때만 `data/results/studio_runs/<CASE>_<YYYYMMDD>_v6/`를 만든다. V4/V6 원본·정규화 필드·warnings·evidence·Python 결과를 나란히 비교하고 차이의 원인이 추출, 구조, 타입, 식별자, 필수값, 근거 중 무엇인지 기록한다. 현재는 V6 쪽이 없으므로 diff 자체가 BLOCKED다.

C008은 명시 receipt_id와 입고별 수량이 있으면 PR #12의 기존 importer에서 지원한다. 합산 한 행을 R1/R2로 나누지 않는다. C017은 명확한 연도 포함 원문을 Studio가 ISO로 구조화해야 하며 Python이 비 ISO 입력을 조용히 정정하지 않는다. 필드가 맞고 Evidence만 없다는 이유로 근거를 만들어 넣지 않는다.

## 현재 상태 문서와 역사 로그

C001 manifest의 `studio_executed=false`와 `pdf_asset_checks.NOT_STUDIO.json`의 0-run은 생성/로컬 기계 검사 시점의 값이다. 실제 V4 실행은 2026-10-30 `execution_record.json`의 완료 Job과 원본 예측이 근거다. `case_types.csv`는 C001만 studio_tested=true이며 확장 케이스는 false다. 이 차이를 새 실행으로 덮어쓰거나 원본 라벨을 고치지 않는다. 최신 진입점은 `docs/WORK_HANDOFF.md` 최상단이며 이번 상태는 `VALIDATION_MATRIX.md`를 따른다.

기계 텍스트 대조는 `EVIDENCE_REVIEW.md`, 사람 검수는 별도 단계다. Studio가 전달한 evidence는 빈 배열 그대로이며, 이번에 만든 PDF 파일/페이지/원문 대조표를 원본 evidence로 위장하지 않았다. evidence_verified_against_pdf=false와 Gold DRAFT 상태를 유지한다.
