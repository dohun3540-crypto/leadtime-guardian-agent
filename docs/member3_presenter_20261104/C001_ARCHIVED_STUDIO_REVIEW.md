# 보관 C001 Studio 자료 확인

조회 커밋: 29d0b71297ef736e8fee66c8b7b67c32efa7991b.
범위: data/results/studio_runs/C001_20261030_v4/의 execution_record.json 및 extract-03/04/05.json 읽기. 신규 실행 없음. 파일 재계산·전체 체인 검증·사람 승인은 아님.

## 실행 기록에 저장된 값 — 현재 서비스에서 재인증한 값 아님
- checkpoint_date_kst: 2026-10-30
- execution_mode: live_studio_web (보관 기록의 선언; 이번 작업에서는 ARCHIVED_STUDIO로 취급)
- workflow_id: agt_bXRXFSAgFmBayPjZF7VqRQ
- config_id: cfg_SZi6qfyZ6XFoNszpXQK5xQ / version 4
- job_id: job_gPmEYKzuJdBA6BmKhVnujs
- native_step_run_id: 63f6a860-7c86-5036-b32d-6eae38ca7677
- studio_execution_completed=true, predictions_modified=false, python_analysis_status=OK는 보관 기록의 보고값.
- human_gold_reviewed=false / accuracy_measured=false / evidence_verified_against_pdf=false.

실행 기록에 적힌 source_pdfs 3개의 SHA-256은 앞서 읽은 SYN-C001 manifest의 선언값과 텍스트상 일치한다. 다운로드 바이트 재계산이나 실제 업로드 File ID 검증은 하지 않았다. 이 기록에는 파일별 File ID·각 Extract Step ID·QA Job 바인딩이 없어 단독으로 완전한 실행 체인을 입증하지 못한다.

## 보관 추출 결과
| 파일 | Git blob SHA | 읽은 핵심 값 |
|---|---|---|
| extract-03.json | 70bc95496149ef3c4b1849ec303ad15abfe030b1 | PO-DOC / PO1 / 기존일 2026-11-03 / A R1 100 EA |
| extract-04.json | 9aa3f308c4d440d34b8100f17dbce27ae2dd0976 | NOTICE-DOC / PO1 / 2026-11-03→2026-11-08 / A R1 100 EA |
| extract-05.json | c89b575ab84c5bb8cd81d04ff9b0c80dff29bb42 | QUOTE-DOC / PO1 / S1 Q1 / 가능량 60 / 입고 2026-11-04 / 단가 문자열 1000.00 / 운송비 문자열 500 / KRW |

세 결과의 evidence 배열은 모두 비어 있다. 세 파일 자체에는 운영 Job/Config/File 귀속 메타데이터가 없다. 상위 실행 기록과 같은 폴더에 있다는 사실만으로 원본 다운로드 전체 바이트의 진위와 귀속을 확정하지 않는다.

PDF에서 읽은 핵심 값과는 위 범위에서 일치하지만 승인 Gold 기반 정량 평가가 아니다. 견적당 운송비 1회 조건과 구매 미실행 문구는 PDF 본문에 있고, 위 추출의 shipping_cost 값만으로 그 조건 전체를 담았다고 주장하지 않는다.

## 발표에 사용할 수 있는 표현
“저장소에 보관된 2026-10-30 V4 실행 기록과 세 추출 파일을 확인했습니다. 신규 Live 실행이나 최신 V6·독립 QA 전체 연결을 이번에 검증한 것은 아닙니다. 공식 정확도는 미측정입니다.”

금지: 보관 결과를 신규 Live 성공으로 소개, 빈 evidence를 채워 원본처럼 보존, 과거 80 passed/Ruff 보고를 이번 HEAD CI로 재사용, AI 판단을 사람 Gold 승인으로 표기.

## 확인 단계와 미완료
보관 자료 조사 4/4 읽기 완료: 실행 기록 1개 + 추출 3개. 이는 수집·읽기 완료율이며 최종 Gate PASS율이 아니다.
다음 조사: analysis/의 실제 계산 파일과 입력 연결, Normalize 원본·QA 입력/출력 존재 여부. 실제 운영 File ID·단계별 원본 SHA·승인 Gold는 담당자 근거 필요.
최종 Gate 완료 입증 0/5 유지. 신규 pytest/Ruff/유료 실행·설정 수정·병합 없음.
