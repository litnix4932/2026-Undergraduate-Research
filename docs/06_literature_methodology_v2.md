# Literature Search Methodology v2 — 개정판
### γ-Al₂O₃ surface chemistry & defect engineering 문헌연구

**v1 문서**: `literature_methodology.md` (결정 D1–D6, 근거 71편)
**이 문서의 성격**: v1을 대체하지 않는 **개정판(amendment)**. v1 대비 **변경된 항목의 전문**과 그 근거를 담는다. 언급되지 않은 결정은 v1이 그대로 유효하다.
**개정 근거**: `seed_set_analysis.md` · `seed_set_v2_review.md` · `reducibility_criteria.md` · `query_v1.md` · `known_item_diagnostic.csv`

### 라벨 (v1과 동일)

| 라벨 | 의미 |
|---|---|
| **①확립** | 기존 방법론 문헌에서 확립된 practice |
| **②수정** | 확립된 practice이나 본 분야 적용을 위해 수정 |
| **③신규** | 본 프로젝트의 신규 제안 — 직접 근거 없음 |

---

## 0. 개정 요약

| # | 개정 항목 | v1 | v2 | 근거 |
|---|---|---|---|---|
| 1 | 연구 framework | Processing → Structure → Oxygen behavior → Reducibility/Reactivity (4단 선형) | **[P] → [S] → [O1]/[O2]/[O3] → [R1]/[R2] + [I] 병렬 경로** | `reducibility_criteria.md` §4 |
| 2 | 증거 인정 기준 | 없음 | **Tier A/B/C 기준**을 결정 ⑤·⑥에 편입 | `reducibility_evidence_criteria.csv` |
| 3 | Gate 구조 | Gate 1(서지) + Gate 2(claim) | **+ Gate 3 (인용 지지 검증)** | Ammendola 사례 (`seed_set_v2_review.md` §1.3) |
| 4 | 보강 경로의 지위 | WoS/Scopus = optional | **abstract 기반 screening을 하려면 필수** | `query_v1.md` §0 (Elsevier abstract 2.6%) |
| 5 | query 기본형 | 필드 제한 Boolean (v1 후반에 도출) | **+ Treatment facet 배제 + 2-tier 설계** | `query_v1.md` §2.1 |
| 6 | SI 참고문헌 | 절차 없음 | **수동 확인을 절차로 신설** | `seed_set_analysis.md` §4.1 |
| 7 | 결과 수가 적을 때 | 규정 없음 | **'문헌 희소성 vs 검색 실패' 판정 절차** | `query_v1.md` §5 |
| 8 | 파이프라인 단계 | S0 → S11 | **S0.5 "검색 가능 텍스트 사전 측정" 신설** | `query_v1.md` §0 |

---

## 1. 개정 1 — 연구 framework (4단 선형 → 5축 + 2분기)

### 1.1 변경 이유

v1의 4단 선형 사슬은 세 가지 오류를 구조적으로 허용했다 **[판단]**.

1. **"Reducibility/Reactivity"를 한 칸에 묶은 것** — Joubert 2006의 25 °C H₂ 활성화는 reactivity이지만 reducibility가 아니다(산소 제거 없음). 한 칸에 두면 *"반응성이 있으니 환원성이 있다"*는 추론이 framework에 내장된다.
2. **"Oxygen behavior"가 세 현상을 뭉친 것** — Ammendola 2011(OH가 산소원)과 Martin 1996(격자 산소 교환)은 산소원이 다른 별개 현상인데 v1에서는 같은 [C]에 들어갔다.
3. **선형 구조가 site-specificity를 담지 못한 것** — reducibility는 물질 속성이 아니라 site·계면 속성이다(`reducibility_criteria.md` §1.2).

### 1.2 개정된 framework

```
[P] Processing / Pretreatment
      │   소성 · 환원 · 수열/steam · 진공 · 플라즈마 · 합성경로 · 전구체 · 도핑
      ▼
[S] Surface & defect structure
      │   Al 배위(IV/V/III) · OH 피복률·유형 · 표면 종결면 · 양이온 공공(구조적)
      ▼
      ├─────────────────────┬──────────────────────┬─────────────────────┐
[O1] OH / 물 화학         [O2] 격자산소 이동        [O3] 산소 제거         │
     산소원 = OH              산소 수 보존 (교환)       산소 수 감소 (공공)    │
      │                         │                        │               │
      ▼                         ▼                        ▼               │
[R1] Surface reactivity                        [R2] Reducibility         │
     H₂/CH₄ 활성화 · Lewis 산염기                   MvK 의미:               │
     anchoring · WGS · spillover                  산소 제거 + 전자 귀속     │
      ▲                                           + 가역성                │
      │                                            ▲                     │
      └────────── [I] Metal/oxide interface 경로 ───┴─────────────────────┘
                  (담지 금속이 있을 때만 열리는 병렬 경로)
```

**[판단] 핵심은 [R1]과 [R2]의 분리, [O]의 3분할, [I]의 병렬화다.** 이 셋이 v1에서 혼동을 일으킨 지점이다.

**라벨: ③신규** — 이 구조를 명시한 선행 문헌은 없다. 단 [R2]의 내용은 Ruiz Puigdollers 2017의 정의를, [I]의 존재는 같은 논문의 계면 논증을 따른다.

---

## 2. 개정 2 — Tier A/B/C 증거 기준의 편입

`reducibility_evidence_criteria.csv`의 12개 기준을 **결정 ⑤(screening)과 결정 ⑥(추출)에 정식 편입**한다.

### 2.1 Screening 단계에서의 사용

full-text screening 시 각 논문에 **어떤 고리의 증거를 담고 있는지** 라벨을 붙인다: `[P]→[S]` / `[O1]` / `[O2]` / `[O3]` / `[R1]` / `[R2]` / `[I]`. 복수 가능.

### 2.2 추출 단계에서의 사용

`[R2] Reducibility` 라벨이 붙은 논문에 대해서만 Tier 판정을 추가한다.

| Tier | 판정 조건 | synthesis에서의 취급 |
|---|---|---|
| **A** | A1(H₂ 소모 + H₂O 생성 동시 정량) **+ (A2 재산화 적정 또는 A3 전자 귀속 확인)**. A4(¹⁸O MvK)가 있으면 최강 | **reducibility 증거로 집계** |
| **B** | OSC류 / ¹⁸O 교환 / 계산 E_Ovac | 보조 지표로만. "reducible하다"는 주장에 사용 금지 |
| **C** | TCD 단독 TPR · H₂ 소모량 단독 · Al 배위·OH 변화 · 복합시료 신호 · 산소 제거 없는 반응성 | **reducibility 증거로 집계하지 않음.** C5는 [R1] 증거로는 유효 |

> **불변 규칙**: Tier C 증거만을 근거로 "γ-Al₂O₃가 환원된다"는 서술을 생성하지 않는다. Tier C 문헌은 **무엇을 측정했는지 그대로** 기술한다(예: "H₂ 분위기 승온에서 267 °C에 TCD 피크가 관측되었다 — 저자는 이를 표면 Al 환원으로 해석").

**라벨: ③신규** (기준 조합) + **①확립** (각 측정 자체는 ceria·titania 문헌의 관행)

---

## 3. 개정 3 — Gate 3 신설 (인용 지지 검증)

### 3.1 왜 필요한가

v1의 Gate 1(서지 검증)과 Gate 2(claim provenance)를 **모두 통과한 인용이 내용적으로 주장을 지지하지 않는 사례**가 실제로 발생했다.

**관측 사례** (`seed_set_v2_review.md` §1.3): Jeong 2020 Supplementary Fig. 1은 H₂-TPR TCD 피크 267/661 °C를 "surface/bulk Al의 환원"으로 귀속하며 Ammendola 2011을 인용한다. 그러나 원문을 읽은 결과 Ammendola 2011은 **CO-TPR** 연구이고(맨 alumina의 H₂-TPR은 아예 없음), 신호 위치는 **594–602 °C**이며, 귀속은 **표면 OH기와 CO의 WGS 반응**이고, **Al 환원 주장은 없다.** 오히려 "TPR 정량을 환원으로 읽지 말라"는 경고문이다.

Gate 1은 "Ammendola 2011이 실재하고 서지가 정확한가"만 확인하고, Gate 2는 "Jeong 2020이 그렇게 썼는가"만 확인한다. **인용의 방향이 반대라는 사실은 두 Gate 어디에도 걸리지 않는다.**

### 3.2 Gate 3 명세

> **목적**: 어떤 주장 C가 문헌 X를 근거로 제시될 때, **X가 실제로 C를 지지하는지** 확인.
> **적용 범위**: 본 연구의 **중심 주장**에 해당하는 인용에 한정한다(모든 인용에 적용하면 비용이 과도하다). 구체적으로 [R2]·[O3] 라벨 claim과, 연구 motivation·결론에 직접 쓰이는 claim.

| 검사 항목 | 통과 조건 |
|---|---|
| 실험 종류 일치 | C가 전제하는 측정과 X가 수행한 측정이 같은가 (예: H₂-TPR vs CO-TPR) |
| 조건 범위 일치 | 온도·분위기·시료가 겹치는가 |
| 귀속 일치 | X의 저자가 그 신호를 C와 같은 현상으로 귀속했는가 |
| 주장 존재 | X에 C에 해당하는 주장이 **실제로 있는가** |

| 상태 | 처리 |
|---|---|
| `supported` | C를 X 근거로 사용 가능 |
| `partially_supported` | 범위를 좁혀 재서술 후 사용 |
| **`not_supported`** | **C를 X 근거로 사용 금지.** 인용 오류를 별도 기록하고, C를 미검증으로 격리 |
| `unreadable` | X 원문 입수 불가 — C는 미검증 격리 |

**운영 규칙**: Gate 3은 **원문 전문 열람을 요구한다**(초록으로는 판정 불가 — Ammendola 사례에서 초록만으로는 CO-TPR임을 알 수 있었지만 신호 위치와 정량값은 본문에만 있었다). 따라서 중심 주장의 인용은 **전문 입수를 전제**로 하고, 입수 불가 시 그 주장은 결론에 쓰지 않는다.

**라벨: ③신규** — 인용 지지 검증을 별도 gate로 규정한 선행 문헌은 찾지 못했다.

---

## 4. 개정 4 — 보강 경로의 지위 격상

### 4.1 측정된 제약

**[측정]** (`query_v1.md` §0) γ-Al₂O₃ 코퍼스 600편 표본의 OpenAlex abstract 보유율:

| 출판사 | 보유율 | 편수 |
|---|---|---|
| **Elsevier BV** | **2.6%** | **422** |
| ACS | 100% | 96 |
| Springer | 4.8% | 21 |
| RSC | 100% | 16 |
| Wiley | 93.8% | 16 |
| 전체 | **27.2%** | 600 |

이 분야의 중심 저널(Journal of Catalysis, Applied Catalysis A/B, Catalysis Today, Surface Science)이 전부 Elsevier다.

### 4.2 개정 내용

| v1 | v2 |
|---|---|
| WoS/Scopus = **optional 보강 경로**. "known-item diagnostic에서 미검출 seed가 발견될 때" 사용 | **abstract(또는 저자 키워드) 기반 screening을 수행하려면 필수.** OpenAlex 단독 경로는 코퍼스 약 73%에 대해 **제목만 검색하는 파이프라인**이 되므로, 그 한계를 수용하지 않는 한 보강이 필요하다 |

Scopus의 `TITLE-ABS-KEY`는 **저자 키워드까지** 포함하므로 Elsevier 문헌의 개념어를 포착할 수 있다 — 이것이 보강의 핵심 가치다 **[판단]**.

**라벨: ②수정** — 보강 경로의 존재는 v1에서 이미 ①확립이었고, 그 **필수성 판정**이 측정에 의해 바뀌었다.

---

## 5. 개정 5 — Query 설계 원칙

### 5.1 추가되는 세 원칙

**① 필드 제한 Boolean을 기본형으로 한다** (v1 후반에 도출, v2에서 정식화)
OpenAlex의 자연어 `search` 파라미터는 본 주제에서 지구화학·CO₂ 수소화 문헌으로 표류한다. `filter=title_and_abstract.search:` + 명시적 Boolean·인용부호를 기본형으로 고정한다. 절단(`*`)을 지원하지 않으므로 변이를 전부 열거한다. **라벨: ②수정**

**② Treatment facet을 검색식에서 제외한다**
**[측정]** (`query_v1.md` §2.1) Treatment facet 추가 시 결과 수는 67,886 → 56,350(−17%)인데 core seed 검출은 19/21 → **11/21로 급감**한다. 처리 조건은 제목·초록에 거의 등장하지 않고 본문 Experimental에 있다.
→ 처리 조건은 **검색 facet이 아니라 추출 필드**로 다룬다. **라벨: ③신규**

**③ facet은 배타적 분할이 아니다**
`dehydroxylation`을 Treatment facet에만 배치해 Ingram-Jones 1996이 탈락한 LOGIC 오류가 발생했다. 한 용어가 처리이면서 현상일 수 있으므로 **복수 facet 중복 배치를 허용**한다. **라벨: ③신규**

### 5.2 2-tier 검색 설계

**[측정]** 단일 Boolean query로 쓸 만한 precision과 known-item recall을 동시에 달성할 수 없다 — core seed 6/21은 5,758건, 21/21은 93,857건으로 **16배 차이**.

| Tier | 구성 | 역할 |
|---|---|---|
| **Tier 1** | γ 표기 요구 + 현상 facet (5,758건) | 재현 가능하고 **전수 screening이 가능한** 기준 집합 |
| **Tier 2** | ① citation chasing(주 담당) ② 현상별 분할 검색 ③ WoS/Scopus 보강 | Tier 1이 놓치는 recall 담당 |

**γ상 지정은 검색식이 아니라 screening 기준으로 옮긴다** — **[측정]** 물질 facet에 γ 표기를 요구하면 core seed의 71%를 잃는다(대부분의 논문이 검색 가능한 텍스트에서 자신을 "alumina"로만 부른다). **라벨: ③신규**

---

## 6. 개정 6 — SI 참고문헌 수동 확인 절차

**관측 근거**: Jeong 2020의 핵심 주장(TCD = Al 환원)의 출처인 Ammendola 2011은 **본문 참고문헌이 아니라 Supplementary 참고문헌**에 있었고, OpenAlex `referenced_works`에 **포함되지 않아** 자동 backward citation chasing에서 누락되었다.

> **절차**: 본 연구의 **중심 주장이 Supplementary 자료의 그림·표에 근거하는 경우**, 해당 SI 파일의 참고문헌 목록을 **사람이 직접 열어 확인**한다. 자동 citation chasing 결과만으로 provenance 추적을 종료하지 않는다.

**라벨: ③신규**

---

## 7. 개정 7 — '문헌 희소성 vs 검색 실패' 판정 절차

**관측 근거**: Tier A 표적 검색에서 A1(H₂O 정량 + TPR)은 **36건**만 반환했고 상위 결과가 전부 담지금속계였다. 이때 "query가 나쁘다"와 "문헌이 없다"를 구분해야 한다.

> **절차**: 결과 수가 예상보다 현저히 적을 때, query를 고치기 전에 다음을 수행한다.
> 1. **독립 경로 재검색** — 다른 어휘 조합, 다른 facet 구성으로 같은 개념을 재검색한다.
> 2. **상위 결과의 성격 확인** — 결과가 적은 것이 아니라 **엉뚱한 것**이 나오는지 본다(어휘 오염).
> 3. **인접 커뮤니티 탐색** — 그 측정을 하는 다른 분야가 있는지 확인한다.
> 4. 세 결과를 종합해 `문헌 희소` / `어휘 오염` / `query 오류` 중 하나로 **판정을 기록**한다.

**이 절차로 확인된 것** (`query_v1.md` §5): A1은 **문헌 희소 확정**, A2·A3은 **어휘 오염**(ceria·담지금속 문맥), A4는 **인접 커뮤니티 발견**(고온산화·산화피막 분야의 ¹⁸O/SIMS alumina scale 연구).

**라벨: ③신규**

### 7.1 반복 확인된 패턴 — 기록해 둘 것 [판단]

γ-Al₂O₃의 산소 거동에 관한 증거는 **촉매 문헌이 아니라 인접 커뮤니티에 축적되어 있다**는 패턴이 세 번 독립적으로 확인되었다.

| 영역 | 담당 커뮤니티 | 확인된 곳 |
|---|---|---|
| 산소공공 분광 (F-center 등) | 핵재료·광학 (중성자 조사 α-Al₂O₃) | `seed_set_analysis.md` §4.3 |
| 벌크 환원의 실제 조건 | 금속공학 (탄소열 환원) | `reducibility_criteria.md` (Ostrovski 2010) |
| ¹⁸O 산소 수송 추적 | 고온산화·산화피막 (alumina scale) | `query_v1.md` §5.1 |

→ 전면 수집 단계에서 이 세 커뮤니티를 **별도 검색 축**으로 둔다. 단 모두 α상 또는 피막이므로 **γ상 분말로의 전이 가능성은 개별 평가**가 필요하다.

---

## 8. 개정 8 — 파이프라인에 S0.5 신설

v1의 S0 → S11 단계 사이에 **검색 가능 텍스트 사전 측정** 단계를 넣는다.

| 단계 | 목적 | 방법 | 산출물 |
|---|---|---|---|
| **S0.5** | 검색 대상 텍스트가 실제로 존재하는지 확인 | 대상 주제의 표본(수백 편)에 대해 **abstract 보유율을 출판사·연도별로 측정** | 보유율 표 + 그에 따른 query 설계 제약 |

**[판단] 이 단계가 없었다면 3-facet AND 설계를 그대로 채택했을 것이고, core seed의 절반 이상을 놓친 채 그 원인을 몰랐을 것이다.** 비용은 API 호출 몇 번이고, 설계 전체를 바꾸는 정보를 준다.

**라벨: ③신규**

---

## 9. 이번 개정의 관측 근거 요약

v2의 개정은 모두 **이번 세션에서 실제로 측정한 값**에 근거한다.

| 관측 | 값 | 개정 항목 |
|---|---|---|
| OpenAlex abstract 보유율 (γ-Al₂O₃ 600편) | 27.2% 전체 / Elsevier 2.6% | 개정 4·5·8 |
| seed 27편의 abstract 보유 | 12/27 | 개정 4·8 |
| γ 표기 요구 시 core seed 검출 | 6/21 | 개정 5 |
| Treatment facet 추가 시 core seed | 19/21 → 11/21 (결과 −17%) | 개정 5 |
| 27/27 recall의 결과 수 | 93,857건 (6/21은 5,758건) | 개정 5 |
| TERM 교정으로 회복된 seed | 3편 (water-gas conversion, surface site, dehydroxylation 배치) | 개정 5-③ |
| query로 도달 불가한 seed | 1편 (Prins 2020 — 제목만, abstract 없음) | 개정 5 (citation chasing 주 담당) |
| Tier A1 표적 결과 수 | 36건, 상위 전부 담지금속계 | 개정 7 |
| Gate 1·2를 통과했으나 지지되지 않은 인용 | 1건 (Jeong 2020 → Ammendola 2011) | 개정 3 |

---

## 10. 변경되지 않은 v1 결정

다음은 v1 그대로 유효하다.

- **결정 ①** review methodology = systematic scoping/mapping hybrid, 보고는 PRISMA-ScR + PRISMA-S. execution/automation을 독립 축으로 분리.
- **결정 ②** source 역할 분리 (discovery=OpenAlex / verification=Crossref / citation=OpenAlex+Semantic Scholar / full-text=publisher·OA / retraction 확인). **단 보강 경로의 지위는 개정 4로 변경.**
- **결정 ③** PICO 미사용, 3-facet 분해, PRESS 자가 적용, PRISMA-S 16항목 기록. **단 facet 구성은 개정 5로 변경.**
- **결정 ④** known-item testing을 정량 threshold 없는 **진단 도구**로 사용. 중단은 marginal yield 기반 pragmatic criterion. completeness 보장 서술 금지. → **이번 세션에서 실제로 이 규칙대로 운용되었고 잘 작동했다**(원인코드 5종으로 전부 분류, R3에서 한계 수확 근거로 중단).
- **결정 ⑤** 3분법 screening(include/borderline/exclude), 단일 검토자 13% 누락 명시, DOI→정규화 제목 2단계 중복 제거.
- **결정 ⑥** LLM은 API 레코드와 실제 full text만 판단, 서지·수치 생성 금지. Gate 1·2 유지(Gate 3 추가).

---

## 11. 다음 단계와 미해결 항목

### 11.1 바로 실행 가능한 것

1. **Tier 1 집합(5,758건) 확보 후 제목 수준 screening** — 현상별로 쪼개면 C1 3,482 / C3 1,675 / C2 1,195 / C4 539건으로 분할 가능.
2. **Scopus/WoS 보강 1회 실행** (`query_v1.md` §6의 변환형 사용) 후 OpenAlex 단독 대비 신규 적격 논문 수 측정 → 개정 4의 "필수" 판정을 정량 확인.
3. **고온산화·산화피막 커뮤니티 탐색** (§7.1) — `Oxidation of Metals`, `Corrosion Science` 계열의 alumina scale ¹⁸O 연구.

### 11.2 미해결

1. **Tier A 문헌이 실재하는지** — A1은 희소 확정이나, A2·A3은 어휘 오염 때문에 판정이 미완이다. alumina 자체로 좁히는 질의를 더 설계해야 한다.
2. **`reducibility_criteria.md`의 9편 미열람** — Ganduglia-Pirovano 2007, Doornkamp 2000 등 산소공공·MvK 표준 리뷰는 서지만 검증된 상태다. Gate 3의 기준을 스스로 적용하면 **이들을 근거로 한 개념 주장은 전문 확인 전까지 잠정**이다.
3. **연구 표적의 선택** — reducibility / defect-site 반응성 / OH 매개 산소 전달 / 계면 경로 중 무엇을 주제로 할지는 과학적 선택으로 남아 있다(`reducibility_criteria.md` §4.3). v2의 framework는 네 경로를 모두 담을 수 있게 설계되었으므로, 선택을 미루고 지도화를 진행할 수 있다.
