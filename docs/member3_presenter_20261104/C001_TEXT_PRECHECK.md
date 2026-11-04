# C001 보관 텍스트 대조 — 사람 검수 아님

조회 기준 커밋: 1b04e8dddf4b6ee50da81802106147ae6949724f
상태: 보관 TXT 내용 읽기 완료 / PDF 시각 대조 NOT_VERIFIED / HUMAN GOLD 미승인.

## 실제 읽은 파일과 Git blob SHA
| 파일 | Git blob SHA |
|---|---|
| docs/handoff/evidence/pdf-text/SYN-C001_purchase_order.txt | 8dc9beb771c71f9db944b97d26e96db4b6239673 |
| docs/handoff/evidence/pdf-text/SYN-C001_delivery_notice.txt | 31a5e897dfd7e82303f7b1a419000c045ababc89 |
| docs/handoff/evidence/pdf-text/SYN-C001_quotation.txt | fc83a0a8a247ce00f73f480b77c5a38825b879a0 |

위 SHA는 Git blob 식별자다. PDF 원본 SHA-256이 아니며 PDF와 TXT의 바이트·의미 일치 검증도 아니다.

## TXT에서 확인한 값
| 문서 | 확인한 값 | 아직 확인하지 못한 것 |
|---|---|---|
| 발주서 | SYN-C001, PO-DOC, PO1, 기존 입고 2026-11-03, A/R1/100 EA | PDF 페이지·셀 배치·원본 SHA-256 |
| 변경통보 | SYN-C001, NOTICE-DOC, PO1, 기존 2026-11-03 → 변경 2026-11-08, A/R1/100 EA, 수량은 그대로이고 날짜만 변경 | PDF 시각 대조·사람 판단 |
| 견적서 | SYN-C001, QUOTE-DOC, Q1/S1, 참조 PO1, 도착 2026-11-04, 1000.00 KRW/EA, 운송비 500 KRW 견적당 1회, A/60 EA | 실제 계산·주문 선택·승인 여부 |

세 TXT 모두 합성 조달 시험 자료임을 밝히고 재고·고객 주문은 별도 trusted JSON 입력이라고 적고 있다. 견적은 대체 구매 검토용이며 발주 완료가 아니라고 적고 있다.

## 해석 경계
- 60 EA × 1000 KRW/EA + 운송비 500 KRW = 60,500 KRW는 견적 조건에 대한 산술 설명이다. 이번에 Python 엔진을 실행한 결과가 아니다.
- 발주 100 EA와 견적 가능량 60 EA만으로 부족량 0→60을 입증할 수 없다. 재고·고객 주문·배분 입력 및 동일 사례 계산 결과가 필요하다.
- TXT 내용 일치는 PDF 사람 검수·Gold 승인·최신 Studio 추출 정확도를 대신하지 않는다.
- 기존 원본 TXT/PDF/Gold 파일을 수정하지 않았다.
