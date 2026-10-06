# γ-Al₂O₃ Surface Chemistry & Defect Engineering — Literature Study

2026 생명화학공학과 학부 졸업연구. γ-Al₂O₃(gamma alumina)의 **synthesis / post-treatment condition이 surface·defect structure를 어떻게 바꾸며, 어떤 조건에서 unusually reactive하거나 potentially reducible한 γ-Al₂O₃가 형성되는가**를 체계적 문헌연구(systematic scoping / mapping)로 규명한다.

최종 목표는 개별 논문의 synthesis recipe 나열이 아니라 **general synthesis / pretreatment strategy의 도출**이다.

> 이 리포지토리는 **문헌연구의 방법론과 중간 산출물**을 기록한다. 본격적인 문헌 수집(Tier 1, 5,758건)은 아직 시작 전이며, 과학적 결론은 어느 문서에도 들어 있지 않다.

---

## 현재 상태

| Phase | 내용 | 산출물 | 상태 |
|---|---|---|---|
| 1 | 문헌검색 방법론 확립 (v1) | `docs/01` + `data/methodology_references.csv` | 완료 |
| 2 | Seed set v1 구축 (16편) | `docs/02` + `data/seed_set_v1_final.csv` | 완료 |
| 3 | Seed set 비판적 재검토 (v2) | `docs/03` + `data/seed_set_v2.csv` | 완료 |
| 4 | "Reducibility" 개념 검증 + 증거 등급 확정 | `docs/04` + `data/reducibility_*.csv` | 완료 |
| 5 | Query v1 설계 + known-item diagnostic + 방법론 v2 | `docs/05`, `docs/06`, `data/known_item_diagnostic.csv` | 완료 |
| 6 | Tier 1 코퍼스 수집 및 screening | — | **다음 단계** |

---

## 디렉터리

```
docs/    방법론·분석 보고서 (Markdown, 작성 순서대로 번호)
data/    검증된 서지 표 및 측정 결과 (CSV)
process/ 각 단계의 실행 계획 (JSON, 과정 기록용)
```

### docs/

| 파일 | 내용 |
|---|---|
| `01_literature_methodology_v1.md` | 채택한 Literature Search Methodology v1과 6개 핵심 결정의 근거. 방법론 문헌 71편에 기반. |
| `02_seed_set_analysis.md` | 초기 seed 4편 분석, coverage·bias 진단, 결손 범주 도출, 후보 탐색 → seed set v1(16편). |
| `03_seed_set_v2_review.md` | Seed set 비판적 재검토. Ammendola 2011 원문 검증, `Al(V) → oxygen vacancy → reducibility` 사슬 감사. KEEP 18 / OPTIONAL 9 / REMOVE 6. |
| `04_reducibility_criteria.md` | "Reducibility"의 문헌상 정의 검증과 **Tier A/B/C 증거 등급** 확정. 4단계 선형 framework → 5축·2분기 구조로 개정. |
| `05_query_v1.md` | Query v1 facet 어휘 전문, 11개 변이의 결과 수·recall 측정, 미검출 원인 진단, 2-tier 설계, Scopus/WoS 변환형. |
| `06_literature_methodology_v2.md` | v1 대비 개정 8항목. Gate 3 신설, S0.5 단계 신설 등 — 전부 Phase 5의 실측에 근거. |

### data/

| 파일 | 행 수 | 내용 |
|---|---|---|
| `methodology_references.csv` | 71 | 방법론 문헌. Crossref 검증 70 + arXiv API 검증 1 = **71/71 검증 완료**. |
| `seed_candidates.csv` | 21 | Gap-filling seed 후보와 다양성 기여 판정. |
| `seed_set_v1_final.csv` | — | Seed set v1 (16편). |
| `seed_set_v2.csv` | 33 | Seed set v2. KEEP 18 / OPTIONAL 9 / REMOVE 6. |
| `reducibility_references.csv` | 18 | Reducibility 개념 검증에 쓴 문헌. 9편 abstract 정독, 9편 서지만 검증(해당 행에 표시). |
| `reducibility_evidence_criteria.csv` | 12 | Tier A/B/C 기준표. 각 행에 "무엇을 입증하는가 / 무엇을 입증하지 **못하는가** / γ-Al₂O₃ 현황". |
| `known_item_diagnostic.csv` | 27 | Seed 27편(core 21 + boundary 6) × query 라운드별 검출 여부·원인코드·조치. |

---

## 연구 framework (v2)

Phase 4에서 4단계 선형 사슬을 폐기하고 다음 구조로 개정했다. 선형 사슬은 reducibility와 reactivity를 한 칸에 묶어 **"반응성이 있으므로 환원된다"는 오류를 구조적으로 내장**하고 있었기 때문이다.

```
[P] Processing  →  [S] Structure  →  ┌ [O1] OH / water chemistry      ┐   ┌ [R1] surface reactivity
                                     ├ [O2] lattice-oxygen mobility   ├ → ┤
                                     └ [O3] oxygen removal            ┘   └ [R2] reducibility
                                                  [I] metal/oxide interface (병렬 경로)
```

연구 표적(reducibility / defect-site reactivity / OH-mediated oxygen transfer / metal-oxide interface)은 **아직 선택하지 않았다**. v2 framework는 네 경로를 모두 수용하도록 설계되어, 표적 확정 없이도 mapping을 진행할 수 있다.

---

## 핵심 방법론 규칙

### 서지·주장 검증 3-Gate

| Gate | 대상 | 통과 조건 |
|---|---|---|
| **Gate 1** | 서지 레코드 (DOI·제목·저자·연도·venue) | Crossref(또는 preprint는 arXiv API) 대조 일치. LLM은 서지정보를 **생성하지 않는다** — 실제 API가 반환한 레코드를 판정만 한다. |
| **Gate 2** | 추출된 과학적 주장 | 원문 내 **verbatim span** 일치 + 출처 위치(page/section/figure/table) + 실험 방법·조건 기록 + `measured_fact` / `author_interpretation` / `ai_inference` 3분류. |
| **Gate 3** | **인용이 실제로 주장을 지지하는가** | 실험 종류·조건 범위·귀속·주장 존재 여부 대조. 판정값 `supported` / `partially_supported` / `not_supported` / `unreadable`. 전문 정독 필요, 중심 주장에만 적용. |

Gate 2의 필요성은 추정이 아니라 측정이다 — LLM이 추출한 인용문 131개 중 **8개(6.1%)가 초록을 함께 제공했음에도 verbatim 검증에 실패**했다.

Gate 3은 Phase 3에서 발견한 실제 사례 때문에 신설했다(아래 참조).

### 불변 규칙

- Al(V), low-coordinate Al, surface defect, oxygen vacancy의 보고는 **그 자체로 γ-Al₂O₃의 reducibility 증거가 아니다**.
- TCD 피크나 H₂ 소모량 자체는 **oxygen removal의 직접 증거가 아니다**.
- Tier C 증거만으로는 reducibility 관련 서술을 할 수 없다.
- 서지정보를 확인할 수 없으면 `unverified`로 표시하고 **evidence synthesis에서 격리**한다.
- 논문·DOI·수치·실험조건·mechanism을 임의 생성하지 않는다.

---

## 주요 발견 (방법론적)

### 1. 인용 사슬이 끊어져 있다 — Gate 3 신설의 계기

이 연구의 출발점은 Jeong et al., *Nat. Catal.* **3**, 368 (2020) [`10.1038/s41929-020-0427-z`]의 Supplementary Fig. 1 — 신선 γ-alumina에서 **267 °C의 큰 H₂-TPR TCD 피크**가 "weakly coordinated surface aluminum의 환원"으로 캡션되어 있고, SI 참고문헌 1을 인용한다.

그 SI 참고문헌 1(Ammendola et al., *Surf. Sci.* **605**, 1812 (2011) [`10.1016/j.susc.2011.06.018`]) 원문을 확보해 읽은 결과:

- 이 논문은 **CO-TPR** 연구이며, **bare alumina의 H₂-TPR은 논문에 존재하지 않는다**.
- CO 소모는 ~400 °C에서 시작해 **594–602 °C**에서 최대 — 267 °C와 무관하다.
- 저자들의 귀속은 환원이 아니라 **surface OH와 CO의 water-gas shift**다: *"Pure and La-stabilized γ-Al₂O₃ reacted with CO at T ≥ 400 °C through a WGS reaction involving surface OH groups producing CO₂ and H₂."*
- 저자들은 오히려 **반대 방향의 경고**를 남겼다: *"quantitative results must be carefully analysed by taking into account hydrogen production associated with the WGS reaction."*

즉 **인용된 근거는 인용한 주장을 지지하지 않는다.** 서지정보는 완벽히 정확하므로 Gate 1·2로는 잡히지 않는다 → Gate 3이 필요하다.

부수 발견: **Supplementary 파일의 참고문헌 목록은 OpenAlex `referenced_works`에 포함되지 않는다.** 자동 backward citation chasing이 구조적으로 놓치므로 SI 수동 확인 절차를 방법론에 추가했다.

### 2. 사슬은 ②번 고리에서 끊어진다

| 고리 | 증거 강도 |
|---|---|
| ① Processing → Al(V) 생성 | **강함** (단 ²⁷Al NMR의 field·spinning 의존성 주의: Jeong 9.4 T vs Kwak 21.1 T) |
| ② **Al(V) → oxygen vacancy** | **양방향 모두 독립 증거 없음** |
| ③ oxygen vacancy → 제거 용이성 | 중간, 전부 "어렵다" 방향 (θ-Al₂O₃ E_Ovac 5.46 eV; ¹⁸O 교환 최대 620 °C vs CeO₂ 410 °C) |
| ④ 267 °C TCD 피크 → oxygen removal | **근거 없음** |

주의해야 할 혼동 하나: Prins (2020)가 논하는 γ-Al₂O₃의 "vacancy"는 **cation vacancy**로, 구조식 (Al_T)(Al_O)₅ᐟ₃(V_O)₁ᐟ₃(O)₄에 내재한 정상적 화학량론적 특징이다 — **oxygen vacancy가 아니다**.

### 3. Al³⁺에는 결정적 신호가 원리적으로 없다

Reducibility의 표준 정의는 lattice oxygen 제거 비용(E_Ovac)이며, 환원의 완결 신호는 **산소가 떠나는 것 + 남은 전자가 어디에 국재하는지**의 두 부분이다. CeO₂는 Ce³⁺, TiO₂는 Ti³⁺로 후자를 직접 보인다. 그러나 **Al³⁺는 산화물 격자 내에서 접근 가능한 낮은 산화상태를 갖지 않으므로**, 결정적 cation 신호가 원리적으로 쓸 수 없다. 입증 부담은 전적으로 defect-state 분광학으로 넘어가는데, γ-Al₂O₃ 촉매 문헌에는 그 측정 전통이 사실상 없다.

### 4. 검색 설계 — 측정이 전제를 뒤집었다

**OpenAlex abstract 보유율** (제목에 γ-Al₂O₃ 표기를 포함한 600편 표본):

| 출판사 | 보유율 | 편수 |
|---|---|---|
| **Elsevier BV** | **2.6 %** | **422** |
| ACS | 100 % | 96 |
| RSC / Wiley | 100 % / 93.8 % | 16 / 16 |
| Springer | 4.8 % | 21 |
| 전체 | 27.2 % | 600 |

연도와 무관하다(2000년대 21 %, 2010년대 28 %). 이 분야 중심 저널(*J. Catal.*, *Appl. Catal. A/B*, *Catal. Today*, *Surf. Sci.*)이 전부 Elsevier이므로, **abstract 기반 Boolean 검색은 코퍼스 약 73 %에 대해 제목만 긁는 검색으로 퇴화한다.** 이것이 WoS/Scopus 보강을 optional에서 **필수**로 격상시킨 근거다.

**Query 변이별 trade-off** (core seed 21편 기준):

| Query | 결과 수 | core seed 검출 |
|---|---|---|
| γ 표기 요구 + 현상 facet | **5,758** | **6 / 21** |
| 넓은 물질어 + 현상 facet (어휘 교정) | 67,886 | 19 / 21 |
| + probe facet | 82,261 | 20 / 21 |
| union | **93,857** | **21 / 21** |

6→21편 recall에 결과 수가 **16배**다. 단일 Boolean query로 쓸 만한 precision과 known-item recall을 동시에 달성하는 것은 이 분야에서 불가능하다 → **2-tier 설계**를 채택했다.

측정에서 직접 따라 나온 두 결정:

- **γ상 지정을 query에 요구하면 core seed의 71 %를 잃는다** → γ 판정은 검색식이 아니라 **screening 기준**으로 이전.
- **Treatment facet을 넣으면 손해다** — 결과는 17 %만 줄고(67,886 → 56,350) core seed 검출은 19/21 → **11/21로 붕괴**. 처리 조건은 제목·초록이 아니라 본문 Experimental에 있다 → 검색 facet이 아니라 **추출 필드**로.

### 5. 미검출 원인은 전부 달랐다

| Seed | 원인코드 | 진단 |
|---|---|---|
| Amenomiya 1978 | TERM | 제목이 "water-gas **conversion**", 어휘집엔 "shift"만 |
| Knözinger 1978 | TERM | "surface sites / surface models" 어휘 부재 |
| Ingram-Jones 1996 | LOGIC | `dehydroxylation`을 Treatment facet에만 배정 → 2-facet 질의에서 탈락. **facet은 배타적 분할이 아니다** |
| Morterra 1996 | TERM+FIELD | abstract 없음 + 제목이 probe 어휘 |
| **Prins 2020** | **FIELD** | 제목이 "On the structure of γ-Al₂O₃"**뿐**, abstract 없음 → **어떤 query로도 도달 불가** |

마지막 항목이 citation chasing을 보조가 아니라 **recall의 주 담당**으로 만드는 직접 근거다.

### 6. 증거는 촉매 문헌 **밖**에 있다 — 세 번의 독립 확인

| 커뮤니티 | 보유한 증거 | 전이 가능성 |
|---|---|---|
| 핵재료 · 광학 | 산소공공 분광(F-center, EPR) | 중성자 조사 **α**-Al₂O₃ 단결정 — 개별 평가 필요 |
| 금속공학 | 벌크 환원 조건(탄소열 환원) | 조건이 촉매 영역과 동떨어짐 |
| 고온산화 · 산화피막 | **¹⁸O/SIMS 산소 수송 추적** | alumina **scale** — γ상 분말로의 전이 가능성 개별 평가 |

γ-Al₂O₃ 촉매 커뮤니티는 defect를 Al 배위수와 OH로 기술하며 oxygen vacancy를 직접 재지 않는다. 이는 **"산소공공이 없다"가 아니라 "측정 전통이 없다"**이다.

---

## 다음 단계

1. **Tier 1 코퍼스(5,758건) 획득 후 제목 screening.** 현상별 분할 가능: reducibility 3,482 / OH-mediated 1,675 / defect reactivity 1,195 / interface 539.
2. **Scopus / WoS 보강 1회 실행** (`docs/05` §6의 변환형 사용) 후 OpenAlex 단독 대비 신규 적격 논문 수를 측정해 "필수" 판정을 정량 확인.
3. **고온산화 · 산화피막 커뮤니티 탐색** (*Oxidation of Metals*, *Corrosion Science*, *Acta Materialia*) — alumina scale의 ¹⁸O tracer 연구. α-scale → γ-powder 전이 가능성은 별도 평가.

### 미해결 항목

- **Tier A 문헌이 존재하는지 자체가 미확정.** A1(H₂O 정량 + TPR)은 36건이고 전부 담지금속계여서 희소성이 확정됐으나, A2(재산화/OSC)·A3(defect state 분광)은 ceria·담지금속 어휘 오염으로 판정 미완. alumina 자체로 좁히는 질의가 필요하다.
- Reducibility 참고문헌 18편 중 **9편이 서지만 검증된 상태**다. Gate 3 자체 기준에 따르면, 이들에 기대는 개념 주장은 전문 확보 전까지 잠정적이다.
- **연구 표적 미선택** (reducibility / defect reactivity / OH-mediated / interface).

---

## 데이터 출처와 검증

| 역할 | 사용 |
|---|---|
| 문헌 탐색 · 인용 네트워크 | OpenAlex API |
| 서지 메타데이터 검증 | Crossref API (`/works/{doi}`) |
| Preprint 검증 | arXiv API (arXiv DOI는 Crossref에 없음) |
| 보강 탐색 | Scopus / Web of Science (PRISMA-S 수준 기록 필요) |
| 전문 | 출판사 · OA 경로 |

이 리포지토리의 모든 DOI는 위 API가 반환한 값이며, 어느 것도 기억이나 추론으로 입력하지 않았다.

---

## 포함하지 않은 것

- **출판사 PDF 원문** — 저작권. 모든 논문은 DOI로 식별되어 있다.
- **파이프라인 스크립트** — 현 단계 산출물을 문서로 한정하기로 결정. 질의 문자열은 `docs/05`에 그대로 수록되어 재현 가능하다.

---

*분석 보조: Claude Science. 모든 서지정보는 학술 API에서 직접 취득해 검증했으며, LLM이 생성한 서지정보는 포함되지 않는다. 확정된 사실 / 저자의 해석 / AI의 추론은 각 문서 내에서 구분 표기되어 있다.*
