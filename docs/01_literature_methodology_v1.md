# Literature Search Methodology v1
### γ-Al₂O₃ surface chemistry & defect engineering 문헌연구를 위한 검색 방법론 결정서

**문서 성격**: 방법론 해설집이 아니라 **채택 결정서(decision record)**. 각 결정마다 `채택안 / 근거 / 기각한 대안 / 재검토 조건(trigger)`을 기록한다.
**작성 시점 기준**: 2026-10
**근거 문헌**: 71편 (전부 독립 source로 서지검증 완료 — `methodology_references.csv`)

---

## 0. 이 문서의 범위와 읽는 법

### 0.1 목적

본 단계의 목적은 "literature-search methodology를 완전히 리뷰하는 것"이 **아니라**, γ-Al₂O₃ 문헌연구를 시작하기 위해 반드시 확정해야 하는 **6개 methodological decision을 근거 있게 닫는 것**이다.

| # | 결정(decision) | 한 줄 질문 |
|---|---|---|
| D1 | Review methodology 축 + execution/automation 축 | 어떤 종류의 review를 하며, 그것을 어떤 수단으로 실행하는가? |
| D2 | Source 역할 분리 | discovery / verification / citation / full-text 각각에 어떤 source를 쓰는가? |
| D3 | Query 개발·검증 | query를 어떻게 만들고 그것이 쓸 만한지 어떻게 확인하는가? |
| D4 | Completeness 평가·중단 | "충분히 찾았다"를 어떻게 판단하고 언제 멈추는가? |
| D5 | Screening | 모은 논문을 어떤 절차로 거르는가? |
| D6 | AI/LLM 허용 범위와 validation gate | LLM을 어디까지 쓰고 무엇으로 막는가? |

### 0.2 명시적 비목표 (non-goals)

- systematic review methodology 전반의 망라적 서베이
- γ-Al₂O₃ 논문의 대량 수집 또는 과학적 결론 도출 (다음 단계)
- 파이프라인 코드 구현 (다음 단계 — 본 문서는 설계 명세까지)

### 0.3 라벨 체계

모든 권고에 다음 라벨을 붙인다.

| 라벨 | 의미 |
|---|---|
| **①확립** | 기존 방법론 문헌/공식 guideline에서 확립된 practice. 그대로 채택. |
| **②수정** | 확립된 practice이지만 chemistry/materials science 적용을 위해 수정이 필요. |
| **③신규** | 이 프로젝트를 위해 새로 제안하는 workflow. 직접적 근거 문헌 없음 — 가설 수준. |

근거의 출처 분야도 함께 표시한다: `[biomed]` `[소프트웨어공학]` `[환경과학]` `[정보학/scientometrics]` `[materials/chemistry]`.

### 0.4 ⚠ 근거 기반의 구조적 한계 (먼저 읽을 것)

본 문서가 인용하는 71편 중 **chemistry/materials science에서 직접 생산된 방법론 근거는 3편뿐**이다 ([Baykoucheva2011] 화학 DB 비교, [Polak2024] / [Dagdelen2024] 재료 데이터 LLM 추출). 나머지는 biomedical, 정보학/scientometrics, 소프트웨어공학, 환경과학에서 왔다.

이것은 본 문서의 결함이 아니라 **분야의 상태**다. search methodology 연구는 임상의학에서 발달했고 재료·촉매 분야에는 이에 상응하는 방법론 문헌이 사실상 없다. 따라서 본 문서의 상당수 결정은 "직접 근거"가 아니라 **"인접 분야에서 전이한 근거 + 전이 타당성에 대한 논증"**이다. 전이가 깨지는 지점은 §9에서 별도로 다룬다.

---

## 1. 결정 D1 — Review methodology 축과 execution/automation 축의 분리

### 1.1 두 축을 왜 분리하는가

흔한 혼동은 "AI-assisted review"를 narrative/systematic/scoping/mapping과 **같은 층위의 review 유형**으로 취급하는 것이다. 이는 범주 오류다. 전자는 *무엇을 하는가*(질문 유형과 추론 구조)이고, 후자는 *어떤 수단으로 하는가*(실행 방식)이다. LLM으로 실행한 scoping review는 여전히 scoping review이며, 수작업으로 한 systematic review와 동일한 보고 기준을 적용받는다.

실제로 automation 문헌은 스스로를 review 유형이 아니라 **공정 가속 수단**으로 규정한다. [Marshall2019]은 automation이 search, screening, data extraction 등 systematic review의 대부분 단계를 "expedite"하기 위해 제안·사용되어 왔다고 정리한다. 즉 automation은 단계에 얹히는 layer이지 단계의 종류를 바꾸지 않는다.

따라서 본 문서는 두 축을 분리해 각각 결정한다.

```
축 A (review methodology)  : 무엇을 하는 연구인가  → 질문 유형, 포함 기준, 종합 방식, 보고 기준
축 B (execution/automation): 어떻게 실행하는가     → 수작업 / API 반자동 / LLM 보조
                              ↑ 축 A의 어느 유형에도 독립적으로 결합 가능
```

**라벨: ③신규** — 이 분리 자체를 명시적으로 규정한 guideline은 찾지 못했다. 다만 [Marshall2019], [Ofori-Boateng2024], [OMara-Eves2015]가 automation을 단계별 보조 수단으로만 다루는 것과 정합적이다.

### 1.2 축 A — review 유형 비교

| 유형 | 핵심 질문 | heterogeneity 허용도 | 산출물 | 본 연구 적합성 |
|---|---|---|---|---|
| Narrative review | "이 분야를 어떻게 이해할 것인가" | 매우 높음 | 서술적 종합 | ✗ 재현성 없음 |
| Systematic review | "특정 효과가 있는가" | 낮음 (동질적 설계 전제) | 효과 추정 / 구조화 종합 | ✗ meta-analysis 불가 |
| Scoping review | "어떤 증거가 존재하며 gap은 어디인가" | 높음 | 증거 지도 + gap | ◎ |
| Systematic mapping | "증거가 어떤 범주에 얼마나 분포하는가" | 높음 | 분류 체계 + 빈도 | ◎ |
| Bibliometric analysis | "연구 활동이 어떻게 구조화되어 있는가" | 해당 없음 | 계량 지표 / 네트워크 | △ 보조적 |

근거:

- 유형 선택 자체가 비자명한 문제다. [Grant2009]은 SALSA 프레임으로 14개 review 유형을 분석하면서, 명시적으로 규정된 방법론을 가진 유형은 소수이며 유형들이 상호배타적이지도 않다고 지적한다. [Sutton2019]은 48개 review 유형을 7개 family로 분류하고, '전통적' systematic review를 벗어나면 정의와 검색 요구사항이 여전히 불확실하다고 본다. → **유형을 고른 뒤 "그 유형의 표준 절차"를 그대로 가져오면 된다는 기대는 성립하지 않는다.**
- [Munn2018]은 지식 gap 식별, 문헌 범위 파악, 개념 명료화, 연구 수행 방식 조사가 목적이라면 systematic review 대신 scoping review가 적절하다고 본다. 본 연구 질문("어떤 처리 조건이 어떤 표면/결함 변화를 만들며, 그중 무엇이 실제 관측 가능한 reduction 거동과 연결되는가")은 효과 크기 추정이 아니라 **증거 지형 파악 + gap 식별**이므로 여기에 해당한다. [Munn2018]은 또한 scoping review가 포함 기준과 질문의 타당성을 확인하는 systematic review의 선행 단계가 될 수 있다고 본다 — 학부 졸업연구의 위치로 적절하다.
- [Petersen2008]은 systematic map과 systematic review가 목표·범위·타당성 쟁점에서 근본적으로 다르며 상호 대체가 아니라 상호 보완으로 쓰여야 한다고 규정한다. 또한 mapping study의 분석은 분류 체계 내 범주별 출판 빈도에 초점을 두어 연구 분야의 coverage를 드러내는 것이라고 설명한다. → 본 연구의 "synthesis condition × surface property" 분류표는 정확히 mapping의 산출물이다.
- 절차 프레임은 [Arksey2005]의 scoping study 프레임워크와 이를 정교화해 study selection과 data extraction을 반복적(iterative) 팀 작업으로 규정한 [Levac2010]을 따른다.
- narrative review 기각 근거: [Snyder2019]는 전통적 문헌고찰이 특정 방법론을 따르지 않고 임기응변적으로 수행되어 철저성과 엄밀성이 결여되는 경우가 많다고 지적한다.
- bibliometric 단독 기각: [Donthu2021]과 [Marzi2024]는 계량 분석의 절차를 제시하지만, [Marzi2024]는 계량 분석을 systematic review·이론 개발과 결합하는 10단계 B-SLR 과정을 제안한다 — 즉 계량 분석은 그 자체로 mechanism 질문에 답하지 못하고 결합되어야 한다.

### 1.3 축 A 결정

> **채택: Systematic scoping/mapping review (hybrid)**
> — scoping review의 질문 구조·반복적 절차 + systematic mapping의 분류 체계·빈도 분석.
> 보고는 **PRISMA-ScR**([Tricco2018]: 필수 20항목 + 선택 2항목 — [Page2021]의 PRISMA 2020을 scoping review용으로 확장한 것), 검색 보고는 **PRISMA-S**(§3).
> 계량 분석(bibliometric)은 "연구 활동이 어디에 몰려 있는가"를 보여주는 **보조 도구로만** 사용하며, 인과·기전 주장의 근거로 쓰지 않는다.

**라벨: ②수정** — scoping/mapping 프레임 자체는 ①확립이나, 원전이 모두 보건·소프트웨어공학 맥락이라 추출 항목(§8)을 재료과학용으로 재정의해야 한다.

**기각한 대안과 이유**

| 대안 | 기각 사유 |
|---|---|
| Full systematic review | 실험 조건(precursor, 소성 온도·분위기, 전처리 이력)이 논문마다 달라 효과 추정을 위한 pooling이 불가능. risk-of-bias 도구도 재료 실험에 존재하지 않음 (§9) |
| Narrative review | 재현 불가 — [Snyder2019] |
| Bibliometric 단독 | surface/defect mechanism 질문에 답하지 못함 |
| Meta-analysis | 위와 동일 + 공통 효과 척도 부재 |

**재검토 trigger**: 수집 결과 특정 하위 질문(예: "calcination 온도 → Al(V) 분율")에 대해 **측정 프로토콜이 충분히 동질적인 연구가 10편 이상** 모이면, 그 하위 질문에 한해 정량 종합(최소한 조건-값 산점도)을 추가 검토한다.

### 1.4 축 B 결정

> **채택: API 기반 반자동 파이프라인 + LLM을 "판정자(judge)"로만 사용하는 layer**
> LLM은 API가 반환한 실제 레코드와 실제 full text에 대해서만 판단하며, 서지정보나 과학적 사실을 **생성하지 않는다**. 상세는 D6(§6).

근거: [OMara-Eves2015]는 study identification에서 text mining을 자동 배제 수단으로 쓰는 것은 "유망하지만 아직 충분히 입증되지 않았다"고 평가하며, 고도로 기술적/임상적 영역에서 상대적으로 더 신뢰할 수 있다고 본다. 즉 자동화는 **보조**까지는 근거가 있으나 **대체**에는 근거가 부족하다.

**라벨: ①확립** (automation을 보조로 한정하는 것) + **③신규** (judge-only 아키텍처의 구체적 규정).

---

## 2. 결정 D2 — Source의 역할 분리

### 2.1 왜 "DB 비교"가 아니라 "역할 분리"인가

"어느 데이터베이스가 가장 좋은가"는 잘못된 질문이다. 한 source가 모든 역할에서 동시에 최선인 경우는 없기 때문이다. 대표적 반례가 Google Scholar다.

[Gusenbauer2018]은 Google Scholar가 3억 8,900만 레코드로 가장 포괄적인 학술 검색엔진이라고 보고한다. 동시에 [Gusenbauer2019]는 28개 검색 시스템을 query 기반으로 평가해, 절반만이 상당한 단서 없이 evidence synthesis에 권장될 수 있으며 Google Scholar는 주 검색 시스템으로 부적절함을 보인다. [Martin-Martin2020]은 같은 Google Scholar가 전체 인용의 88%를 찾아내며 다른 source가 찾은 인용을 거의 모두 포함한다고 보고한다.

이 셋은 모순이 아니다. **coverage는 최고, 재현 가능한 Boolean 검색 능력은 미달**이라는 뜻이다. 따라서 Google Scholar는 *discovery의 주 엔진*으로는 부적격이지만 *보조 확인 도구*로는 유용하다. 같은 논리가 모든 source에 적용되므로, 결정의 단위는 DB가 아니라 **역할(role)**이어야 한다.

[Visser2021]은 Scopus, Web of Science, Dimensions, Crossref, Microsoft Academic을 대규모 비교하면서 포괄적 coverage와 유연한 필터 집합의 결합이 중요하다고 강조한다 — 단일 source 선택이 아니라 조합 설계가 요점이라는 것이다. 조합의 효과는 정량적으로도 보고되어 있다: [Bramer2017]은 Embase·MEDLINE·Web of Science Core Collection·Google Scholar의 조합이 전체 recall 98.3%, 분석 대상 리뷰의 72%에서 recall 100%를 달성했고 단일 DB 중에서는 Embase가 가장 많은 고유 문헌(n=132)을 제공했다고 보고한다. 다만 이 조합은 biomedical 대상이므로 본 분야에 그대로 전이되지 않는다.

### 2.2 역할 × source 매트릭스

| 역할 | 채택 (primary) | 보강 (supplementary) | 금지/비채택 |
|---|---|---|---|
| **(a) Literature discovery** | OpenAlex API | WoS / Scopus (수동 export), SciFinder·Reaxys, arXiv | Google Scholar를 주 엔진으로 사용 |
| **(b) Bibliographic metadata verification** | Crossref API | arXiv API (preprint DOI), publisher 레코드 | OpenAlex 단독 자기검증, LLM |
| **(c) Citation network (BWC/FWC)** | OpenAlex (`referenced_works` / `cited_by`) | Semantic Scholar / S2ORC, WoS Core Collection | — |
| **(d) Full text** | Publisher / OA 원문 (PDF·XML) | S2ORC, PMC | abstract만으로 claim 추출 |
| **(e) Retraction·integrity check** | OpenAlex + Crossref retraction 표시 | WoS | 확인 생략 |

### 2.3 각 역할의 근거

**(a) Discovery — OpenAlex를 주 엔진으로**

- [Culbert2025]은 1,680만 건 규모에서 OpenAlex의 평균 참고문헌 수와 내부 coverage 비율이 Web of Science 및 Scopus와 비견될 만하다고 보고한다. 즉 구독 DB 대비 치명적 결손이 있다는 전제는 더 이상 성립하지 않는다.
- [Delgado-Quiros2024]는 Dimensions, OpenAlex, Scilit, The Lens 같은 third-party 데이터베이스가 Google Scholar·Microsoft Academic·Semantic Scholar 같은 academic search engine보다 메타데이터 품질과 완전성이 높다고 보고한다.
- [Simard2024]는 diamond·gold open access 저널의 coverage가 WoS와 Scopus에서 더 낮다고 보고한다. 촉매·재료 분야의 OA 저널 비중을 고려하면 OpenAlex 기반 discovery가 오히려 유리할 수 있다.
- 한계도 기록한다: [Culbert2025]은 OpenAlex가 ORCID는 더 많이, abstract는 더 적게 수집한다고 보고한다 (→ abstract 결손 시 full-text 경로 필요). [Cespedes2025]는 OpenAlex의 언어 메타데이터가 부정확해 영어를 과대, 기타 언어를 과소 추정한다고 보고한다 (→ 언어 필터를 신뢰하지 말 것).

**(b) Verification — Crossref를 discovery가 아니라 검증 source로**

이것이 본 결정의 핵심이다. Crossref는 **DOI 등록 기관**이며 그 레코드는 출판사가 기탁한 것이다. 따라서 Crossref의 가치는 "무엇을 찾아주는가"가 아니라 **"이 DOI가 가리키는 서지 레코드의 정준(canonical) 형태가 무엇인가"**에 있다. [Visser2021]이 Crossref를 Scopus·WoS와 나란히 비교 대상 데이터 source로 다룬 것과 [Harzing2019]가 Crossref와 Dimensions를 Google Scholar·Microsoft Academic·Scopus·WoS와 비교한 것은 Crossref가 독립적 비교 기준점으로 쓰일 수 있음을 보여준다.

> **운영 규칙**: discovery에서 얻은 모든 레코드는 Crossref에서 DOI로 재조회해 **title / authors / year / venue**를 대조한다. 불일치 시 채택하지 않는다 (Gate 1, §6.3).

**이 세션에서의 실측 (observed)**: 본 문서의 근거 71편을 이 규칙으로 처리한 결과 —
- 70/71이 Crossref에서 확인됨.
- 1건은 arXiv DOI(`10.48550/...`)로 Crossref에 등록되어 있지 않아 **arXiv API로 검증 경로를 분기**해야 했다. → preprint는 별도 검증 경로가 필요하다는 것이 설계 요구사항으로 확인됨.
- 1건은 Crossref title에 `<scp>` 마크업이 포함되어 단순 문자열 비교가 **거짓 불일치**를 만들었다. → 비교 전 태그 제거·유니코드 정규화가 필수.

**(c) Citation network**

- [Gusenbauer2024]는 forward citation 검색에서 Google Scholar, ResearchGate, Semantic Scholar, Lens를 선도적 선택지로, backward citation 검색의 정확도에서는 Scopus보다 Web of Science Core Collection을 권장한다. → 구독이 없는 조건에서는 OpenAlex + Semantic Scholar 조합이 현실적 차선이며, **BWC 정확도가 상대적 약점**임을 한계로 기록한다.
- [Lo2020]의 S2ORC는 수백 개 출판사·아카이브의 논문을 통합하고, 8.1M open access 논문의 본문에 인라인 인용을 자동 검출해 해당 논문 객체에 연결한다 — 인용 문맥까지 필요할 때의 보강 경로.

**(d) Full text** — claim 추출은 반드시 원문에서 한다(§6.4 Gate 2). abstract 기반 추출을 금지하는 이유는 §6.2의 실측에서 설명한다.

**(e) Retraction** — [Ortega2024]는 비선별적 데이터베이스(Dimensions, OpenAlex, Scilit, Lens)가 선별적 데이터베이스보다 철회 문헌을 더 많이 색인하며, OpenAlex·Scilit·WoS를 합치면 표본의 99%가 포괄된다고 보고한다. OpenAlex를 주 discovery로 쓰면 **철회 논문이 결과에 포함될 가능성이 상대적으로 높다**는 뜻이므로, 최종 포함 목록에 대해 철회 여부 확인을 의무화한다.

### 2.4 보강 경로(supplementary route)의 조건

구독 DB와 arXiv는 **모두** 보강 경로로 분류한다. 보강 경로를 사용할 경우 [Rethlefsen2021]의 PRISMA-S 16개 보고 항목 수준으로 **검색일, 플랫폼, 전체 query 문자열, 결과 수, export 파일명**을 기록해야 하며, 기록이 없으면 그 결과는 사용하지 않는다.

| 보강 source | 사용이 정당화되는 조건 | 비고 |
|---|---|---|
| WoS / Scopus | known-item diagnostic(§4.3)에서 OpenAlex 미검출 seed가 발견될 때 | 프로그램 접근 불가 — 수동 export만 가능. [Baas2020]은 Scopus의 독립 선정위원회 기반 품질관리와 저자·기관 프로파일링을, [Birkle2020]은 WoS의 분석용 데이터셋 제공을 각각 기술한다 |
| SciFinder / Reaxys | 특정 전구체·합성 경로를 화학 구조/반응 기준으로 찾아야 할 때 | [Baykoucheva2011]은 SciFinder 내 CAPLUS와 MEDLINE의 문서 중복이 20–24%에 불과하다고 보고한다 → 화학 DB는 대체재가 아니라 **보완재** |
| arXiv | cond-mat 계열 계산(DFT) 연구의 preprint 확인 | 무기산화물·촉매 실험 문헌의 preprint 비중은 낮다고 판단 — **라벨 ③신규(근거 없음, 수집 중 검증 필요)** |
| Google Scholar | 개별 seed paper의 존재 확인, 인용 추적 보조 | 주 discovery 엔진 금지 — [Gusenbauer2019] |

### 2.5 환경 제약 (기록)

본 분석 환경에서는 **Web of Science, Scopus, Google Scholar에 프로그램적으로 접근할 수 없다**(API 미제공 또는 구독 필요). 따라서 자동 파이프라인은 OpenAlex + Crossref + (필요 시) arXiv·Semantic Scholar로 구성되고, 구독 DB는 사람이 수행하는 수동 보강 단계로만 들어온다. 이는 재현성 측면에서는 오히려 명확하다 — **스크립트 경로는 100% 재현 가능하고, 수동 경로는 PRISMA-S 기록으로 추적 가능**하다.

**재검토 trigger**: 기관 구독이 확인되면 WoS/Scopus를 discovery 보강으로 1회 실행하고, OpenAlex 단독 대비 **신규 적격 논문 수**를 측정해 §2.2 매트릭스를 갱신한다.

---

## 3. 결정 D3 — Query 개발과 검증

### 3.1 Research question → search concept 분해

**PICO는 쓰지 않는다.** PICO(Population–Intervention–Comparison–Outcome)는 임상 개입 연구의 구조를 전제하는데, 본 연구에는 population도 comparison군도 없다. 대신 재료 문헌의 구조에 맞는 3-facet 분해를 사용한다. 이는 [Booth2008]이 "building blocks"로 부른 고전적 facet 조합 방식에 해당한다.

| Facet | 내용 | 예시 term (seed에서 수확 예정) |
|---|---|---|
| **A. Material** | 대상 물질과 그 표기 변이 | gamma-alumina, γ-Al2O3, transition alumina, Al₂O₃ support |
| **B. Treatment / synthesis** | 합성 및 후처리 조건 | calcination, dehydroxylation, thermal treatment, reduction, sol-gel, precursor |
| **C. Property / probe** | 표면·결함 성질과 그 관측 수단 | penta-coordinated Al, Al(V), oxygen vacancy, defect site, Lewis acid site, ²⁷Al MAS NMR, H₂-TPR, EPR, DFT |

검색식의 기본형은 `A AND B AND C`이며, recall을 올려야 할 때 C를 제거한 `A AND B`로 확장한다.

**라벨: ②수정** — facet 조합(building blocks)은 ①확립이나, facet 정의는 본 분야용으로 새로 세운 것.

### 3.2 통제어휘(controlled vocabulary)의 부재가 의미하는 것

biomedical 검색의 핵심 자산인 MeSH 같은 통제어휘가 **OpenAlex와 Crossref에는 없다.** 이것이 왜 중대한 제약인지는 다음 근거가 보여준다.

- [Markey1980]은 free text 검색식이 recall이 높고 controlled vocabulary 검색식이 precision이 높으며, 검색 목표(고recall이냐 고precision이냐)가 둘 중 선택을 결정해야 한다고 보고했다. 또한 통제어휘 디스크립터로는 표현할 수 없고 free text로만 입력 가능한 6개 범주의 검색 개념이 존재함을 발견했다.
- [Gross2005]는 subject heading이 없었다면 키워드 검색으로 성공적으로 검색된 레코드의 1/3 이상이 손실되었을 것이며, 개별 사례에서는 80%, 90%, 심지어 100%가 검색되지 않았을 것이라고 보고한다.

[Gross2005]의 상황은 "통제어휘가 있는 DB에서 그것을 빼면 얼마나 잃는가"이고, 우리 상황은 **처음부터 없는 것**이다. 전이의 방향이 다르므로 수치를 그대로 가져올 수는 없지만, 함의는 명확하다: **통제어휘가 없는 환경에서 free-text query만으로 높은 recall을 기대할 수 없으며, 용어 변이(term variation)를 사람이 명시적으로 수확해 넣어야 한다.** 재료 분야의 표기 변이(γ-Al₂O₃ / gamma-alumina / g-Al2O3 / transition alumina)와 단위·조건 표현의 다양성을 고려하면 이 부담은 biomedical보다 크다.

**→ 결론: query 단독으로는 부족하며 citation chasing이 필수 보완 수단이다(§4).** 이는 선택이 아니라 통제어휘 부재에서 오는 구조적 귀결이다. **라벨: ②수정**

### 3.3 Recall / precision trade-off의 실제 크기

[Terwee2009]는 측정 속성 연구를 찾기 위한 PubMed 검색 필터를 개발하면서, gold standard 레코드와 100편의 systematic review에서 검색어를 선정·조합해 평가했다. 그 결과 **민감 필터는 116편 중 113편을 검색해 sensitivity 97.4%를 달성했으나 precision은 4.4%에 그쳤다.**

이 수치는 본 연구의 작업량 설계에 직접 쓰인다. 높은 recall을 목표로 하면 **적격 1편당 20편 이상을 screening해야 한다**는 뜻이다. 100편 이상의 적격 논문을 목표로 한다면 title/abstract screening 대상은 수천 건 규모가 될 수 있고, 이것이 §6의 LLM 보조 screening을 정당화하는 실질적 이유다.

**라벨: ①확립** (trade-off의 존재와 크기) / **②수정** (수치 자체는 biomedical 필터의 값이므로 본 분야에서 재측정 필요).

### 3.4 반복적 query 개선 루프의 정식 명칭

사용자가 서술한 루프 — `seed 선정 → query 작성 → seed 검출 확인 → 미검출 분석 → term 추가 → 재검색` — 에 대응하는 **단일한 표준 용어는 존재하지 않는다.** 조사 결과 이 루프는 세 가지 기존 기법이 합쳐진 형태다.

| 구성 요소 | 기존 명칭 | 근거 |
|---|---|---|
| seed가 검색되는지 확인 | **known-item testing** / gold-standard 기반 필터 개발 | [Terwee2009]가 gold standard 레코드에서 검색어를 선정하고 그에 대한 sensitivity를 측정한 절차가 이에 해당 |
| 찾은 문헌에서 새 term을 수확해 query 확장 | **pearl growing** (citation pearl growing) | [Booth2008]이 'Building Blocks', 'Berry Picking', 'Successive Fractions'와 함께 문헌검색 toolbox의 전술로 정리 |
| 전체를 반복 | **iterative search strategy development** | [Levac2010]의 iterative 접근, [MacFarlane2022] |

⚠ **중요한 반증**: pearl growing은 항상 작동하지 않는다. [Papaioannou2009]는 사회과학 systematic review에서 **pearl growing을 중단**했는데, 지명된 pearl들이 여러 데이터베이스에 분산되어 어떤 단일 DB도 4편 넘게 색인하지 못했기 때문이다. 같은 연구에서 전통적 주제 검색은 포함된 41편 중 30편만 찾아냈고 나머지는 보조 기법으로 확보되었다. 재료·촉매 문헌 역시 저널이 분산되어 있으므로 **pearl growing이 실패할 가능성을 미리 인정하고, 실패 시 citation chasing으로 대체하는 경로를 설계에 포함한다.**

또한 [MacFarlane2022]는 검색 전략 구축 방법이 복잡하고 시간·자원 소모적이며 오류가 발생하기 쉽다고 지적하고, 신뢰·설명가능성·재현성을 위한 설계 원칙의 필요성을 주장한다.

### 3.5 Query의 품질 검증 — PRESS

1인 연구에서도 query를 검증 없이 쓰지 않는다. [McGowan2016]의 PRESS 2015 guideline은 원래 7개 요소 중 6개를 유지했으며, 여기에는 연구질문의 번역, Boolean·근접 연산자, subject heading, text-word 검색어가 포함된다. 같은 연구는 구조화된 PRESS가 검색 오류를 식별하고 검색어 선택을 개선할 수 있음을 시사한다고 보고한다. [Sampson2009]는 이 peer review 절차의 근거 기반 guideline을 제시한다.

> **채택**: 최종 query 확정 전 PRESS 6요소 체크리스트를 **자가 적용**하고, 가능하면 지도교수 또는 동료 1인의 검토를 받는다. 체크 결과를 기록으로 남긴다.
> **라벨: ②수정** — PRESS는 전문 사서의 peer review를 전제하지만, 본 연구에는 사서가 없으므로 자가 적용 + 1인 검토로 축소한다. 이 축소가 PRESS의 효과를 유지하는지에 대한 근거는 **없다**.

### 3.6 검색 보고

[Rethlefsen2021]의 PRISMA-S는 16개 보고 항목으로 구성되며, 기존 검색 보고 guidance가 다양하고 상세함이 부족했던 문제를 겨냥한다. [Kugley2017]은 Campbell Collaboration의 정보검색 guide로 검색 전략 템플릿과 정보검색 활동 체크리스트를 부록으로 제공한다.

> **채택**: 모든 검색(자동·수동)을 PRISMA-S 16항목 수준으로 기록. 최소 필수 필드는 `source, 플랫폼, 검색일, 전체 query 문자열, 필터, 결과 수`.
> **라벨: ①확립**

---

## 4. 결정 D4 — Search completeness 평가와 중단 기준

### 4.1 대전제: completeness는 증명할 수 없다

[Blair1985]는 실무 full-text 검색 시스템 평가에서 **해당 시스템이 특정 검색에 대해 관련 문서의 20% 미만을 검색하고 있음**을 보였다. 검색자가 스스로 충분히 찾았다고 믿는 상태와 실제 recall 사이의 간극을 보여준 고전적 결과다.

방법론 문헌 자체도 완전성 판단의 근거가 빈약함을 인정한다. [Booth2016]은 질적 연구 검색에서 **현재의 정보검색 실무를 뒷받침하는 경험적 근거가 빈약하다**고 평가하며, [Sutton2019]는 '전통적' systematic review를 벗어나면 검색 요구사항에 대한 정의 자체가 불확실하다고 본다.

> **따라서 본 연구는 "문헌을 모두 찾았다"는 주장을 하지 않는다.** completeness를 보장한다는 서술을 보고서에서 금지하고, 대신 **무엇을 어떻게 찾았고 어디서 멈췄는지**를 기록한다. **라벨: ①확립**

### 4.2 Known-item testing — 정량 threshold 없이 진단 도구로 사용

사용자 지시에 따라, 그리고 §4.1의 근거에 따라, **임의의 recall threshold(예: "seed의 90%를 검색해야 한다")를 설정하지 않는다.** 방법론 문헌에서 보편적으로 정당화된 threshold를 찾지 못했기 때문이다. [Terwee2009]의 97.4%는 특정 주제·특정 DB에서 개발된 필터의 성능값이지 일반 기준이 아니다.

> **채택: diagnostic criterion**
> seed paper 전체에 대해 개별적으로 "검색되었는가 / 안 되었다면 왜인가"를 분석하고 그 결과를 표로 남긴다. 미검출 원인은 다음으로 분류한다.
>
> | 미검출 원인 코드 | 의미 | 대응 |
> |---|---|---|
> | `TERM` | query에 없는 용어·표기 변이 사용 | term 추가 후 재검색 |
> | `FIELD` | 해당 용어가 title/abstract에 없고 본문에만 존재 | full-text 검색 또는 citation chasing에 의존 |
> | `COVERAGE` | source에 레코드 자체가 없음 | 보강 경로(§2.4) 검토 |
> | `LOGIC` | Boolean 구조 오류 (AND/OR/괄호) | query 수정 — PRESS 재적용 |
> | `TYPE` | 문서 유형 필터에 의해 배제 (book chapter, 학위논문 등) | 필터 조정 |
>
> 각 미검출 seed에 대해 **원인 코드와 조치를 1행씩 기록**하며, 원인이 `TERM`/`LOGIC`인 경우에는 query를 수정하고 전체 루프를 다시 돈다.

**라벨: ②수정** — known-item testing 자체는 ①확립이나, "threshold 없는 진단적 사용"으로 운용 형태를 바꾼 것.

### 4.3 Seed set의 구성 원칙

known-item testing의 타당성은 seed set의 질에 전적으로 의존한다. seed가 편향되면 진단도 편향된다.

> **채택**: seed set은 (i) 서로 다른 연구그룹, (ii) 서로 다른 연도대(최소 2000년대·2010년대·2020년대), (iii) 서로 다른 방법론(실험 분광학 / DFT 계산 / 촉매 반응)을 포함하도록 **의도적으로 다양화**한다. seed 선정 근거를 1편당 1행으로 기록한다.
> **라벨: ③신규** — seed 구성 기준에 대한 직접 근거 문헌은 찾지 못함.

### 4.4 Citation chasing — 선택이 아니라 필수

§3.2에서 통제어휘 부재가 query 기반 recall을 구조적으로 제한한다고 결론지었다. citation chasing은 이 결손을 메우는 주된 수단이며, 근거가 비교적 강한 영역이다.

- [Hirt2023]은 citation tracking을 다룬 연구들을 검토해 **96%에서 증거 검색에 대한 부가가치가 확인**되었다고 보고한다. 동시에 citation tracking 용어가 이질적이고 모호하다고 지적한다.
- [Hirt2024]의 **TARCiS statement는 citation searching의 수행·보고에 대한 10개 권고**를 각각의 근거와 함께 제시한다.
- [Haddaway2022]는 citation chasing이 **리뷰어가 쓴 용어를 사용하지 않아 다른 검색 방법으로는 검색되지 않았을 연구**를 찾아낸다고 설명한다 — §3.2의 term-variation 문제에 정확히 대응하는 기능이다.
- [Wohlin2014]는 systematic literature study를 위한 snowballing guideline을 제시하고, [Wohlin2022]는 데이터베이스 검색과 snowballing을 결합한 hybrid 전략이 **데이터베이스 검색 단독 대비 30% 더 많은 primary study를 식별**했다고 보고한다.
- 실행 비대칭에 대한 경고: [Briscoe2019]는 Cochrane 리뷰 215편 중 **backward citation 검색은 172편이 보고했으나 forward citation 검색은 18편에 그쳤다**고 보고한다. 즉 FWC는 체계적으로 과소 사용된다.
- [Cooper2017]은 저자 연락, citation chasing, handsearching, 임상시험 등록부 검색, 웹 검색 등 5개 보조 검색 방법을 검토했으며, 어떤 전략을 언제 쓸지 합리적으로 선택하기 위해서는 추가 연구가 필요하다고 결론짓는다.

> **채택**: 포함이 확정된 모든 논문에 대해 **backward(참고문헌) + forward(피인용) 양방향 citation chasing을 1 round 실행**한다. 구현은 OpenAlex `referenced_works` / `cited_by`. 보고는 TARCiS 권고를 따른다.
> **라벨: ①확립**

### 4.5 중단 기준 — pragmatic stopping criterion

> **정의 (중요)**: 본 연구의 중단 기준은 **전체 문헌의 completeness를 보장하지 않는다.** 이는 추가 iterative search 및 citation chasing의 **marginal yield(한계 수확)**에 근거한 **실용적 중단 기준**일 뿐이다.

> **채택되는 중단 조건** — 아래를 **모두** 만족할 때 검색을 종료한다.
> 1. 모든 seed paper가 검색되었거나, 미검출 seed 각각에 대해 §4.2의 원인 코드와 조치가 기록되었다.
> 2. 직전 1 round의 citation chasing에서 새로 추가된 **적격** 논문 수가 그 round 검토량 대비 뚜렷이 감소했다 (수치 기준은 수집 착수 후 실제 분포를 보고 사전 고정하되, 사후 조정하지 않는다).
> 3. 마지막 query 수정이 새로운 적격 논문을 만들어내지 못했다.
>
> 종료 시 **"왜 여기서 멈췄는가"를 marginal yield 수치와 함께 1문단으로 기록**한다. 이 기록이 없으면 종료로 인정하지 않는다.

**라벨: ③신규** — [Cooper2017]과 [Booth2016]이 보여주듯 "언제 멈출지"에 대한 합의된 근거 기준은 존재하지 않는다. 위 조건은 본 프로젝트가 스스로 정한 실용적 규칙이며, 근거 문헌에 의해 뒷받침되는 것은 **"합의된 기준이 없으므로 실용적 규칙을 투명하게 선언해야 한다"는 메타 수준의 주장**뿐이다.

### 4.6 Grey literature

[Garousi2018]은 소프트웨어공학에서 grey literature를 포함하는 multivocal literature review의 guideline을 제시한다. 본 연구에서는 **학위논문·기술보고서·특허를 기본 제외**하되, 제외를 기록하고 특정 합성 조건이 특허에만 기술된 정황이 발견되면 그 하위 주제에 한해 보강한다. **라벨: ②수정**

---

## 5. 결정 D5 — Screening

### 5.1 1인 연구라는 구조적 제약을 숫자로 인정하기

[Gartlehner2020]은 crowd 기반 무작위 연구에서 **단일 검토자 abstract screening이 관련 연구의 13%를 놓쳤고(sensitivity 86.6%, 95% CI 80.6–91.2%), 이중 검토자는 3%를 놓쳤다(sensitivity 97.5%, 95% CI 95.1–98.8%)**고 보고한다.

본 연구는 1인 수행이므로 **구조적으로 ~13% 누락 수준에서 출발한다.** 이것은 숨길 것이 아니라 보고서 limitation에 명시하고, 완화 수단을 설계해야 할 사항이다.

> **채택되는 완화 수단 (3중)**
> 1. **LLM을 제2 검토자로** 사용 — 사람과 LLM의 판정이 불일치하는 레코드만 재검토 (§6).
> 2. **무작위 재검토** — 사람이 제외(exclude)한 레코드에서 무작위 표본을 추출해 재판정하고, 뒤집힌 비율을 보고한다.
> 3. **Citation chasing**(§4.4)이 screening 누락을 부분적으로 보상한다.
>
> **라벨: ①확립**(문제 인식) + **③신규**(LLM을 제2 검토자로 쓰는 구성 — §6.3에서 근거와 한계를 따로 평가).

### 5.2 Inclusion / exclusion criteria

> **채택**: 기준은 **검색 착수 전에 사전 정의**하되, seed set 20편에 대한 **파일럿 적용 후 1회 개정**을 허용한다. 개정 이력은 날짜와 사유를 남긴다. 파일럿 이후에는 기준을 변경하지 않는다. 변경이 불가피하면 변경 전 판정 전체를 재실행한다.

[Levac2010]이 scoping study의 study selection을 반복적(iterative) 팀 작업으로 규정한 것과 정합적이다. **라벨: ②수정** (팀 → 1인).

초안 기준 (수집 착수 전 확정 예정):

| 구분 | 기준 |
|---|---|
| 포함 | γ-Al₂O₃(또는 transition alumina 중 γ상 명시)를 대상으로 하고, 합성 또는 후처리 조건이 기술되어 있으며, 표면/결함 구조 또는 산소 거동/환원 거동에 대한 실험적 또는 계산적 관측을 보고 |
| 제외 | γ상이 특정되지 않은 일반 alumina, Al₂O₃가 단순 지지체로만 등장하고 지지체 자체의 표면·결함을 다루지 않는 연구, 조건 기술이 없는 연구, 원문 입수 불가 |
| 보류(borderline) | §5.4 |

### 5.3 중복 제거 (deduplication)

자동 중복 제거의 성능 차이는 크고 실측되어 있다.

- [Rathbone2015]: SRA-DM의 sensitivity 84%·specificity 100%로 EndNote(sensitivity 51%, specificity 99.83%)보다 우수했고, 전체적으로 EndNote 자동 중복제거 대비 **검출 중복 레코드가 42.86% 증가**했다.
- [McKeown2021]: Ovid·EndNote·Mendeley·Zotero·Covidence·Rayyan의 기본 설정을 수동 대조군과 비교해, **Ovid와 Covidence가 specificity가 가장 높고 Rayyan이 sensitivity가 가장 높았다**고 보고한다.
- [Borissov2022]: Deduklick은 평균 recall 99.51%, precision 100.00%, F1 99.75%를 달성해 수동 중복제거(recall 88.65%, F1 91.98%)를 상회했다.

여기서 읽어야 할 핵심은 "어떤 도구가 1등인가"가 아니라 **도구마다 sensitivity/specificity 균형이 다르고, 수동 중복제거조차 recall 88.65%에 그쳤다**는 점이다.

> **채택**: ① DOI 정규화 후 완전일치로 1차 제거 → ② 제목 정규화(소문자·공백·구두점·유니코드 제거) + 연도 + 제1저자 성으로 2차 제거 → ③ 유사도 경계 구간의 레코드는 **자동 삭제하지 않고 사람이 확인**. 삭제된 레코드 수를 단계별로 기록(PRISMA flow에 필요).
> **라벨: ②수정** — 전용 도구 대신 API 메타데이터 기반 규칙으로 구현하되, 경계 구간 수동 확인으로 보완.

### 5.4 Borderline 논문 처리

[Wohlin2022]는 snowballing 기반 문헌연구에서 개별 판단의 여지를 수용하고 관련 연구를 배제할 위험을 최소화하기 위해 **'wild cards'와 'borderline articles'라는 두 개념을 도입**했다.

> **채택**: 이분법(include/exclude)이 아니라 **3분법(include / borderline / exclude)**을 사용한다. borderline은 즉시 버리지 않고 별도 목록으로 보존하며, full-text 단계에서 재판정한다. 최종 보고서에 borderline 건수와 최종 처리 결과를 보고한다.
> **라벨: ①확립** (단, 근거는 소프트웨어공학 분야)

### 5.5 2단계 screening과 도구

> **채택**: title/abstract screening → full-text screening의 2단계. 각 단계의 제외 사유를 코드로 기록(full-text 단계는 PRISMA 요구사항).
> 도구: [Ouzzani2016]의 Rayyan은 설문 응답자 기준 **평균 40%의 시간 절감**(34%는 50% 이상 절감)을 보고한다. 다만 본 파이프라인은 API 기반 자체 스크립트를 쓰므로 Rayyan은 선택적 보조로만 둔다.
> **라벨: ①확립**

---

## 6. 결정 D6 — AI/LLM 허용 범위와 2단계 Validation Gate

### 6.1 왜 서지정보 생성은 전면 금지인가

이 금지는 취향이 아니라 측정된 실패율에 근거한다.

- [Walters2023]: ChatGPT가 생성한 인용 중 **GPT-3.5는 55%, GPT-4는 18%가 날조(fabricated)**였다. 더 중요한 점은 **날조가 아닌 실재 인용 중에서도 GPT-3.5는 43%, GPT-4는 24%가 실질적 인용 오류를 포함**했다는 것이다.
- [Bhattacharyya2023]: ChatGPT가 생성한 의학 콘텐츠의 참고문헌 중 **47%가 날조, 46%는 실재하나 부정확, 단 7%만이 실재하고 정확**했다.
- [Chelli2024]: systematic review 맥락에서 ChatGPT와 Bard의 hallucination 비율과 참고문헌 정확도를 직접 비교 평가했다.
- [Adel2025]: ChatGPT 기반 문헌 종합에서 **hallucination 비율이 91%에 달했다**고 보고하며 면밀한 감독의 필요성을 강조한다.

[Walters2023]의 두 번째 수치가 결정적이다. **"그 논문이 실재하는가"만 확인하는 것으로는 부족하다** — 실재하는 논문에 대해서도 인용 내용이 틀릴 수 있다. 이것이 Gate를 1단계가 아니라 **2단계**로 나누는 직접적 이유다.

> **원칙 (架構)**: LLM은 **academic API가 반환한 실제 레코드와 실제 full text에 대해서만 판단(judge)**한다. 서지정보, 수치, 실험 조건, mechanism을 **생성(generate)하지 않는다.**

이 아키텍처의 타당성은 [Han2024]가 지지한다 — **RAG가 LLM의 생성 능력과 실시간 정보검색의 정확성을 결합함으로써 hallucination과 부정확성의 한계를 완화**한다고 설명하며, 문헌검색·스크리닝·데이터추출·정보종합의 4단계를 포괄하는 틀을 제안한다. 다만 RAG는 완화이지 제거가 아니며, 아래 Gate가 여전히 필요하다. **라벨: ①확립**(위험의 존재) + **③신규**(judge-only 아키텍처의 명문화)

### 6.2 이 세션에서 관측된 실패율 (observed)

본 문서를 작성하면서 동일한 아키텍처를 실제로 적용했고, 다음을 관측했다.

| 관측 | 값 | 함의 |
|---|---|---|
| 선정 레코드의 독립 검증 | 71편 중 70편 Crossref 확인, 1편은 arXiv DOI여서 arXiv API로 분기 검증 | 검증 source는 단일화할 수 없음 — preprint 경로 필요 |
| Crossref title 마크업 | 1건에서 `<scp>` 태그가 거짓 불일치 유발 | 비교 전 태그 제거·정규화 필수 |
| LLM이 추출한 findings의 인용문 검증 | 131건 중 **8건(6.1%)이 abstract에 존재하지 않는 문구**여서 자동 기각 | **abstract 원문을 함께 제공했음에도** 6%가 비(非)축자 인용 → Gate 2의 필요성이 직접 확인됨 |

마지막 행이 중요하다. LLM에게 원문을 주고 "축자 인용만 하라"고 지시한 조건에서조차 6%가 실패했다. **따라서 claim 추출에 대한 자동 축자 대조는 선택이 아니라 필수다.**

### 6.3 단계별 AI/LLM 허용 범위

| 단계 | AI 허용 | 역할 | 알려진 error / risk | 요구되는 validation |
|---|---|---|---|---|
| Query 용어 제안 | ✅ 보조 | 동의어·표기 변이 후보 생성 | 비존재 용어 제안, facet 누락 | 사람이 전수 승인 + PRESS 체크 + known-item 진단으로 사후 검증 |
| **논문 발견(discovery)** | ❌ **금지** | — | 날조 인용 ([Walters2023], [Bhattacharyya2023], [Adel2025]) | 해당 없음 — 레코드는 **오직 API에서만** 획득 |
| 서지 메타데이터 생성 | ❌ **금지** | — | 위와 동일 | 해당 없음 — Gate 1이 API 대조로 처리 |
| TiAb screening | ✅ 보조 (제2 검토자) | 사람 판정과 병행 | sensitivity 변동 폭이 큼 | 불일치 전수 사람 재판정 + 제외 표본 재검토 |
| Full-text screening | ✅ 보조 | 사람 판정 보조 | 동일 | 사람이 최종 판정 |
| 구조화 데이터 추출 | ✅ 보조 | 조건·수치의 후보 추출 | 사실 부정확 | **Gate 2** (축자 대조 + 위치 기록) |
| 요약 | ✅ 허용 | 이미 검증된 내용의 재서술 | 새로운 사실 삽입 | 요약에 새 수치·주장이 없는지 대조 |
| 인용 검증 | ❌ **금지** | — | LLM은 검증 주체가 될 수 없음 | Gate 1이 API로 수행 |
| 과학적 결론 도출 | ❌ **금지** | — | 저자 해석과 AI 추론의 혼동 | 해당 없음 — §6.4의 3분 라벨로 분리 |

**screening 보조를 허용하는 근거와 그 한계**

성능 보고는 **일관되지 않으며, 이 불일치 자체가 설계 제약이다.**

- [Guo2023]: 합의 기반 인간 판정 대비 **κ = 0.96**. 그러나 같은 연구에서 **포함 논문에 대한 sensitivity는 0.76**, 제외 논문에 대해서는 0.91로 **비대칭**이었다 — 즉 놓치는 쪽이 포함 논문이다.
- [Oami2024]: 통합 sensitivity 0.75(95% CI 0.43–0.92), specificity 0.99에서 출발해 프롬프트 최적화로 **sensitivity 0.91까지 개선**.
- [Dennstadt2024]: 모델·데이터셋에 따라 **sensitivity 81.93–100%, specificity 4.54–75.19%**로 폭이 매우 크며, **지시 프롬프트의 사소한 수정이나 Likert 척도 범위 변경만으로도 성능이 크게 달라졌다**.
- [Khraisha2024]: 우연 일치와 데이터셋 불균형을 보정하자 **모든 단계에서 성능 점수가 하락**했다(스크리닝은 없음~보통). 다만 고신뢰 프롬프트로 full-text를 스크리닝할 때는 "human-like" 수준에 도달했다고 보고한다.
- 작업량 절감 쪽 근거: [Hamel2020]은 95% recall 기준에서 **스크리닝 부담 중앙값 47.1% 감소**와 **중앙값 29.8시간 절감**을 보고하고, [Chai2021]은 11개 리뷰에서 **60–96% 작업량 절감**을 보고한다.
- 경고: [Przybyla2018]은 ML 보조 스크리닝에서 **사용자의 자만(complacency)과 중단 기준의 필요성**을 핵심 쟁점으로 지적한다. [OMara-Eves2015]는 자동 배제 용도는 아직 완전히 입증되지 않았다고 본다.

> **채택**: LLM은 **recall 우선 프롬프트**로 제2 검토자 역할만 수행한다. LLM 단독 제외를 금지하고, 사람–LLM 불일치는 전수 사람이 재판정한다. 사용 전 **seed set을 포함한 소규모 라벨링 세트에서 sensitivity를 직접 측정**하고 그 값을 보고서에 기록한다([Dennstadt2024]가 보여주듯 성능은 프롬프트·데이터셋 의존적이므로 타 연구의 수치를 가져다 쓸 수 없다).
> **라벨: ②수정**

**추출 보조를 허용하는 근거 — 이 영역은 재료 분야 직접 근거가 있다**

- [Polak2024]의 ChatExtract는 **최고 수준 대화형 LLM에서 재료 데이터 추출의 precision과 recall이 모두 90%에 근접**했고, **후속 질문(follow-up questions)이 LLM의 사실 부정확 문제를 상당 부분 극복**했다고 보고한다.
- [Dagdelen2024]는 사전학습 LLM을 미세조정해 과학 텍스트에서 복잡한 지식 레코드를 추출할 수 있으며 **출력을 JSON 객체 목록 같은 구조화 형식으로 반환**할 수 있음을 보인다.

이 둘은 본 연구와 같은 재료 도메인에서 나온 근거이므로 전이 부담이 가장 적다. 다만 두 연구 모두 **추출의 정확도를 별도로 측정**했다는 점이 중요하다 — 측정 없는 추출은 근거가 없다. **라벨: ②수정**

### 6.4 Gate 1 — Bibliographic verification

> **목적**: 레코드가 실재하고 서지 필드가 정확함을 **API 레코드 대조로** 보장.
> **입력**: discovery에서 얻은 레코드 (OpenAlex)
> **검증 source**: Crossref API (주), arXiv API (preprint DOI), publisher 레코드 (예외 처리)

| 검사 항목 | 통과 조건 |
|---|---|
| DOI | 검증 source에서 해석(resolve)됨 |
| Title | 정규화 후 일치 (유니코드 정규화 + XML/HTML 태그 제거 + 영숫자 외 제거, 앞 60자 비교) |
| Authors | 제1저자 성이 양측에서 일치 |
| Year | 두 source 간 차이 ≤ 1년 (online-first/issue 연도 차이 허용) |
| Venue | 기록 (불일치는 경고로만 — 레코드 간 표기 관행 차이가 큼) |
| Retraction | 철회 표시 확인 ([Ortega2024]) |

**상태값과 처리**

| status | 의미 | 처리 |
|---|---|---|
| `verified` | 모든 검사 통과 | evidence synthesis 사용 **가능** |
| `verified_preprint` | preprint 경로(arXiv API)로 확인 | 사용 가능, preprint임을 본문에 명시 |
| `mismatch` | 필드 불일치 | **격리(quarantine)** — 사람이 원인 확인 후 수동 판정 |
| `unverified` | 검증 source에서 확인 불가 | **격리 — 보존하되 synthesis 투입 금지** |

> **불변 규칙 (invariant)**: `verified` 또는 `verified_preprint`가 아닌 레코드는 **어떤 경우에도 evidence synthesis에 투입되지 않는다.** 레코드는 삭제하지 않고 보존하며, 최종 보고서에 격리 건수와 사유를 보고한다.

**라벨: ①확립**(검증 필요성) + **③신규**(구체적 필드·임계·상태 기계)

### 6.5 Gate 2 — Scientific claim verification

Gate 1을 통과해도 "그 논문이 실제로 무엇을 보고했는가"는 보장되지 않는다([Walters2023]의 실재-인용 오류 43%/24%). Gate 2는 **추출된 각 claim이 원문의 실제 experiment / result / figure / table / 문장에 의해 뒷받침되는지**를 확인한다.

> **입력**: full text (PDF/XML) + LLM이 추출한 claim 후보
> **출력**: claim-level provenance 레코드

**claim-level provenance 스키마**

| 필드 | 내용 | 필수 |
|---|---|---|
| `paper_id` | DOI (Gate 1 통과 레코드만) | ✔ |
| `claim_id` | `{paper_id}#c{n}` | ✔ |
| `claim_text` | 추출된 주장 (1문장) | ✔ |
| `source_location` | page / section / figure / table 중 최소 1개 — 예: `p.4, Fig.3b`, `Table 2`, `§3.2` | ✔ |
| `supporting_span` | **원문에서 축자로 복사한 구절** | ✔ |
| `span_verified` | `supporting_span`이 원문에 축자 존재하는지 자동 대조 결과 (True/False) | ✔ |
| `method` | 측정·계산 방법 (예: `²⁷Al MAS NMR (16.4 T)`, `H₂-TPR`, `DFT PBE+U`) | ✔ |
| `conditions` | 실험 조건 (precursor, 소성 온도·시간·분위기, 전처리, 승온속도 등) | ✔ |
| `evidence` | 실제 측정값·관측값 (수치 + 단위) | 가능 시 |
| `interpretation_level` | `measured_fact` / `author_interpretation` / `ai_inference` 중 1 | ✔ |
| `verification_status` | `verified` / `unverified` / `conflicted` | ✔ |
| `extracted_by` | `human` / `llm:<model>` | ✔ |

**interpretation_level의 3분 라벨 — 본 프로젝트의 핵심 안전장치**

| 라벨 | 정의 | 예 |
|---|---|---|
| `measured_fact` | 논문이 **측정**한 값 | "소성 1073 K 후 ²⁷Al MAS NMR에서 Al(V) 신호가 관측됨" |
| `author_interpretation` | 저자가 측정으로부터 **해석**한 것 | "저자는 이를 표면 결함 생성으로 해석함" |
| `ai_inference` | LLM 또는 연구자가 **추론**한 것 | "이 결과는 oxygen lability 증가를 시사할 수 있음" |

> **불변 규칙**: `ai_inference`는 **증거로 집계되지 않는다.** 가설 생성에만 사용하며, 최종 보고서에서 반드시 구분 표기한다.
> 특히 **"Al(V) 또는 oxygen vacancy를 보고했다"는 사실로부터 "γ-Al₂O₃의 reducibility가 입증되었다"로 넘어가는 추론은 `ai_inference`이며, 그런 주장을 한 논문이 따로 있지 않는 한 증거로 쓰지 않는다.**

**통과 조건과 실패 처리**

| 조건 | 처리 |
|---|---|
| `span_verified = True` + `source_location` 기록 + `interpretation_level` 지정 | `verified` → synthesis 사용 가능 |
| `span_verified = False` | **자동 기각** 후 사람 재추출 (§6.2에서 6.1% 발생 관측) |
| 필수 필드 누락 | `unverified` → 격리 |
| 동일 조건에서 다른 논문과 상반된 값 | `conflicted` → 폐기하지 않고 **상충 증거로 별도 집계** (본 연구의 목적상 중요) |

**라벨: ③신규** — claim-level provenance에 대한 확립된 표준은 존재하지 않는다. 설계 착상은 [Polak2024]의 follow-up 검증과 [Dagdelen2024]의 구조화 JSON 출력, [Han2024]의 RAG 접지에서 가져왔으나, 위 스키마 자체는 본 프로젝트의 제안이다.

---

## 7. 통합 파이프라인 (Literature Search Methodology v1)

### 7.1 흐름도

```
 [S0] 연구질문 → search concept 분해 (A:material × B:treatment × C:property)
   │
 [S1] Seed set 구성 (그룹·연도·방법 다양화, 선정근거 기록)
   │
 [S2] Query v1 작성 (facet 조합, free-text 중심)
   │
 [S3] ◆ Known-item diagnostic ─── 미검출 seed 원인코드(TERM/FIELD/COVERAGE/LOGIC/TYPE)
   │         └── TERM·LOGIC → term 수확/구조 수정 후 [S2]로 복귀 (반복)
   │
 [S4] 본 검색 (OpenAlex API) ── 보강: WoS/Scopus/SciFinder/arXiv (PRISMA-S 기록 필수)
   │
 [S5] 중복 제거 → ▣ GATE 1 (Crossref/arXiv 서지검증) ── unverified → 격리
   │
 [S6] Citation chasing 1 round (BWC + FWC, OpenAlex) → 신규 레코드는 [S5]로
   │
 [S7] TiAb screening (사람 + LLM 제2검토자, 불일치 전수 재판정) → include/borderline/exclude
   │
 [S8] Full-text screening (borderline 재판정, 제외사유 코드 기록)
   │
 [S9] 구조화 추출 → ▣ GATE 2 (축자 대조 + claim-level provenance + 3분 라벨)
   │         └── span_verified=False → 자동 기각·재추출
   │
 [S10] Evidence synthesis / mapping (조건 × 표면성질 분류표, 상충 증거 별도 집계)
   │
 [S11] 보고 (PRISMA-ScR + PRISMA-S + 중단 사유 + 격리 통계 + limitation)
```

### 7.2 단계 명세

| 단계 | 목적 | Input | Method | Output | Validation | AI 허용 |
|---|---|---|---|---|---|---|
| S0 | 질문을 검색 가능한 개념으로 | 연구질문 | 3-facet 분해 (PICO 미사용) | facet 정의표 | 지도교수 검토 | 보조 |
| S1 | 진단 기준점 확보 | 사전 지식, 예비 검색 | 그룹·연도·방법 다양화 | seed 목록 + 선정근거 | Gate 1 적용 | ❌ |
| S2 | 검색식 작성 | facet 정의 | Boolean 조합, 표기 변이 수확 | query v_n | PRESS 6요소 자가 체크 | 보조(용어 제안) |
| S3 | query 진단 | query, seed | known-item testing (threshold 없음) | 미검출 원인표 | 원인코드 전수 기록 | ❌ |
| S4 | 레코드 수집 | 확정 query | OpenAlex API (+수동 보강) | 원 레코드 집합 | PRISMA-S 16항목 기록 | ❌ |
| S5 | 중복 제거·서지검증 | 원 레코드 | DOI→정규화 제목 2단계, Crossref 대조 | 검증 레코드 / 격리 목록 | **Gate 1** | ❌ |
| S6 | query 결손 보완 | 포함 확정 논문 | BWC+FWC (TARCiS 보고) | 추가 레코드 | marginal yield 기록 | ❌ |
| S7 | 1차 선별 | 검증 레코드 | 사람 + LLM 병행 | include/borderline/exclude | 불일치 전수 재판정, 제외 표본 재검토 | ✅ 제2검토자 |
| S8 | 2차 선별 | S7 통과분 + borderline | 원문 검토 | 최종 포함 집합 | 제외사유 코드 기록 | ✅ 보조 |
| S9 | 증거 추출 | full text | 구조화 추출 + 축자 대조 | claim provenance 테이블 | **Gate 2** | ✅ 보조 |
| S10 | 종합 | claim 테이블 | 조건×성질 매핑, 상충 집계 | 증거 지도, gap 목록 | `ai_inference` 분리 | 보조 |
| S11 | 보고 | 전 단계 기록 | PRISMA-ScR + PRISMA-S | 최종 보고서 | 인용-근거표 대조 | 보조 |

---

## 8. 추출 항목 (S9에서 채울 필드) — 재료 분야용 재정의

scoping/mapping review의 "data charting"을 본 분야용으로 구체화한 것이다. **라벨: ③신규** (항목 구성은 본 프로젝트 제안).

| 범주 | 필드 |
|---|---|
| 서지 | DOI, 연도, 저널, 연구그룹 |
| 물질 | 상(γ 확인 여부와 그 근거), 비표면적, 결정자 크기, 전구체(boehmite/gibbsite/alkoxide 등) |
| 합성 | 합성법, pH, 숙성 조건 |
| 열처리 | 소성 온도·시간·승온속도·분위기, 재수화/탈수화 이력 |
| 전처리 | 진공/환원/산화 처리 조건, 온도, 가스 |
| 표면 관측 | Al(IV)/Al(V)/Al(VI) 분율, OH 종류·밀도, 산점(Lewis/Brønsted) 종류·세기·밀도 |
| 산소/환원 거동 | 산소 공공 관련 관측, H₂ 소모량, 환원 온도, 산소 교환 결과 |
| 방법 | 사용한 characterization / 계산 방법과 조건 |
| 해석 | 저자 해석 (`author_interpretation`) |
| 품질 | γ상 확인 여부, 조건 기술 완전성, 재현 정보 유무 |

---

## 9. biomedical 방법론의 전이 가능성 — 결정에 영향을 준 범위에서만

| biomedical 전제 | 본 연구에서의 상태 | 처리 |
|---|---|---|
| PICO 질문 구조 | **깨짐** — population/comparison 없음 | 3-facet 분해로 대체 (§3.1) |
| MeSH 등 통제어휘 | **부재** — OpenAlex/Crossref에 없음 | free-text 중심 + term 수확 + citation chasing 의무화 (§3.2, §4.4) |
| study design 기반 evidence hierarchy | **비적용** — RCT 위계가 의미 없음 | 대신 **조건 기술의 완전성**과 **방법의 직접성**으로 증거 강도를 판단 (§8 품질 필드) — **라벨 ③신규** |
| risk-of-bias 도구 | **부재** — 재료 실험용 표준 도구 없음 | 도구를 발명하지 않는다. 품질 필드 기록에 그치고, 등급화하지 않음 |
| meta-analysis | **불가** — 공통 효과 척도 없음 | mapping + 조건-값 산점도 수준의 기술적 종합 |
| 이중 검토자 | **불가** — 1인 연구 | 13% 누락을 명시하고 3중 완화 (§5.1) |
| 사서(information specialist) 협업 | **부재** | PRESS 자가 적용으로 축소 — 효과 유지 근거 없음 (§3.5) |
| 효과 추정 중심 보고 | **부적합** | [Haddaway2018]이 환경 분야에서 PRISMA 적용의 12개 문제(메타분석 과도 강조 포함)를 지적한 것과 동일한 구조의 문제. 단 [Page2021b]는 PRISMA 2020이 통계적 종합을 포함하지 않는 리뷰에도 적용되도록 설계되었다고 밝히므로, 보고 틀 자체는 전이 가능 |

**전이 판단의 요약**: 전이되는 것은 **절차적 규율**(사전 기준 정의, 2단계 screening, 중복 제거, 검색 기록, 투명한 보고)이고, 전이되지 않는 것은 **인식론적 장치**(설계 위계, 비뚤림 평가, 효과 pooling)다. 전자는 분야와 무관하게 "무엇을 했는지 추적 가능한가"의 문제이므로 그대로 쓰고, 후자는 임상 연구의 통계적 구조에 의존하므로 버린다.

---

## 10. 한계와 재검토 조건

### 10.1 본 방법론의 한계 (보고서에 그대로 옮길 것)

1. **근거의 분야 편향** — 71편 중 재료/화학 직접 근거는 3편. 대부분의 결정이 인접 분야 전이에 의존한다(§0.4).
2. **1인 검토의 구조적 누락** — 단일 검토자 기준 ~13% 누락 [Gartlehner2020]. LLM 제2검토자와 재검토 표본으로 완화하나 제거되지 않는다.
3. **completeness 미보장** — 중단 기준은 marginal yield 기반의 실용 규칙일 뿐이다(§4.5). [Blair1985]가 보여주듯 검색자의 완전성 인식은 신뢰할 수 없다.
4. **BWC 정확도** — 구독 DB 없이 OpenAlex에 의존하므로 backward citation 정확도가 WoS Core Collection 대비 열위일 수 있다 [Gusenbauer2024].
5. **Gate 2는 검증된 표준이 아니다** — 본 프로젝트의 신규 제안이며, 그 자체의 오류율은 아직 측정되지 않았다.
6. **LLM 성능의 프롬프트 의존성** — [Dennstadt2024]가 보여주듯 사소한 프롬프트 변경으로 성능이 크게 변한다. 따라서 프롬프트를 버전 고정하고 변경 시 재측정해야 한다.
7. **화학 전용 DB 미포함** — SciFinder/Reaxys 없이는 특정 합성 경로 문헌이 누락될 수 있다 [Baykoucheva2011].

### 10.2 재검토 trigger (이 문서를 v2로 올려야 하는 조건)

| trigger | 조치 |
|---|---|
| 기관 WoS/Scopus 구독 확인 | discovery 보강 1회 실행 후 §2.2 매트릭스 갱신 |
| known-item diagnostic에서 `COVERAGE` 원인이 3건 이상 | source 구성 재검토 |
| LLM screening sensitivity 측정값이 0.9 미만 | LLM 제2검토자 역할 축소 또는 제외 |
| Gate 2 자동 기각률이 15% 초과 | 추출 프롬프트 재설계 또는 수동 추출로 전환 |
| 특정 하위 질문에 동질적 연구 10편 이상 축적 | 해당 하위 질문에 한해 정량 종합 추가 검토 (§1.3) |

---

## 11. Appendix

### A1. 검토했으나 채택하지 않은 기법

| 기법 | 미채택 사유 |
|---|---|
| Capture–recapture 기반 누락 추정 | 독립적인 2개 이상의 검색 경로가 통계적 독립성을 만족해야 하나, OpenAlex 중심 단일 경로 구성에서 그 가정이 성립하지 않음. 또한 §4.1의 근거에 따라 completeness를 수치로 주장하지 않기로 했으므로 목적 자체가 사라짐 |
| Inter-rater reliability (Cohen's κ 등) 정식 산출 | 검토자가 1인이므로 κ의 전제인 독립적 복수 평가자가 없음. 사람–LLM 일치도는 참고 지표로만 기록하고 신뢰도 주장으로 쓰지 않음 |
| PROSPERO 등 프로토콜 사전등록 | 재료과학 리뷰를 받는 등록처 관행이 확립되어 있지 않음. 대신 본 문서 자체를 **버전 고정된 사전 프로토콜**로 사용하고, 변경 시 버전을 올려 이력을 남김 |
| Risk-of-bias 등급화 | 재료 실험용 검증된 도구 부재 (§9). 도구를 임의 제작하면 근거 없는 등급이 생성되므로 품질 필드 기록에 그침 |
| Meta-analysis | 공통 효과 척도 부재 |

### A2. 근거표(`methodology_references.csv`) 사용법

| 컬럼 | 의미 |
|---|---|
| `ref_key` | 본문 인용 키 (예: `Gartlehner2020`) |
| `decision` / `decision_label` | 이 문헌이 뒷받침하는 결정 |
| `doi` | DOI (검증된 값) |
| `title` / `authors` / `year` / `venue` | **API에서 가져온 서지 필드** — 기억이나 추정으로 작성된 값 없음 |
| `verification_status` | `verified` (Crossref 대조 통과) / `verified_preprint_arxiv_api` |
| `source_discovery` / `source_verification` | 발견 source와 검증 source의 분리 기록 |
| `relevance_note` | 해당 문헌이 그 결정에 왜 관련되는지 |

### A3. 용어 대응

| 한국어 | English |
|---|---|
| 포괄성/완전성 | completeness |
| 재현율 / 정밀도 | recall (sensitivity) / precision (specificity) |
| 기지항목 검사 | known-item testing |
| 인용 추적 (후방/전방) | citation chasing (backward / forward) |
| 눈덩이 표집 | snowballing |
| 중복 제거 | deduplication |
| 한계 수확 | marginal yield |
| 증거 지도 | evidence map |
| 출처 이력 | provenance |

---

## 12. 근거 문헌 (verified)

아래 모든 레코드는 OpenAlex에서 발견하고 **Crossref API(또는 preprint의 경우 arXiv API)로 독립 검증**한 것이다. 검증되지 않은 레코드는 본문에서 인용하지 않았다.


### D1 review methodology / automation axis

- **[Arksey2005]** Arksey et al. (n=2) (2005). Scoping studies: towards a methodological framework. *International Journal of Social Research Methodology*. DOI: `10.1080/1364557032000119616` — verified (Crossref)
- **[Petersen2008]** Petersen et al. (n=4) (2008). Systematic Mapping Studies in Software Engineering. *Electronic workshops in computing*. DOI: `10.14236/ewic/ease2008.8` — verified (Crossref)
- **[Grant2009]** Grant et al. (n=2) (2009). A typology of reviews: an analysis of 14 review types and associated methodologies. *Health Information & Libraries Journal*. DOI: `10.1111/j.1471-1842.2009.00848.x` — verified (Crossref)
- **[Levac2010]** Levac et al. (n=3) (2010). Scoping studies: advancing the methodology. *Implementation Science*. DOI: `10.1186/1748-5908-5-69` — verified (Crossref)
- **[Haddaway2018]** Haddaway et al. (n=4) (2018). ROSES RepOrting standards for Systematic Evidence Syntheses: pro forma, flow-diagram and descriptive summary of the plan and conduct of environmental systematic reviews and systematic maps. *Environmental Evidence*. DOI: `10.1186/s13750-018-0121-7` — verified (Crossref)
- **[Munn2018]** Munn et al. (n=6) (2018). Systematic review or scoping review? Guidance for authors when choosing between a systematic or scoping review approach. *BMC Medical Research Methodology*. DOI: `10.1186/s12874-018-0611-x` — verified (Crossref)
- **[Tricco2018]** Tricco et al. (n=28) (2018). PRISMA Extension for Scoping Reviews (PRISMA-ScR): Checklist and Explanation. *Annals of Internal Medicine*. DOI: `10.7326/m18-0850` — verified (Crossref)
- **[Snyder2019]** Snyder (2019). Literature review as a research methodology: An overview and guidelines. *Journal of Business Research*. DOI: `10.1016/j.jbusres.2019.07.039` — verified (Crossref)
- **[Donthu2021]** Donthu et al. (n=5) (2021). How to conduct a bibliometric analysis: An overview and guidelines. *Journal of Business Research*. DOI: `10.1016/j.jbusres.2021.04.070` — verified (Crossref)
- **[Page2021]** Page et al. (n=26) (2021). The PRISMA 2020 statement: an updated guideline for reporting systematic reviews. *BMJ*. DOI: `10.1136/bmj.n71` — verified (Crossref)
- **[Page2021b]** Page et al. (n=26) (2021). PRISMA 2020 explanation and elaboration: updated guidance and exemplars for reporting systematic reviews. *BMJ*. DOI: `10.1136/bmj.n160` — verified (Crossref)
- **[Marzi2024]** Marzi et al. (n=4) (2024). Guidelines for Bibliometric‐Systematic Literature Reviews: 10 steps to combine analysis, synthesis and theory development. *International Journal of Management Reviews*. DOI: `10.1111/ijmr.12381` — verified (Crossref)

### D2 source roles

- **[Baykoucheva2011]** Baykoucheva (2011). Comparison of the Contributions of CAPLUS and MEDLINE to the Performance of SciFinder in Retrieving the Drug Literature. *Issues in Science and Technology Librarianship*. DOI: `10.29173/istl1522` — verified (Crossref)
- **[Bramer2017]** Bramer et al. (n=4) (2017). Optimal database combinations for literature searches in systematic reviews: a prospective exploratory study. *Systematic Reviews*. DOI: `10.1186/s13643-017-0644-y` — verified (Crossref)
- **[Gusenbauer2018]** Gusenbauer (2018). Google Scholar to overshadow them all? Comparing the sizes of 12 academic search engines and bibliographic databases. *Scientometrics*. DOI: `10.1007/s11192-018-2958-5` — verified (Crossref)
- **[Gusenbauer2019]** Gusenbauer et al. (n=2) (2019). Which academic search systems are suitable for systematic reviews or meta‐analyses? Evaluating retrieval qualities of Google Scholar, PubMed, and 26 other resources. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1378` — verified (Crossref)
- **[Harzing2019]** Harzing (2019). Two new kids on the block: How do Crossref and Dimensions compare with Google Scholar, Microsoft Academic, Scopus and the Web of Science?. *Scientometrics*. DOI: `10.1007/s11192-019-03114-y` — verified (Crossref)
- **[Baas2020]** Baas et al. (n=5) (2020). Scopus as a curated, high-quality bibliometric data source for academic research in quantitative science studies. *Quantitative Science Studies*. DOI: `10.1162/qss_a_00019` — verified (Crossref)
- **[Birkle2020]** Birkle et al. (n=4) (2020). Web of Science as a data source for research on scientific and scholarly activity. *Quantitative Science Studies*. DOI: `10.1162/qss_a_00018` — verified (Crossref)
- **[Lo2020]** Lo et al. (n=5) (2020). S2ORC: The Semantic Scholar Open Research Corpus. DOI: `10.18653/v1/2020.acl-main.447` — verified (Crossref)
- **[Martin-Martin2020]** Martín-Martín et al. (n=4) (2020). Google Scholar, Microsoft Academic, Scopus, Dimensions, Web of Science, and OpenCitations’ COCI: a multidisciplinary comparison of coverage via citations. *Scientometrics*. DOI: `10.1007/s11192-020-03690-4` — verified (Crossref)
- **[Visser2021]** Visser et al. (n=3) (2021). Large-scale comparison of bibliographic data sources: Scopus, Web of Science, Dimensions, Crossref, and Microsoft Academic. *Quantitative Science Studies*. DOI: `10.1162/qss_a_00112` — verified (Crossref)
- **[Delgado-Quiros2024]** Delgado-Quirós et al. (n=2) (2024). Completeness degree of publication metadata in eight free-access scholarly databases. *Quantitative Science Studies*. DOI: `10.1162/qss_a_00286` — verified (Crossref)
- **[Gusenbauer2024]** Gusenbauer (2024). Beyond Google Scholar, Scopus, and Web of Science: An evaluation of the backward and forward citation coverage of 59 databases' citation indices. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1729` — verified (Crossref)
- **[Ortega2024]** Ortega et al. (n=2) (2024). The indexation of retracted literature in seven principal scholarly databases: a coverage comparison of dimensions, OpenAlex, PubMed, Scilit, Scopus, The Lens and Web of Science. *Scientometrics*. DOI: `10.1007/s11192-024-05034-y` — verified (Crossref)
- **[Simard2024]** Marc-Andre Simard (2024). The open access coverage of OpenAlex, Scopus and Web of Science. *arXiv (Cornell University)*. DOI: `10.48550/arxiv.2404.01985` — verified (arXiv API, preprint)
- **[Cespedes2025]** Céspedes et al. (n=13) (2025). Evaluating the linguistic coverage of OpenAlex : An assessment of metadata accuracy and completeness. *Journal of the Association for Information Science and Technology*. DOI: `10.1002/asi.24979` — verified (Crossref)
- **[Culbert2025]** Culbert et al. (n=7) (2025). Reference coverage analysis of OpenAlex compared to Web of Science and Scopus. *Scientometrics*. DOI: `10.1007/s11192-025-05293-3` — verified (Crossref)

### D3 query development

- **[Markey1980]** Markey et al. (n=3) (1980). An analysis of controlled vocabulary and free text search statements in online searches. *Online Review*. DOI: `10.1108/eb024031` — verified (Crossref)
- **[Gross2005]** Gross et al. (n=2) (2005). What Have We Got to Lose? The Effect of Controlled Vocabulary on Keyword Searching Results. *College & Research Libraries*. DOI: `10.5860/crl.66.3.212` — verified (Crossref)
- **[Booth2008]** Booth (2008). Unpacking your literature search toolbox: on search styles and tactics. *Health Information & Libraries Journal*. DOI: `10.1111/j.1471-1842.2008.00825.x` — verified (Crossref)
- **[Papaioannou2009]** Papaioannou et al. (n=5) (2009). Literature searching for social science systematic reviews: consideration of a range of search techniques. *Health Information & Libraries Journal*. DOI: `10.1111/j.1471-1842.2009.00863.x` — verified (Crossref)
- **[Sampson2009]** Sampson et al. (n=6) (2009). An evidence-based practice guideline for the peer review of electronic search strategies. *Journal of Clinical Epidemiology*. DOI: `10.1016/j.jclinepi.2008.10.012` — verified (Crossref)
- **[Terwee2009]** Terwee et al. (n=4) (2009). Development of a methodological PubMed search filter for finding studies on measurement properties of measurement instruments. *Quality of Life Research*. DOI: `10.1007/s11136-009-9528-5` — verified (Crossref)
- **[McGowan2016]** McGowan et al. (n=6) (2016). PRESS Peer Review of Electronic Search Strategies: 2015 Guideline Statement. *Journal of Clinical Epidemiology*. DOI: `10.1016/j.jclinepi.2016.01.021` — verified (Crossref)
- **[Kugley2017]** Kugley et al. (n=7) (2017). Searching for studies: a guide to information retrieval for Campbell systematic reviews. *Campbell Systematic Reviews*. DOI: `10.4073/cmg.2016.1` — verified (Crossref)
- **[Rethlefsen2021]** Rethlefsen et al. (n=41) (2021). PRISMA-S: an extension to the PRISMA Statement for Reporting Literature Searches in Systematic Reviews. *Systematic Reviews*. DOI: `10.1186/s13643-020-01542-z` — verified (Crossref)
- **[MacFarlane2022]** MacFarlane et al. (n=3) (2022). Search strategy formulation for systematic reviews: Issues, challenges and opportunities. *Intelligent Systems with Applications*. DOI: `10.1016/j.iswa.2022.200091` — verified (Crossref)

### D4 completeness & stopping

- **[Blair1985]** Blair et al. (n=2) (1985). An evaluation of retrieval effectiveness for a full-text document-retrieval system. *Communications of the ACM*. DOI: `10.1145/3166.3197` — verified (Crossref)
- **[Wohlin2014]** Wohlin (2014). Guidelines for snowballing in systematic literature studies and a replication in software engineering. DOI: `10.1145/2601248.2601268` — verified (Crossref)
- **[Booth2016]** Booth (2016). Searching for qualitative research for inclusion in systematic reviews: a structured methodological review. *Systematic Reviews*. DOI: `10.1186/s13643-016-0249-x` — verified (Crossref)
- **[Cooper2017]** Cooper et al. (n=4) (2017). A comparison of results of empirical studies of supplementary search techniques and recommendations in review methodology handbooks: a methodological review. *Systematic Reviews*. DOI: `10.1186/s13643-017-0625-1` — verified (Crossref)
- **[Garousi2018]** Garousi et al. (n=3) (2018). Guidelines for including grey literature and conducting multivocal literature reviews in software engineering. *Information and Software Technology*. DOI: `10.1016/j.infsof.2018.09.006` — verified (Crossref)
- **[Briscoe2019]** Briscoe et al. (n=3) (2019). Conduct and reporting of citation searching in Cochrane systematic reviews: A cross‐sectional study. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1355` — verified (Crossref)
- **[Sutton2019]** Sutton et al. (n=4) (2019). Meeting the review family: exploring review types and associated information retrieval requirements. *Health Information & Libraries Journal*. DOI: `10.1111/hir.12276` — verified (Crossref)
- **[Haddaway2022]** Haddaway et al. (n=3) (2022). Citationchaser: A tool for transparent and efficient forward and backward citation chasing in systematic searching. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1563` — verified (Crossref)
- **[Wohlin2022]** Wohlin et al. (n=4) (2022). Successful combination of database search and snowballing for identification of primary studies in systematic literature studies. *Information and Software Technology*. DOI: `10.1016/j.infsof.2022.106908` — verified (Crossref)
- **[Hirt2023]** Hirt et al. (n=4) (2023). Citation tracking for systematic literature searching: A scoping review. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1635` — verified (Crossref)
- **[Hirt2024]** Hirt et al. (n=5) (2024). Guidance on terminology, application, and reporting of citation searching: the TARCiS statement. *BMJ*. DOI: `10.1136/bmj-2023-078384` — verified (Crossref)

### D5 screening

- **[Rathbone2015]** Rathbone et al. (n=4) (2015). Better duplicate detection for systematic reviewers: evaluation of Systematic Review Assistant-Deduplication Module. *Systematic Reviews*. DOI: `10.1186/2046-4053-4-6` — verified (Crossref)
- **[Ouzzani2016]** Ouzzani et al. (n=4) (2016). Rayyan—a web and mobile app for systematic reviews. *Systematic Reviews*. DOI: `10.1186/s13643-016-0384-4` — verified (Crossref)
- **[Gartlehner2020]** Gartlehner et al. (n=7) (2020). Single-reviewer abstract screening missed 13 percent of relevant studies: a crowd-based, randomized controlled trial. *Journal of Clinical Epidemiology*. DOI: `10.1016/j.jclinepi.2020.01.005` — verified (Crossref)
- **[Hamel2020]** Hamel et al. (n=6) (2020). An evaluation of DistillerSR’s machine learning-based prioritization tool for title/abstract screening – impact on reviewer-relevant outcomes. *BMC Medical Research Methodology*. DOI: `10.1186/s12874-020-01129-1` — verified (Crossref)
- **[McKeown2021]** McKeown et al. (n=2) (2021). Considerations for conducting systematic reviews: evaluating the performance of different methods for de-duplicating references. *Systematic Reviews*. DOI: `10.1186/s13643-021-01583-y` — verified (Crossref)
- **[Borissov2022]** Borissov et al. (n=8) (2022). Reducing systematic review burden using Deduklick: a novel, automated, reliable, and explainable deduplication algorithm to foster medical research. *Systematic Reviews*. DOI: `10.1186/s13643-022-02045-9` — verified (Crossref)

### D6 AI/LLM scope & gates

- **[OMara-Eves2015]** O’Mara-Eves et al. (n=5) (2015). Using text mining for study identification in systematic reviews: a systematic review of current approaches. *Systematic Reviews*. DOI: `10.1186/2046-4053-4-5` — verified (Crossref)
- **[Przybyla2018]** Przybyła et al. (n=8) (2018). Prioritising references for systematic reviews with RobotAnalyst: A user study. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1311` — verified (Crossref)
- **[Marshall2019]** Marshall et al. (n=2) (2019). Toward systematic review automation: a practical guide to using machine learning tools in research synthesis. *Systematic Reviews*. DOI: `10.1186/s13643-019-1074-9` — verified (Crossref)
- **[Chai2021]** Chai et al. (n=4) (2021). Research Screener: a machine learning tool to semi-automate abstract screening for systematic reviews. *Systematic Reviews*. DOI: `10.1186/s13643-021-01635-3` — verified (Crossref)
- **[Bhattacharyya2023]** Bhattacharyya et al. (n=4) (2023). High Rates of Fabricated and Inaccurate References in ChatGPT-Generated Medical Content. *Cureus*. DOI: `10.7759/cureus.39238` — verified (Crossref)
- **[Guo2023]** Guo et al. (n=6) (2023). Automated Paper Screening for Clinical Reviews Using Large Language Models: Data Analysis Study. *Journal of Medical Internet Research*. DOI: `10.2196/48996` — verified (Crossref)
- **[Walters2023]** Walters et al. (n=2) (2023). Fabrication and errors in the bibliographic citations generated by ChatGPT. *Scientific Reports*. DOI: `10.1038/s41598-023-41032-5` — verified (Crossref)
- **[Chelli2024]** Chelli et al. (n=10) (2024). Hallucination Rates and Reference Accuracy of ChatGPT and Bard for Systematic Reviews: Comparative Analysis. *Journal of Medical Internet Research*. DOI: `10.2196/53164` — verified (Crossref)
- **[Dagdelen2024]** Dagdelen et al. (n=8) (2024). Structured information extraction from scientific text with large language models. *Nature Communications*. DOI: `10.1038/s41467-024-45563-x` — verified (Crossref)
- **[Dennstadt2024]** Dennstädt et al. (n=5) (2024). Title and abstract screening for literature reviews using large language models: an exploratory study in the biomedical domain. *Systematic Reviews*. DOI: `10.1186/s13643-024-02575-4` — verified (Crossref)
- **[Han2024]** Han et al. (n=3) (2024). Automating Systematic Literature Reviews with Retrieval-Augmented Generation: A Comprehensive Overview. *Applied Sciences*. DOI: `10.3390/app14199103` — verified (Crossref)
- **[Khraisha2024]** Khraisha et al. (n=5) (2024). Can large language models replace humans in systematic reviews? Evaluating GPT ‐4's efficacy in screening and extracting data from peer‐reviewed and grey literature in multiple languages. *Research Synthesis Methods*. DOI: `10.1002/jrsm.1715` — verified (Crossref)
- **[Oami2024]** Oami et al. (n=3) (2024). Performance of a Large Language Model in Screening Citations. *JAMA Network Open*. DOI: `10.1001/jamanetworkopen.2024.20496` — verified (Crossref)
- **[Ofori-Boateng2024]** Ofori-Boateng et al. (n=4) (2024). Towards the automation of systematic reviews using natural language processing, machine learning, and deep learning: a comprehensive review. *Artificial Intelligence Review*. DOI: `10.1007/s10462-024-10844-w` — verified (Crossref)
- **[Polak2024]** Polak et al. (n=2) (2024). Extracting accurate materials data from research papers with conversational language models and prompt engineering. *Nature Communications*. DOI: `10.1038/s41467-024-45914-8` — verified (Crossref)
- **[Adel2025]** Adel et al. (n=2) (2025). Can generative AI reliably synthesise literature? exploring hallucination issues in ChatGPT. *AI & Society*. DOI: `10.1007/s00146-025-02406-7` — verified (Crossref)

---

*검증 요약: 총 71편. Crossref 검증 70편, arXiv API 검증 1편, 미검증 0편.
서지 필드는 전부 API 응답에서 취득했으며 본문 인용 키 71개가 모두 위 표에 대응한다 (자동 대조 통과).*



