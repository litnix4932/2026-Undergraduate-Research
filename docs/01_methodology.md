# 문헌검색 방법론 (현행판)

> **요약**
> - 연구 형태는 **systematic scoping/mapping review**다. 검색은 OpenAlex, 서지 검증은 Crossref로 역할을 나눈다.
> - 검색어(query)만으로는 recall이 구조적으로 부족하다. 그래서 **citation chasing을 recall의 주 수단**으로 둔다.
> - LLM은 API가 돌려준 실제 레코드와 원문을 **판정만** 한다. 서지·수치를 생성하지 않는다. 검증 관문(Gate)은 3단계다.
> - 완전성(completeness)은 주장하지 않는다. 중단은 한계 수확(marginal yield)에 근거한 실용 규칙으로 정한다.
>
> 라벨(①②③, [측정]/[저자해석]/[판단])은 [README](../README.md#표기)를 참조. 근거 문헌 71편의 서지는 [`methodology_references.csv`](../data/methodology_references.csv)에 있다. 본문에서 직접 언급하지 않은 문헌도 `decision`과 `relevance_note` 열에 어느 결정을 뒷받침하는지 기록되어 있다.

**근거의 한계 (먼저 읽을 것).** 근거 문헌 71편 중 화학·재료 분야에서 나온 방법론 근거는 3편뿐이다([Baykoucheva2011], [Polak2024], [Dagdelen2024]). 나머지는 의학, 정보학, 소프트웨어공학, 환경과학에서 왔다. 따라서 많은 결정은 직접 근거가 아니라 **인접 분야에서 옮겨온 근거**에 기댄다. 이것은 분야의 상태다. 재료·촉매 분야에는 검색 방법론 연구가 사실상 없다.

---

## D1. 리뷰 유형

**채택: systematic scoping/mapping review (hybrid)** — ②수정

- **scoping review**: "어떤 증거가 존재하고 공백(gap)은 어디인가"를 묻는 리뷰. 효과 크기를 추정하지 않는다.
- **systematic mapping**: 문헌을 분류 체계에 넣고 범주별 빈도를 세어 연구 지형을 보여주는 방식.

본 연구 질문은 효과 추정이 아니라 **증거 지형 파악과 gap 식별**이므로 scoping review에 해당한다[Munn2018]. "처리 조건 × 표면 성질" 분류표는 mapping의 산출물이다[Petersen2008]. 절차는 [Arksey2005]와 [Levac2010]을 따른다.

보고 기준은 다음과 같다.
- **PRISMA-ScR**: scoping review 보고 체크리스트(필수 20항목)[Tricco2018].
- **PRISMA-S**: 검색 과정 보고 체크리스트(16항목)[Rethlefsen2021].

| 기각한 대안 | 사유 |
|---|---|
| Full systematic review / meta-analysis | 실험 조건(전구체, 소성 온도·분위기, 전처리)이 논문마다 달라 결과를 합칠(pooling) 수 없다. 재료 실험용 risk-of-bias 도구(연구의 편향 위험 평가 도구)도 없다 |
| Narrative review | 정해진 절차가 없어 재현이 불가능하다[Snyder2019] |
| Bibliometric 단독 | 피인용 같은 계량 지표는 기전 질문에 답하지 못한다[Marzi2024]. 보조 도구로만 쓴다 |

**실행 방식**은 리뷰 유형과 별개의 축이다. 자동화는 각 단계를 빠르게 하는 수단일 뿐 리뷰 종류를 바꾸지 않는다[Marshall2019]. 채택한 방식은 API 기반 반자동 파이프라인에 LLM을 **판정자(judge)**로만 얹는 구조다(D6). 자동화가 사람의 판단을 *보조*하는 데까지는 근거가 있지만 *대체*하는 데에는 근거가 부족하다[OMara-Eves2015]. — ①확립 + ③신규

**재검토 조건**: 특정 하위 질문(예: 소성 온도 → Al(V) 분율)에 측정 프로토콜이 동질적인 연구가 10편 이상 모이면, 그 질문에 한해 정량 종합(조건–값 산점도)을 검토한다.

---

## D2. Source 역할 분리

"어느 DB가 가장 좋은가"는 잘못된 질문이다. 한 source가 모든 역할에서 최선인 경우는 없다. 예를 들어 Google Scholar는 coverage가 가장 넓다[Gusenbauer2018][Martin-Martin2020]. 그러나 재현 가능한 Boolean 검색(AND/OR/NOT 논리 검색)이 안 되어 주 검색엔진으로는 부적합하다[Gusenbauer2019]. 그래서 결정의 단위를 DB가 아니라 **역할**로 잡는다.

| 역할 | 주 source | 보강 | 금지 |
|---|---|---|---|
| (a) 문헌 발견 (discovery) | **OpenAlex API** | WoS·Scopus(수동 export), SciFinder·Reaxys, arXiv | Google Scholar를 주 엔진으로 |
| (b) 서지 검증 | **Crossref API** | arXiv API(preprint), 출판사 레코드 | OpenAlex 자기검증, LLM |
| (c) 인용 네트워크 | OpenAlex `referenced_works`/`cited_by` | Semantic Scholar, WoS | — |
| (d) 원문 | 출판사·OA 원문 | S2ORC, PMC | 초록만으로 주장 추출 |
| (e) 철회(retraction) 확인 | OpenAlex + Crossref 표시 | WoS | 확인 생략 |

- **OpenAlex**: 무료 공개 학술 메타데이터 DB. 참고문헌 coverage가 WoS·Scopus와 비슷하다[Culbert2025]. 단 **초록을 더 적게 보유한다**[Culbert2025]. 언어 메타데이터는 부정확하다[Cespedes2025]. 철회 논문도 더 많이 색인되므로 최종 목록의 철회 확인을 의무화한다[Ortega2024].
- **Crossref**: DOI 등록 기관. 출판사가 직접 기탁한 레코드라서 "이 DOI의 정식 서지가 무엇인가"의 기준점이 된다. 발견용이 아니라 **검증용**으로 쓴다.

**보강 경로 사용 조건.** 구독 DB와 arXiv는 모두 보강 경로다. 사용하면 PRISMA-S 수준으로 기록한다(검색일, 플랫폼, 전체 query 문자열, 결과 수, export 파일명). 기록이 없으면 그 결과는 쓰지 않는다.

**WoS·Scopus 보강은 필수다 (v2 개정, ②수정).** OpenAlex에서 Elsevier 논문의 초록 보유율이 **2.6%**로 측정되었다([04_query.md §0](04_query.md#0-설계-전제를-뒤집은-관측--openalex-초록-보유율)). 이 분야 핵심 저널은 대부분 Elsevier다. 따라서 OpenAlex 단독으로는 코퍼스의 약 73%를 **제목만으로** 검색하게 된다. 초록 기반 screening을 하려면 보강이 필요하다. Scopus의 `TITLE-ABS-KEY`는 저자 키워드까지 검색하므로 이 공백을 메운다.

**환경 제약.** 이 분석 환경에서는 WoS, Scopus, Google Scholar에 프로그램으로 접근할 수 없다. 그래서 자동 경로는 OpenAlex + Crossref(+arXiv)로 구성하고, 구독 DB는 사람이 수동으로 실행한다.

---

## D3. Query 개발

**Facet 분해.** PICO(임상연구용 Population–Intervention–Comparison–Outcome 틀)는 쓰지 않는다. 본 연구에는 환자군도 비교군도 없기 때문이다. 대신 검색 개념을 **facet**(독립적인 개념 묶음. 묶음 안은 OR, 묶음 사이는 AND로 결합)으로 나눈다[Booth2008]. 실제 facet과 어휘는 [04_query.md](04_query.md)에 있다. — ②수정

**통제어휘가 없다.** 의학 DB에는 MeSH 같은 **통제어휘**(색인자가 논문마다 표준 주제어를 붙인 것)가 있어서, 저자가 어떤 표현을 썼든 같은 개념으로 찾을 수 있다. OpenAlex와 Crossref에는 이것이 없다. 통제어휘가 없으면 키워드 검색으로 찾던 레코드의 1/3 이상이 사라질 수 있다[Gross2005]. 그러므로 표기 변이(γ-Al₂O₃ / gamma-alumina / transition alumina 등)를 사람이 직접 수확해 넣어야 한다. 그래도 query만으로는 부족하다. **citation chasing은 선택이 아니라 구조적 필수다.** — ②수정

**Recall과 precision은 trade-off다.**
- **recall(재현율)**: 관련 문헌 중 검색에 걸린 비율.
- **precision(정밀도)**: 검색 결과 중 실제로 관련 있는 비율.

의학 검색 필터 예에서 recall 97.4%를 얻을 때 precision은 4.4%였다[Terwee2009]. 즉 적격 1편당 20편 이상을 걸러야 한다. 본 분야 실측값은 [04_query.md §2](04_query.md#2-query-변이별-측정-결과)에 있다. — ①확립(수치는 재측정 필요)

**Query 개선 루프.** 개선 루프는 `seed 선정 → query 작성 → seed 검출 확인 → 미검출 원인 분석 → 용어 추가 → 재검색`이다. 이 루프는 기존 기법 세 가지의 결합이다.

| 구성 요소 | 기존 명칭 |
|---|---|
| 이미 아는 핵심 논문(**seed**)이 검색에 걸리는지 확인 | **known-item testing** [Terwee2009] |
| 찾은 논문에서 새 용어를 수확해 query 확장 | **pearl growing** [Booth2008] |
| 위를 반복 | iterative search strategy development [Levac2010][MacFarlane2022] |

pearl growing은 실패할 수 있다. 핵심 논문이 여러 DB에 흩어져 있으면 작동하지 않는다[Papaioannou2009]. 실패하면 citation chasing으로 대체한다.

**v2에서 추가된 query 원칙** (근거 측정은 모두 [04_query.md](04_query.md)):
1. **필드 제한 Boolean을 기본형으로 한다.** OpenAlex의 자연어 `search`는 지구화학, CO₂ 수소화 문헌으로 표류했다. 그래서 `filter=title_and_abstract.search:` + 명시적 Boolean을 쓴다. 절단 검색(`*`, 예: `reducib*`)이 지원되지 않으므로 변이를 모두 열거한다. — ②수정
2. **처리 조건(Treatment) facet은 검색식에서 뺀다.** 넣으면 결과는 17%만 줄고 핵심 seed 검출은 19/21 → 11/21로 무너진다. 처리 조건은 본문 Experimental에 있으므로 **추출 필드**로 다룬다. — ③신규
3. **facet은 배타적 분할이 아니다.** 예를 들어 `dehydroxylation`(탈수산기)은 처리이면서 현상이다. 한 용어를 여러 facet에 중복 배치할 수 있다. — ③신규
4. **2-tier 설계.** 단일 query로는 쓸 만한 precision과 recall을 동시에 얻을 수 없다. 그래서 전수 screening용 Tier 1과 recall 보완용 Tier 2로 나눈다. γ상 지정은 검색식이 아니라 screening 기준으로 옮긴다. — ③신규

**검증과 보고.**
- query 확정 전 **PRESS** 체크리스트를 자가 적용한다[McGowan2016]. PRESS는 사서가 검색식을 동료 검토할 때 쓰는 6요소 체크리스트다. 사서 검토 대신 자가 적용과 지도교수 1인 검토로 축소하는데, 이 축소가 효과를 유지한다는 근거는 없다. — ②수정
- 모든 검색은 PRISMA-S 16항목 수준으로 기록한다. — ①확립

---

## D4. 완전성 평가와 중단

**완전성은 증명할 수 없다.** 검색자가 "충분히 찾았다"고 믿을 때 실제 recall이 20% 미만이었던 사례가 있다[Blair1985]. 그러므로 보고서에서 "문헌을 모두 찾았다"는 서술을 금지한다. 대신 무엇을 어떻게 찾았고 어디서 멈췄는지를 기록한다. — ①확립

**Known-item testing은 진단 도구로만 쓴다.** "seed의 90%를 찾아야 한다" 같은 수치 기준(threshold)은 두지 않는다. 일반적으로 정당화된 기준이 없기 때문이다. 대신 미검출 seed마다 원인을 아래 코드로 기록한다. — ②수정

| 코드 | 의미 | 대응 |
|---|---|---|
| `TERM` | query에 없는 용어·표기 변이 사용 | 용어 추가 후 재검색 |
| `FIELD` | 해당 용어가 제목·초록에 없고 본문에만 있음 | citation chasing에 의존 |
| `COVERAGE` | source에 레코드 자체가 없음 | 보강 경로 검토 |
| `LOGIC` | Boolean 구조 오류 (AND/OR/괄호, facet 배정) | query 수정 후 PRESS 재적용 |
| `TYPE` | 문서 유형 필터로 배제됨 | 필터 조정 |

**Seed set은 의도적으로 다양화한다.** 서로 다른 연구그룹, 연도대, 방법(실험/DFT/반응)을 섞는다. seed가 편향되면 진단도 편향되기 때문이다. — ③신규

**Citation chasing은 필수다.** citation chasing(인용 추적)은 포함 논문의 참고문헌을 거슬러 가는 **backward(BWC)**와 그 논문을 인용한 문헌을 따라가는 **forward(FWC)** 두 방향으로 한다. 근거는 다음과 같다.
- citation tracking 연구의 96%에서 부가가치가 확인되었다[Hirt2023].
- DB 검색과 snowballing(인용 추적을 반복하는 것)을 결합하면 DB 검색 단독보다 30% 더 많은 논문을 찾는다[Wohlin2022].
- FWC는 체계적으로 과소 사용된다. Cochrane 리뷰 215편 중 BWC 172편, FWC 18편이었다[Briscoe2019].

포함이 확정된 모든 논문에 대해 양방향 1 round를 실행하고, TARCiS 권고(citation 검색 보고 지침 10항목)[Hirt2024]에 따라 보고한다. — ①확립

**SI 참고문헌은 사람이 직접 확인한다 (v2, ③신규).** Supplementary 파일의 참고문헌은 OpenAlex `referenced_works`에 들어가지 않는다. 자동 BWC가 이를 놓친다. 실제로 Jeong 2020의 핵심 주장 근거(Ammendola 2011)가 SI에만 있었다([02_evidence_framework.md §4](02_evidence_framework.md#4-사례-인용이-주장을-지지하지-않는다)). 중심 주장이 SI 그림·표에 근거하면 SI 참고문헌을 직접 연다.

**'문헌 희소성 vs 검색 실패'를 판정한다 (v2, ③신규).** 결과가 예상보다 훨씬 적을 때 query를 고치기 전에 다음을 한다.
1. 다른 어휘·facet 조합으로 같은 개념을 재검색한다.
2. 상위 결과가 **엉뚱한 분야**로 채워지는지 확인한다(어휘 오염).
3. 그 측정을 하는 인접 커뮤니티가 있는지 찾는다.
4. `문헌 희소` / `어휘 오염` / `query 오류` 중 하나로 판정을 기록한다.

**중단 기준 (③신규).** 이 기준은 완전성을 보장하지 않는다. 추가 검색의 **한계 수확(marginal yield)**, 즉 노력 대비 새로 얻는 적격 논문 수에 근거한 실용 규칙이다. 아래를 모두 만족하면 종료한다.
1. 모든 seed가 검출되었거나, 미검출 seed마다 원인 코드와 조치가 기록되었다.
2. 직전 citation chasing round의 신규 적격 논문 수가 검토량 대비 뚜렷이 줄었다. 수치 기준은 수집 착수 후 사전 고정하며, 사후 조정하지 않는다.
3. 마지막 query 수정이 새 적격 논문을 만들지 못했다.

종료 시 "왜 여기서 멈췄는가"를 marginal yield 수치와 함께 1문단으로 기록한다.

**Grey literature.** grey literature는 정식 출판되지 않은 학위논문, 보고서, 특허를 말한다. 기본적으로 제외하고 제외 사실을 기록한다. 특정 합성 조건이 특허에만 있는 정황이 보이면 그 주제에 한해 보강한다[Garousi2018]. — ②수정

---

## D5. Screening

**1인 연구의 누락을 숫자로 인정한다.** screening은 수집한 문헌을 기준에 따라 거르는 단계다. 검토자 1명이 초록을 screening하면 관련 연구의 13%를 놓친다(sensitivity 86.6%). 2명이면 3%를 놓친다[Gartlehner2020]. 본 연구는 1인이므로 이를 limitation에 명시하고 세 가지로 완화한다. — ①확립 + ③신규
1. LLM을 제2 검토자로 둔다. 사람과 LLM이 불일치한 레코드만 사람이 재판정한다.
2. 사람이 제외한 레코드에서 무작위 표본을 뽑아 재판정하고, 판정이 뒤집힌 비율을 보고한다.
3. citation chasing이 누락을 부분 보상한다.

**포함/제외 기준.** 기준은 검색 착수 전에 정의한다. seed로 파일럿 적용한 뒤 1회만 개정할 수 있다. 이후 변경하면 전체 판정을 재실행한다. — ②수정

| 구분 | 기준 (초안) |
|---|---|
| 포함 | γ-Al₂O₃(또는 γ상을 명시한 transition alumina)를 대상으로 한다. 합성·후처리 조건이 기술되어 있다. 표면·결함 구조 또는 산소·환원 거동의 실험·계산 관측을 보고한다 |
| 제외 | γ상이 특정되지 않은 alumina. 지지체 자체의 표면을 다루지 않는 단순 지지체 연구. 조건 기술이 없는 연구. 원문 입수 불가 |
| 보류 | 3분법(include / **borderline** / exclude)으로 처리한다. borderline은 버리지 않고 원문 단계에서 재판정한다[Wohlin2022] |

**Framework 라벨 (v2).** 원문 screening 때 각 논문에 어느 고리의 증거인지 라벨을 붙인다(`[P]→[S]`, `[O1]`, `[O2]`, `[O3]`, `[R1]`, `[R2]`, `[I]`, 복수 가능). 라벨 정의는 [02_evidence_framework.md §2](02_evidence_framework.md#2-연구-framework)에 있다. `[R2]` 라벨 논문에는 Tier A/B/C 판정을 추가한다.

**중복 제거.** 자동 도구마다 sensitivity/specificity 균형이 다르다[Rathbone2015][McKeown2021]. 수동 중복 제거조차 recall이 88.65%에 그쳤다[Borissov2022]. 채택 절차는 다음과 같다. — ②수정
1. DOI 정규화 후 완전 일치로 제거한다.
2. 정규화 제목 + 연도 + 제1저자 성으로 제거한다.
3. 경계 사례는 사람이 확인한다.
4. 단계별 제거 수를 기록한다.

**2단계 screening.** 제목·초록(TiAb) screening → 원문(full-text) screening 순서로 하고, 제외 사유를 코드로 기록한다. Rayyan(screening 웹 도구, 평균 40% 시간 절감[Ouzzani2016])은 선택적 보조로만 쓴다. — ①확립

---

## D6. AI/LLM 사용 범위와 검증 관문

**서지 생성은 전면 금지한다.** 근거는 측정된 실패율이다.
- ChatGPT가 생성한 인용 중 날조 비율은 GPT-3.5 55%, GPT-4 18%였다. 실재하는 인용 중에서도 각각 43%, 24%가 내용 오류를 포함했다[Walters2023].
- 의학 콘텐츠 참고문헌 중 실재하고 정확한 것은 7%였다[Bhattacharyya2023].
- 문헌 종합에서 hallucination(그럴듯하지만 사실이 아닌 생성) 비율이 91%였다[Adel2025]. [Chelli2024]도 같은 문제를 비교 평가했다.

"논문이 실재하는가"만 확인해서는 부족하다. 실재 논문에 대해서도 인용 내용이 틀릴 수 있다. 그래서 검증을 여러 단계로 나눈다.

**원칙.** LLM은 학술 API가 반환한 실제 레코드와 실제 원문에 대해서만 **판정(judge)**한다. 서지, 수치, 실험 조건, 기전을 **생성하지 않는다**. 원문을 근거로 주는 RAG(검색 증강 생성) 구조는 hallucination을 완화할 뿐 제거하지는 못한다[Han2024]. — ①확립 + ③신규

**이 프로젝트에서 관측된 실패.**
- 근거 71편 중 70편은 Crossref로 확인되었다. 1편은 arXiv DOI라서 arXiv API로 분기했다 → preprint용 검증 경로가 필요하다.
- Crossref 제목의 `<scp>` 태그 1건이 거짓 불일치를 냈다 → 비교 전 태그 제거와 정규화가 필수다.
- **LLM이 추출한 인용문 131개 중 8개(6.1%)가 원문에 없는 문구였다.** 초록을 함께 주고 "축자 인용만 하라"고 지시했는데도 그랬다. → 자동 축자 대조는 필수다.

| 단계 | AI 허용 | 요구 검증 |
|---|---|---|
| Query 용어 제안 | 보조 | 사람 전수 승인 + PRESS + known-item 진단 |
| 문헌 발견, 서지 생성, 인용 검증, 과학적 결론 | **금지** | 레코드는 API에서만, 검증은 Gate가 수행 |
| TiAb screening | 제2 검토자 | 불일치 전수 재판정 + 제외 표본 재검토 |
| Full-text screening | 보조 | 사람이 최종 판정 |
| 구조화 추출 | 보조 | **Gate 2** |
| 요약 | 허용 | 요약에 새 수치·주장이 없는지 대조 |

**LLM screening 성능은 일관되지 않다.**
- 포함 논문에 대한 sensitivity가 0.76에 그친 사례가 있다. 놓치는 쪽이 포함 논문이다[Guo2023].
- 프롬프트 최적화로 0.75 → 0.91로 개선된 사례가 있다[Oami2024].
- 프롬프트를 사소하게 바꾸기만 해도 성능이 크게 변했다[Dennstadt2024].
- 우연 일치를 보정하면 성능 점수가 하락했다[Khraisha2024].
- 작업량 절감 근거도 있다. [Hamel2020]은 중앙값 47.1% 감소, [Chai2021]은 60–96% 절감을 보고했다. 다만 사용자의 자만(complacency)이 위험 요인이다[Przybyla2018].

→ **채택**: recall 우선 프롬프트를 쓰고, LLM 단독 제외는 금지한다. 사용 전 소규모 라벨 세트에서 sensitivity를 직접 측정해 기록한다. 타 연구의 수치는 가져다 쓸 수 없다. — ②수정

추출 보조는 재료 분야 직접 근거가 있다. 대화형 LLM에 후속 질문으로 재확인시키면 재료 데이터 추출의 precision·recall이 약 90%에 도달했다[Polak2024]. 구조화(JSON) 출력도 가능하다[Dagdelen2024]. 두 연구 모두 정확도를 **별도로 측정**했다는 점이 중요하다. — ②수정

### Gate 1 — 서지 검증

①확립 + ③신규. discovery에서 얻은 레코드를 Crossref(preprint는 arXiv API)와 대조한다.

| 검사 | 통과 조건 |
|---|---|
| DOI | 검증 source에서 해석(resolve)됨 |
| 제목 | 유니코드 정규화, 태그 제거 후 앞 60자 일치 |
| 저자 | 제1저자 성 일치 |
| 연도 | 차이 ≤ 1년 (온라인 선공개 연도 차이 허용) |
| Venue | 기록만 (불일치는 경고) |
| 철회 | 표시 확인 |

상태값은 `verified` / `verified_preprint` / `mismatch` / `unverified` 넷이다. **앞의 두 상태가 아닌 레코드는 어떤 경우에도 evidence synthesis(증거 종합)에 투입하지 않는다.** 이런 레코드는 삭제하지 않고 격리(quarantine)하며, 건수와 사유를 보고한다.

### Gate 2 — 주장(claim) 검증

③신규. Gate 1을 통과해도 "그 논문이 실제로 무엇을 보고했는가"는 보장되지 않는다. 추출한 주장마다 다음 필드를 채운다(**claim-level provenance**: 주장 하나하나의 출처 기록).

| 필드 | 내용 |
|---|---|
| `paper_id`, `claim_id`, `claim_text` | DOI, `{DOI}#c{n}`, 주장 1문장 |
| `source_location` | page / section / figure / table 중 최소 1개 |
| `supporting_span` | 원문에서 **축자(verbatim) 복사**한 구절 |
| `span_verified` | 그 구절이 원문에 실제로 있는지 자동 대조한 결과 |
| `method`, `conditions`, `evidence` | 측정 방법, 실험 조건, 측정값과 단위 |
| `interpretation_level` | `measured_fact`(측정값) / `author_interpretation`(저자 해석) / `ai_inference`(AI·연구자 추론) |
| `verification_status`, `extracted_by` | `verified`/`unverified`/`conflicted`, `human`/`llm:<model>` |

처리 규칙은 다음과 같다.
- `span_verified = False`이면 자동 기각하고 사람이 재추출한다.
- 같은 조건에서 다른 논문과 값이 상반되면 `conflicted`로 표시한다. 폐기하지 않고 **상충 증거로 따로 집계**한다.
- **`ai_inference`는 증거로 집계하지 않는다.** 특히 "Al(V) 또는 oxygen vacancy를 보고했다"에서 "reducibility가 입증되었다"로 넘어가는 추론은 `ai_inference`다.

### Gate 3 — 인용 지지 검증

v2 신설, ③신규. **필요한 이유.** 서지가 정확하고(Gate 1) 저자가 실제로 그렇게 썼어도(Gate 2), **인용된 문헌이 그 주장을 실제로 지지하는지**는 따로 확인해야 한다. 실제 사례가 있다. Jeong 2020이 인용한 Ammendola 2011은 그 주장을 지지하지 않았다([02_evidence_framework.md §4](02_evidence_framework.md#4-사례-인용이-주장을-지지하지-않는다)).

**적용 범위.** 중심 주장에만 적용한다: `[R2]`·`[O3]` 라벨 주장과 연구 동기·결론에 직접 쓰는 주장. 전 인용에 적용하면 비용이 과도하다. 판정에는 **원문 전문이 필요하다.** 입수할 수 없으면 그 주장은 결론에 쓰지 않는다.

| 검사 | 질문 |
|---|---|
| 실험 종류 | 주장이 전제하는 측정과 인용 문헌이 수행한 측정이 같은가 (예: H₂-TPR vs CO-TPR) |
| 조건 범위 | 온도·분위기·시료가 겹치는가 |
| 귀속 | 인용 문헌의 저자가 그 신호를 같은 현상으로 해석했는가 |
| 주장 존재 | 인용 문헌에 그 주장이 실제로 있는가 |

판정값은 네 가지다.
- `supported`: 사용 가능.
- `partially_supported`: 범위를 좁혀 재서술하고 사용.
- `not_supported`: 사용 금지. 인용 오류를 기록하고 주장을 격리.
- `unreadable`: 원문 미입수. 주장을 격리.

---

## 파이프라인

```
S0    연구질문 → facet 분해
S0.5  검색 가능 텍스트 사전 측정 (출판사·연도별 초록 보유율)        ← v2 신설
S1    Seed set 구성 (그룹·연도·방법 다양화)
S2    Query 작성 (필드 제한 Boolean)
S3    Known-item 진단 → TERM·LOGIC이면 S2로 복귀
S4    본 검색: Tier 1(OpenAlex) + WoS·Scopus 보강 (PRISMA-S 기록)
S5    중복 제거 → Gate 1 (unverified는 격리)
S6    Citation chasing 1 round (BWC+FWC, 중심 주장은 SI 참고문헌 수동 확인) → 신규는 S5로
S7    TiAb screening (사람 + LLM 제2검토자) → include / borderline / exclude
S8    Full-text screening (framework 라벨, 제외 사유 코드)
S9    구조화 추출 → Gate 2 → (중심 주장) Gate 3
S10   Evidence mapping (조건 × 표면 성질, 상충 증거 별도 집계)
S11   보고 (PRISMA-ScR + PRISMA-S + 중단 사유 + 격리 통계 + limitation)
```

**S0.5가 중요한 이유 [판단].** 이 단계가 없었다면 3-facet AND 설계를 그대로 채택해 핵심 seed의 절반 이상을 놓쳤을 것이다. 게다가 그 원인도 몰랐을 것이다. 비용은 API 호출 몇 번이다.

## 추출 항목 (S9) — ③신규

| 범주 | 필드 |
|---|---|
| 서지 | DOI, 연도, 저널, 연구그룹 |
| 물질 | 상(γ 확인 여부와 근거), 비표면적, 결정자 크기, 전구체(boehmite/gibbsite/alkoxide 등) |
| 합성·열처리·전처리 | 합성법, pH, 숙성 / 소성 온도·시간·승온속도·분위기, 재수화·탈수화 이력 / 진공·환원·산화 처리 조건 |
| 표면 관측 | Al(IV)/Al(V)/Al(VI) 분율, OH 종류·밀도, 산점(Lewis/Brønsted) 종류·세기·밀도 |
| 산소·환원 거동 | 산소공공 관련 관측, H₂ 소모량, H₂O 생성 정량 여부, 재산화, 산소 교환, **Tier 판정** |
| 방법·해석·품질 | characterization·계산 방법과 조건, 저자 해석, 조건 기술 완전성 |

## 의학 방법론의 전이 가능성

| 의학 분야의 전제 | 본 연구 | 처리 |
|---|---|---|
| PICO, 통제어휘(MeSH) | 없음 | facet 분해 + 용어 수확 + citation chasing 의무화 |
| 연구설계 위계(RCT 등), risk-of-bias 도구 | 비적용 / 없음 | 도구를 만들지 않는다. 조건 기술 완전성과 방법의 직접성을 기록만 하고 등급화하지 않음 |
| meta-analysis | 공통 효과 척도 없음 | mapping + 조건–값 산점도 수준 |
| 이중 검토자, 사서 협업 | 1인 | 13% 누락 명시 + 3중 완화, PRESS 자가 적용 |

**요약하면** 전이되는 것은 **절차적 규율**(사전 기준, 2단계 screening, 검색 기록, 투명한 보고)이다. 전이되지 않는 것은 **인식론적 장치**(설계 위계, 편향 평가, 효과 pooling)다. PRISMA 2020 자체는 통계 종합이 없는 리뷰에도 적용되도록 설계되었다[Page2021b]. 다만 환경 분야에서는 PRISMA의 메타분석 편향이 문제로 지적되었다[Haddaway2018].

검토했으나 쓰지 않은 기법도 있다.
- **Capture–recapture 누락 추정**: 검색 경로들이 통계적으로 독립이어야 하는데 이 조건이 성립하지 않는다. 완전성을 수치로 주장하지도 않는다.
- **Cohen's κ**(검토자 간 일치도): 검토자가 1명이라 산출할 수 없다.
- **PROSPERO 사전등록**: 재료 분야 등록 관행이 없다. 대신 이 문서를 버전 고정 프로토콜로 쓴다.

## 한계와 재검토 조건

**한계 (보고서에 옮길 것)**
1. 근거의 분야 편향: 화학·재료 직접 근거는 71편 중 3편이다.
2. 1인 검토로 약 13%가 구조적으로 누락된다.
3. 완전성을 보장하지 않는다.
4. 구독 DB 없이 OpenAlex에 의존하므로 BWC 정확도가 WoS보다 낮을 수 있다[Gusenbauer2024].
5. Gate 2·3은 검증된 표준이 아니며, 자체 오류율도 미측정이다.
6. LLM 성능이 프롬프트에 의존한다. 프롬프트를 버전 고정하고, 바꾸면 재측정한다.
7. SciFinder/Reaxys가 없어 특정 합성 경로 문헌이 누락될 수 있다. 이 DB들은 의학 DB와 문서 중복이 20–24%에 불과한 보완재다[Baykoucheva2011].

**재검토 조건**

| 조건 | 조치 |
|---|---|
| WoS/Scopus 보강 실행 | OpenAlex 단독 대비 신규 적격 논문 수를 측정하고 D2를 갱신 |
| known-item 진단에서 `COVERAGE`가 3건 이상 | source 구성 재검토 |
| LLM screening sensitivity < 0.9 | LLM 제2검토자 역할 축소 또는 제외 |
| Gate 2 자동 기각률 > 15% | 추출 프롬프트 재설계 또는 수동 추출 |
| 동질적 연구 10편 이상 | 해당 하위 질문에 정량 종합 검토 |
