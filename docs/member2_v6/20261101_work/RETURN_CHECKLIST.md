# Studio에서 개인 Work로 돌려줄 자료

이 문서는 수신 체크리스트이며 실제 실행 기록이나 Native 결과가 아니다. 실제 확인한 값만 별도 기록하고, 미확인 항목을 과거 V4/V5 값으로 채우지 않는다.

| 항목 | 받아야 할 실제 자료 |
|---|---|
| 역할 | 팀원 2 운영 후보 / 팀원 1 독립 QA Sandbox 구분 |
| 설정 | 워크플로우 이름, 워크스페이스, Agent ID, Config ID, 저장 version·시각·확인 화면 |
| 설정 파일 | 변경 전후 Native 설정 export 원본, SHA-256 |
| 케이스 | C001 우선, 이후 C013 → C017 → C008 |
| 실제 입력 | PDF 이름·수·업로드 순서·파일 ID·해시·해시 출처 |
| 실제 실행 | Job ID, 시작/완료/실패 시각, 상태, Step ID·이름·유형·상태 |
| 최종 출력 | 수정하지 않은 Native final JSON. 다운로드 성공 여부를 실행 완료와 구분 |
| 중간 출력 | 다운로드 가능한 Parse/Classify/각 Extract/Merge/Instruct 원본 JSON |
| 실패 | 실패 단계, 오류의 비밀 없는 요약, 원본 보존 여부 |
| 근거 | 실제 metadata/warnings/evidence. 없는 좌표·confidence·페이지 근거 생성 금지 |

Native 원본을 먼저 전달한다. documents를 수동 수정하거나 개인 Work의 분석 JSON을 Studio 원본으로 바꾸지 않는다. 스키마 통과·Studio COMPLETED·Python OK·독립 QA·사람 Gold 검수는 각각 별도 상태다. 키·토큰·쿠키·인증 헤더는 전달하지 않는다.
