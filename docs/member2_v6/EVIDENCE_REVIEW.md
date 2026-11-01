# PDF 근거 대조표

2026-10-31 KST. C001의 저장된 실제 V4 예측 필드를 PDF의 원문 텍스트와 기계 대조했다. 원본 Studio Evidence는 빈 배열 그대로이며 아래 대조 결과를 예측 JSON에 삽입하지 않았다. 사람 라벨 검수·레이아웃 검증은 완료하지 않았고 evidence_verified_against_pdf=false를 유지한다.

| PDF 파일 | SHA-256 | 페이지 | 필드 | 예측값 | 원문 구절 | 대조 |
|---|---|---|---|---|---|---|
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | po_id | PO1 | PO ID / 발주번호 / PO1 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | original_delivery | 2026-11-03 | Original delivery / 기존 입고일 / 2026-11-03 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | items[0].product_id | A | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | items[0].receipt_id | R1 | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | items[0].quantity | 100 | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_purchase_order.pdf | 9246b69363e3cec3dca7654b14bc7facdb0f762e8ae72c42594f38efabadc930 | 1 | items[0].unit | EA | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | po_id | PO1 | PO ID / 발주번호 / PO1 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | original_delivery | 2026-11-03 | Original delivery / 기존 입고일 / 2026-11-03 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | revised_delivery | 2026-11-08 | Revised delivery / 변경 입고일 / 2026-11-08 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | items[0].product_id | A | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | items[0].receipt_id | R1 | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | items[0].quantity | 100 | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_delivery_notice.pdf | 7a5f7b8f025a79a0751a6b6c41e21292fc62c1c02cdd071048e38a66e4bf7f2b | 1 | items[0].unit | EA | A / R1 / 100 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | po_id | PO1 | Related PO / 참조 발주번호 / PO1 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | items[0].product_id | A | A / 60 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | items[0].quantity | 60 | A / 60 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | items[0].unit | EA | A / 60 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.quote_id | Q1 | Quote ID / 견적번호 / Q1 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.supplier_id | S1 | Supplier ID / 대체 공급업체 / S1 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.arrival_date | 2026-11-04 | Arrival date / 대체 입고일 / 2026-11-04 | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.unit_price | 1000.00 | Unit price / 단가 / 1000.00 KRW / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.shipping_cost | 500 | Shipping cost / 운송비 / 500 KRW (once per quote) | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.currency | KRW | Currency / 통화 / KRW | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.product_id | A | A / 60 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |
| SYN-C001_quotation.pdf | 35c9deddbc06d0cb49c1e45cd859a95b97e2a9cde2ea5931d1f8ffe6dfc3c551 | 1 | quote.capacity | 60 | A / 60 / EA | MACHINE_TEXT_MATCH / 사람 검수 대기 |

C008·C013·C017의 PDF 원문도 읽어 EVIDENCE_TEXT_CHECKS.json에 보존했다. C013 통보서의 PO999, C008 R1=40/R2=60 및 통보 R2=60, C017의 2026년 11월 3일·8일·4일 표기를 확인했다. 이 세 케이스의 실제 V6 예측이 없으므로 추출 정확도나 V6 필드 일치를 판정하지 않았다.
