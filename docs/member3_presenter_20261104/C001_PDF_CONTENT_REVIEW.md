# C001 PDF 본문 AI 대조

상태: PDF 본문 확인 / 사람 검수 NOT_VERIFIED / Gold 미승인.

## 수신 출처
사본 저장소 커밋 83bb46500bf41205f1db91f8213d692110fcf801의 data/cases/SYN-C001/에서 세 PDF를 다운로드하여 대화 자료로 등록했다. 조회한 고정 커밋의 파일이며 최신 통합 PR #3 또는 실제 Studio 입력과 동일하다고 보증하지 않는다.

| 파일 | 대화 파일 ID | 수신 크기(bytes) | Git blob SHA |
|---|---|---:|---|
| SYN-C001_purchase_order.pdf | file_XFd7oMDbyqRtEAAHLMV67f | 24899 | e25b56ec55fa94a7ce6f24545e5d35c800931a03 |
| SYN-C001_delivery_notice.pdf | file_TYb4q4nBX6UrXysejieajU | 26421 | 1e9e33b967b5f9b184feda7db8c0bc508771e8df |
| SYN-C001_quotation.pdf | file_mSaVwf9Jg8GCvLrTbtouo8 | 29272 | c06cb7f37facde545422f37bb348c004605b8960 |

대화 파일 ID는 이번 대화의 첨부 식별자이며 기존 운영 Studio File ID가 아니다. Git blob SHA는 PDF SHA-256이 아니다. SHA-256 재계산 및 실제 운영 입력과 바이트 비교는 미수행.

## 읽힌 PDF 1쪽 본문과 기존 사전 대조표 비교
| 항목 | PDF 본문에서 읽힌 내용 | 비교 결과 |
|---|---|---|
| 발주 식별자 | 발주서: SYN-C001 / PO-DOC / PO1; 입고 R1 | 기존 TXT 사전 대조표와 일치 |
| 발주 수량·일자 | A / R1 / 100 EA; 2026-11-03 | 일치 |
| 변경 식별자·일자 | SYN-C001 / NOTICE-DOC / PO1; 2026-11-03 → 2026-11-08 | 일치 |
| 변경 범위 | A / R1 / 100 EA; 수량 변경 없이 납기만 변경 | 일치 |
| 견적 식별자 | SYN-C001 / QUOTE-DOC / Q1 / S1 / 참조 PO1 | 일치 |
| 견적 가능량·입고일 | A / 60 EA; 2026-11-04 | 일치 |
| 견적 비용 조건 | 1000.00 KRW/EA; 운송비 500 KRW 견적당 1회; KRW | 일치 |

위 7/7은 정한 일곱 비교 항목의 읽힌 본문 일치 수다. 추출 정확도·전체 필드 평가·사람 검수율이 아니며 PDF 이미지 시각 검사를 했다는 뜻도 아니다. 표의 행/열과 문구를 제공된 PDF 분석 본문에서 확인했다.

## 발표 표현에 필요한 제한
- 견적서 1쪽은 대체 구매 검토용 견적이며 발주가 아니라고 명시한다. 구매 실행 완료라고 말하지 않는다.
- 세 PDF 모두 합성 조달 시험 자료라고 명시하며 재고와 고객 주문은 별도 trusted JSON 입력이라고 밝힌다. 실기업 실거래 문서라고 소개하지 않는다.
- 60 × 1000 + 500 = 60,500 KRW는 공급 가능량 전량 구매 가정의 단순 산술이다. 실제 선택 수량과 부족량 0→60은 별도 입력·계산 결과로 검증해야 한다.
- 동일 운영 Job, Native, Python, QA, 승인 Gold는 이번 PDF 읽기만으로 입증되지 않는다.

## 남은 사람 판단
김민주가 원본 PDF의 해당 표와 문구를 직접 보고 HUMAN_REVIEW_WORKSHEET.csv의 7개 항목에 실제 판단·페이지·검수자·시각을 남긴다. 승인 권한이 없으면 검수 사실만 전달한다. 이 AI 대조 기록으로 기존 사람 검수 상태를 승격하지 않는다.

## 재현 위치
각 파일은 https://github.com/oxyznewl/leadtime-guardian-agent-upstage-kmj/tree/83bb46500bf41205f1db91f8213d692110fcf801/data/cases/SYN-C001 에서 확인 가능하다. 본문 근거: 각 PDF 1쪽의 식별자 표·품목 표·조건 문구. 기존 비교 기준: C001_TEXT_PRECHECK.md.
