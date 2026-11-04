# C001 입력·보관 계산 출처 점검

읽기 기준: 58be72f858b7af4cc2cc757d782d046cd9bced5e.
수정 범위: 이 보고서만 추가. 기존 PDF·manifest·계산·Gold는 변경하지 않는다.

## 실제 읽은 저장소 파일
- data/cases/SYN-C001/manifest.json — Git blob b29ba89df9d18266717db10ff720ee072adc9b68
- data/cases/SYN-C001/trusted_base_case.json — Git blob 3ef7b5f511381779aef546c8191533530a91c3f6
- data/cases/SYN-C001/local_calculation.NOT_STUDIO.json — Git blob 976ed613ac5565e925f073ab6ac4bebe99ce0e71

## 매니페스트에 기록된 원본 해시
아래는 저장된 선언값을 읽은 것이며 현재 다운로드 바이트를 재계산한 결과가 아니다.

| 파일 | 선언된 SHA-256 | 선언 페이지 |
|---|---|---:|
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 |

manifest는 synthetic=true, studio_executed=false, human_gold_reviewed=false를 기록한다. 이는 이 자료 묶음의 저장 상태이며 프로젝트 전체에 Studio 실행이 없다는 의미로 확대하지 않는다. source는 data/sample/portfolio_case.json을 가리키지만 그 파일은 이번 점검에서 읽지 않았다.

## trusted 입력에서 확인
- case_id SYN-C001, snapshot_date 2026-11-01.
- 품목 A 가용재고 40.
- 주문 O1: 품목 A, 납기 2026-11-05, 수량 100.
- 입고 R1: PO1/A, original_eta 및 eta 2026-11-03, 수량 100.
- quotes=[] 및 documents=[]. 따라서 이 파일 단독으로 견적·변경 문서 반영이 끝난 입력이라고 볼 수 없다.

## 보관 결과에서 확인
provenance는 'offline repository sample; NOT Studio extraction'이다. 결과의 status=OK / execution_status=COMPLETED는 이 오프라인 샘플 내부의 값이며 신규 Studio 성공이 아니다.
- delay_days 5.
- O1 배분 40 / 부족 60 / 기준 부족 0 / 추가 부족 60.
- Q1/S1 공급 옵션 60, 도착 2026-11-04, 단가 문자열 1000.00.
- estimated_quote_cost_krw 문자열 60500.00.
- evidence_verified_against_pdf=false, external_action_taken=false.
- evidence_document_ids는 PO-DOC, NOTICE-DOC를 담는다. 비용 주장에 필요한 QUOTE-DOC가 이 목록에는 없어 견적 근거까지 완전 연결됐다고 판정하지 않는다. 필드 설계 결함인지 여부는 담당자 확인 전 확정하지 않는다.

## 원문과의 설명 수준 점검
이번 대화로 수신한 PDF 본문은 기존 입고 11/03→변경 11/08, 견적 입고 11/04 및 60 EA·단가 1000·운송비 500 견적당 1회를 보여준다. trusted 입력의 주문 납기 11/05와 재고 40을 함께 보면 보관 결과의 부족 60과 비용 60500은 산술상 설명 가능하다. 하지만 실제 adapter→V6 실행 재현, 전체 배분 규칙 검증, Native 입력 해시 연결을 수행한 것은 아니다. 증거 수준은 'PDF 본문 + 저장 JSON 읽기 + 산술 검토'다.

## 판정과 다음 인계
| 항목 | 판정 |
|---|---|
| 매니페스트 해시 선언 3개 확인 | 확인 |
| 다운로드 PDF 해시 재계산·선언값 비교 | NOT_RUN |
| 저장 입력·오프라인 결과 읽기 | 확인 |
| PDF→실제 운영 Job→V6→QA 바이트 연결 | NOT_VERIFIED |
| 최신 Python V6 실행 재현 | NOT_RUN |
| 사람 Gold 승인·공식 정확도 | 미승인 / NOT_MEASURED |

윤현준: 실제 Native를 입력한 V6 결과와 입력/출력 SHA, 버전, 명령·로그를 인계. 견적 비용의 출처 연결 범위 확인.
구도훈: 동일 PDF 입력의 운영 Job/Config/Step/File 및 원본 Native, QA 입력 바인딩 제공.
최유석: PDF SHA 재계산·승인 Gold·평가 적격성 확인.
김민주: 사람 원문 검수와 발표 문구 확정. '오프라인 샘플 결과'는 사용 가능하지만 '신규 Live 검증 완료'로 표현하지 않는다.

이번 작업은 실행이나 사람 승인을 생성하지 않는다. 최종 Gate 통과 입증은 0/5 유지.
