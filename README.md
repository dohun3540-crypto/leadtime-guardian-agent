# LeadTime Guardian Agent

> Upstage AI Agent Hackathon V.2 | 납기 지연 영향 분석 및 구매 대응 AI Agent

## 프로젝트 개요

**LeadTime Guardian**은 공급업체의 발주서, 납기 변경 통보서, 대체 공급업체 견적서를 분석하고 재고·고객 주문 데이터와 연결하여 **납기 영향과 부족 수량을 정량적으로 계산**하고 **실행 가능한 구매 대응안**을 제안하는 프로젝트입니다.

> **현재 상태: 초기 개발 스캐폴드** — Python 기반 납기 계산 데모는 실행 가능하지만, 실제 Upstage Studio Agent/API, 공개 데이터셋, 웹 UI는 아직 연동되지 않았습니다.

## 핵심 흐름

```text
문서(PDF/이메일/견적서)
   ↓
Upstage Studio: Parse → Classify → Extract → Instruct
   ↓
구조화된 추출 결과(JSON)
   ↓
Python 분석: 기존/변경 납기 + 재고 + 고객 주문 + 대체 업체
   ↓
부족 수량 / 위험도 / 대응 시나리오 / 근거
   ↓
담당자 검토 → 이메일 및 수정 발주 초안
```

## 개발 범위

| 범위 | 목표 |
|---|---|
| MVP | 문서 유형 분류, 필드 추출, 누락 검증, 납기 계산, 재고 부족 분석 |
| 고도화 1 | 대체 업체 비교, 긴급 구매 시나리오, 비용·지연 트레이드오프 |
| 고도화 2 | 판단 근거 표시, 예외 사례 평가, 승인 기반 대응 자동화, 데모 UI |
| 범위 제외 | 실제 외부 업체로 무단 발주·이메일 자동 발송 |

프로젝트는 **문서 이해에 Upstage Studio**, **정확한 수치·재고 계산에 Python**, **의사결정 설명에 LLM**을 사용합니다. Studio 설정 JSON은 Studio에서 실제 구성을 완료한 후 내보내기로 저장합니다.

## 실행 (Python 3.11)

```bash
git clone https://github.com/dohun3540-crypto/leadtime-guardian-agent.git
cd leadtime-guardian-agent
python -m venv .venv
# Windows PowerShell: .\.venv\Scripts\Activate.ps1
# macOS / Linux: source .venv/bin/activate
pip install -r requirements-dev.txt
python scripts/run_demo.py
pytest -q
ruff check .
```

`.env.example`을 `.env`로 복사해 로컬에 보관하세요. **실제 API 키는 절대 커밋하지 않습니다.**

## 파일 구조

```text
.github/                   # CI, Issue/PR 템플릿
configs/schemas/           # 문서 추출 및 납기 분석 JSON Schema
data/sample/               # 공개 가능한 합성 샘플
data/raw/, data/processed/ # 원천·가공 데이터(기본적으로 Git 제외)
docs/                      # 아키텍처, 데이터, 협업 규칙, 로드맵
src/leadtime_guardian/     # 계산 엔진
scripts/run_demo.py        # 오프라인 동작 검증용 데모
tests/                     # pytest
```

## 협업 규칙

전체 규칙은 [docs/TEAM_RULES.md](docs/TEAM_RULES.md)를 확인하세요.

- `main`은 동작 가능한 상태를 유지합니다. 변경은 `feat/`, `fix/`, `data/`, `docs/` 브랜치에서 작업하고 PR을 만듭니다.
- PR에는 실행 방법·테스트 결과·변경 요약을 남깁니다. 가능하면 다른 팀원 1명 이상 검토 후 병합합니다.
- 커밋은 `feat:`, `fix:`, `docs:`, `data:`, `test:`, `chore:` 접두사를 사용합니다.
- 모든 공유 스키마(JSON 키, 필드 의미, 날짜·수량 단위)는 협의 없이 변경하지 않습니다.
- 개인정보·실거래 문서·비밀키를 저장소에 올리지 않습니다. 합성 데이터는 구분 표기합니다.
- 실제 발주·외부 발송은 반드시 담당자 승인을 거칩니다.
- 브랜치 보호는 GitHub Settings에서 별도로 활성화해야 합니다.

## 해커톤 주요 일정 (KST)

| 일시 | 내용 |
|---|---|
| 10/30 09:00 | 플랫폼 준비 설문 / Discord 입장 마감 |
| 10/30 14:00 | 교육 OT |
| 11/02 17:00 | Upstage 온라인 교육 |
| 11/03 | Mission 1 개인 제출 |
| 11/06 | Mission 2 팀 제출 (LMS 정확한 마감 시각 확인) |
| 11/09 13:00 | 오피스아워 질문 마감 |
| 11/10 17:00 | **최종 제출** |
| 11/12 13:00 | 본선 발표 |
| 11/13 | 오프라인 데모데이 |

## 최종 제출물

- [ ] Studio 워크플로우 설정 JSON
- [ ] 테스트 문서 **20건 이상** + 정답 JSON(출력 키 동일) + 케이스 유형표
- [ ] 워크플로우 설계서 1장
- [ ] 데이터셋 실행 결과 JSON
- [ ] 데모 영상
- [ ] 발표자료 PDF
- [ ] 선택: 데모 URL, GitHub 코드

## 참고

- [Upstage Studio 노드 가이드](https://console.upstage.ai/ko/docs/studio/key-features)
- [Upstage Agents API 가이드](https://console.upstage.ai/docs/agents)
- [팀 Ground Rules](docs/TEAM_RULES.md)
- [기술 구조](docs/ARCHITECTURE.md)
- [개발 단계](docs/PROJECT_PLAN.md)

모든 문서·데이터셋의 라이선스와 공개 가능 범위를 확인하세요. 공개 데이터의 배송 지연과 공급업체의 구매 납기 지연은 다른 문제이므로, 공개 데이터는 참고 정보로 사용하고 구매 업무 문서는 명시적으로 합성하여 테스트합니다.
