# γ-Al₂O₃ Literature Study

γ-Al₂O₃(gamma alumina)의 **synthesis / post-treatment condition이 surface 및 defect structure를 어떻게 바꾸며, 어떤 조건에서 reactive하거나 reducible한 γ-Al₂O₃가 형성되는가**를 문헌연구로 규명하고, 최종적으로 **pretreatment strategy를 도출**한다.

> 이 저장소에는 문헌연구의 **방법론과 중간 산출물**이 들어 있다. 본 수집(Tier 1, 5,758건)은 아직 시작하지 않았고, 과학적 결론은 어느 문서에도 없다.

---

## 현재 상태

| 단계 | 내용 | 상태 |
|---|---|---|
| 1–5 | 방법론 확립, seed set 구축·재검토, reducibility 증거 기준, query 설계·시험 | 완료 |
| 6 | Tier 1 코퍼스 수집 및 screening | **다음 단계** |

## 문서 (읽는 순서)

| 파일 | 내용 |
|---|---|
| [`docs/01_methodology.md`](docs/01_methodology.md) | 현행 검색 방법론. 리뷰 유형, source 역할, query 원칙, 중단 기준, screening, LLM 사용 범위와 검증 관문(Gate 1–3) |
| [`docs/02_evidence_framework.md`](docs/02_evidence_framework.md) | reducibility의 정의, 연구 framework(5축·2분기), Jeong 2020 → Ammendola 2011 인용 검증, 증거 등급 Tier A/B/C |
| [`docs/03_seed_set.md`](docs/03_seed_set.md) | seed set v2 (KEEP 18 / OPTIONAL 9 / REMOVE 6)와 선정 근거 |
| [`docs/04_query.md`](docs/04_query.md) | 검색식 전문, 변이별 recall 측정, 미검출 진단, 2-tier 설계, Scopus/WoS 변환형 |

## 데이터

| 파일 | 행 | 내용 |
|---|---|---|
| `data/methodology_references.csv` | 71 | 방법론 근거 문헌 (Crossref 70 + arXiv 1 검증). 본문 인용 키 `[Key]`와 대응 |
| `data/reducibility_references.csv` | 18 | reducibility 개념 문헌. `content_read` 열에 초록 열람(9) / 서지만 검증(9) 표시 |
| `data/reducibility_evidence_criteria.csv` | 12 | Tier A/B/C 기준. 각 기준이 입증하는 것과 **입증하지 못하는 것** |
| `data/seed_set_v2.csv` | 33 | 현행 seed set |
| `data/seed_set_v1_final.csv` / `seed_candidates.csv` | 16 / 21 | v1 seed set과 후보 평가 (이력) |
| `data/known_item_diagnostic.csv` | 27 | seed × query 라운드별 검출 여부, 원인 코드, 조치 |

`process/`에는 각 단계의 실행 계획(JSON)이 과정 기록으로 남아 있다. 그 안의 문서 파일명은 작성 당시의 옛 이름이다.

---

## 핵심 발견 (방법론적)

1. **인용이 주장을 지지하지 않는다.** 연구 동기인 Jeong 2020 SI Fig. 1은 267 °C H₂-TPR(TCD) 피크를 "표면 Al 환원"으로 해석하며 Ammendola 2011을 인용한다. 그러나 원문을 확인해 보니 그 논문은 **CO-TPR** 연구였다. 신호는 594–602 °C에 있었고, 저자 귀속은 **표면 OH의 water-gas shift**였다. 이 발견으로 인용 지지 검증(Gate 3)을 신설했다. → [02 §4](docs/02_evidence_framework.md#4-사례-인용이-주장을-지지하지-않는다)
2. **가설 사슬은 Al(V) → oxygen vacancy에서 끊어진다.** 이 연결은 어느 방향으로도 측정된 적이 없다. Al(V)는 양이온의 배위 상태이고, oxygen vacancy는 산소 결손이다. → [02 §6](docs/02_evidence_framework.md#6-사슬-고리별-증거-감사)
3. **Al³⁺에는 결정적 환원 신호가 원리적으로 없다.** Ce³⁺나 Ti³⁺ 같은 낮은 산화수가 없어서, 입증 부담이 결함상태 분광으로 넘어간다. 현재 γ-Al₂O₃의 Tier A 증거는 0건이다.
4. **OpenAlex의 Elsevier 초록 보유율은 2.6%다.** 그래서 이 분야의 초록 검색은 대부분 제목 검색이 된다. WoS·Scopus 보강을 필수로 격상했다. → [04 §0](docs/04_query.md#0-설계-전제를-뒤집은-관측--openalex-초록-보유율)
5. **단일 query로는 precision과 recall을 함께 얻을 수 없다.** core seed 6/21은 5,758건, 21/21은 93,857건이다. 그래서 2-tier로 설계하고 citation chasing을 recall의 주 담당으로 둔다.
6. **산소 거동의 직접 증거는 촉매 문헌 밖에 있다.** 핵재료·광학(F-center), 금속공학(탄소열 환원), 고온산화(¹⁸O/SIMS) 커뮤니티에 있다. 단, 모두 α상 또는 피막이다.

## 다음 단계

1. Tier 1(5,758건)을 확보한 뒤 제목 screening. 현상별로 분할할 수 있다(reducibility 3,482 / OH 매개 1,675 / defect 반응성 1,195 / 계면 539).
2. Scopus·WoS 보강을 1회 실행하고, OpenAlex 단독 대비 신규 적격 논문 수를 측정.
3. 고온산화·산화피막 문헌 탐색. α상 피막 → γ상 분말 전이 가능성은 별도로 평가.

**미해결**: Tier A 문헌의 존재 여부(A2·A3은 어휘 오염으로 판정 미완), 서지만 검증한 개념 문헌 9편의 원문 확인, 연구 표적 선택(reducibility / defect 반응성 / OH 매개 / 계면).

---

## 표기

| 라벨 | 의미 |
|---|---|
| **[측정]** | 논문이 실제로 측정·계산한 값 |
| **[저자해석]** | 저자가 측정에서 끌어낸 해석 |
| **[문헌정의]** | 문헌이 명시적으로 내린 정의 |
| **[판단]** | 이 프로젝트(분석 보조 AI 포함)의 판단 — 논문의 주장이 아님 |
| ①확립 / ②수정 / ③신규 | 방법론 결정의 출처. 기존 문헌에서 확립됨 / 확립된 것을 이 분야에 맞게 수정함 / 이 프로젝트의 신규 제안(직접 근거 없음) |
| † | 서지만 검증한 문헌. 내용 주장 없이 표준 참조로만 인용 |

### 자주 나오는 용어

| 용어 | 뜻 |
|---|---|
| seed | 이미 알고 있는 핵심 논문. 검색식이 이를 찾는지로 query를 진단한다 |
| recall / precision | 관련 문헌 중 검색에 걸린 비율 / 검색 결과 중 관련 문헌 비율 |
| citation chasing (BWC / FWC) | 참고문헌을 거슬러 가기(backward) / 인용한 문헌을 따라가기(forward) |
| Al(V) | 5배위 알루미늄. 표면에만 있는 저배위 Al site |
| oxygen vacancy | 격자에서 O²⁻가 빠진 자리. cation vacancy(Al 자리의 빈자리, γ-Al₂O₃에 원래 존재)와 다르다 |
| E_Ovac | 산소공공 하나를 만드는 데 드는 에너지. reducibility의 대표 척도 |
| TCD | 열전도도 검출기. 어떤 기체가 변했는지 구별하지 못한다 |
| Tier A/B/C | reducibility 증거로 인정 / 보조 / 불인정 |

---

## 데이터 출처와 검증

- 문헌 탐색과 인용 네트워크에는 OpenAlex API를 썼다.
- 서지 검증에는 Crossref API(preprint는 arXiv API)를 썼다.
- 이 저장소의 모든 DOI는 위 API가 반환한 값이다. 기억이나 추론으로 입력한 것은 없다.
- 출판사 PDF 원문은 저작권 때문에 포함하지 않았다.
- 파이프라인 스크립트는 포함하지 않았다. 질의 문자열은 `docs/04`에 그대로 있어 재현할 수 있다.

*분석 보조: Claude Science. 확정된 사실, 저자의 해석, AI의 추론은 각 문서에서 구분 표기했다.*
