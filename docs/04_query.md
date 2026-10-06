# Query v1 — 설계·시험·채택

> **요약**
> - OpenAlex의 Elsevier 초록 보유율이 **2.6%**다. 그래서 이 분야에서 초록 기반 검색은 대부분 **제목 검색**이 된다.
> - query에 γ상 표기를 요구하면 core seed의 71%를 놓친다. Treatment facet을 넣으면 recall이 무너진다.
> - 단일 query로는 precision과 recall을 함께 얻을 수 없다. core seed 6/21이면 5,758건, 21/21이면 93,857건이다.
> - 채택안은 **2-tier**다. **Tier 1**(5,758건)은 전수 screening하고, **Tier 2**는 citation chasing, 현상별 분할 검색, WoS·Scopus 보강으로 recall을 담당한다.
>
> 시험 대상: seed 27편(core 21, boundary 6 — [03_seed_set.md](03_seed_set.md)). 검색 엔진: OpenAlex `filter=title_and_abstract.search:` (필드 제한 Boolean). seed별 결과: [`known_item_diagnostic.csv`](../data/known_item_diagnostic.csv)

---

## 0. 설계 전제를 뒤집은 관측 — OpenAlex 초록 보유율

query를 쓰기 전에, 검색 대상 텍스트가 실제로 있는지부터 쟀다(방법론의 S0.5 단계).

**[측정]** seed 27편: OpenAlex 레코드는 27/27 존재하지만, 초록은 **12/27**에만 있다.

**[측정]** 제목에 γ-Al₂O₃ 표기가 있는 문헌 600편 표본:

| 출판사 | 초록 보유율 | 편수 |
|---|---|---|
| **Elsevier** | **2.6%** | **422** |
| ACS | 100% | 96 |
| Springer | 4.8% | 21 |
| RSC | 100% | 16 |
| Wiley | 93.8% | 16 |
| **전체** | **27.2%** | 600 |

연도별로는 1970년대 20.8%, 2000년대 21.1%, 2010년대 28.3%다. 즉 **오래된 문헌만의 문제가 아니다.**

**[판단]** 이 분야 중심 저널은 거의 전부 Elsevier다(J. Catal., Appl. Catal. A/B, Catal. Today, Surf. Sci., J. Mol. Catal.). 그러니 OpenAlex에서는 코퍼스 약 73%를 **제목만으로** 검색하게 된다. 제목은 짧아서 facet 여러 개를 AND로 묶는 설계는 구조적으로 실패한다. OpenAlex가 초록을 적게 수집한다는 일반 보고[Culbert2025]가 이 분야에서 얼마나 치명적인지 정량화한 결과다.

*표본 caveat*: 이 표본은 "제목에 γ 표기 포함" 조건으로 뽑았다. 그래서 전체 코퍼스의 출판사 분포와 다를 수 있다.

---

## 1. Facet과 어휘

**facet**은 하나의 개념에 해당하는 동의어 묶음이다. 묶음 안은 OR, 묶음 사이는 AND로 결합한다.

| Facet | 역할 |
|---|---|
| A. Material | `A_strict`는 γ 표기를 요구한다. `A_broad`는 alumina·Al₂O₃까지 포함한다 |
| B. Treatment | **검색식에서 제외** (§2). 추출 필드로 이전 |
| C. Phenomenon | C1 reducibility / C2 defect-site 반응성 / C3 OH 매개 / C4 계면 |
| C5. Probe (측정 수단) | 선택. 포함하면 core +1편, 결과 +21% |

현상 facet을 4분기로 둔 이유가 있다 **[판단]**. 어느 현상을 연구할지 query로 미리 정하지 않기 위해서다. 분류축으로 넣으면 증거 분포가 **결과로** 나온다.

```
A_strict = ("gamma-alumina" OR "γ-Al2O3" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina")
A_broad  = A_strict OR "alumina" OR "Al2O3"

B  = (calcination OR calcined OR dehydroxylation OR dehydration OR "thermal treatment"
      OR "heat treatment" OR reduction OR reduced OR "pre-reduction" OR hydrothermal
      OR steam OR vacuum OR pretreatment OR "pre-treatment" OR plasma OR precursor
      OR boehmite OR "sol-gel" OR doping OR doped)

C1 = (reducibility OR reducible OR "oxygen vacancy" OR "oxygen vacancies" OR "lattice oxygen"
      OR "oxygen removal" OR "temperature-programmed reduction" OR "temperature programmed reduction"
      OR "H2-TPR" OR "oxygen storage" OR reoxidation OR "18O" OR "Mars-van Krevelen"
      OR "F center" OR "F centre" OR "colour centre" OR "color center"
      OR "oxygen exchange" OR "oxygen mobility")

C2 = ("Lewis acid" OR "coordinatively unsaturated" OR "penta-coordinated" OR "pentacoordinated"
      OR "five-coordinate" OR "Al(V)" OR tricoordinate OR "tri-coordinated" OR "defect site"
      OR "defect sites" OR heterolytic OR "H2 dissociation" OR "methane activation"
      OR "C-H activation" OR "surface site" OR "surface sites" OR "acid site" OR "acid sites"
      OR "basic site" OR "surface model" OR "surface models" OR "unsaturated site")

C3 = (hydroxyl OR "OH group" OR "OH groups" OR "surface hydroxyl" OR "water gas shift"
      OR "water-gas shift" OR formate OR carboxy OR carbonate OR "water-gas conversion"
      OR "water gas conversion" OR dehydroxylation OR dehydration OR "hydroxyl group"
      OR "hydroxyl groups")

C4 = ("metal-support interaction" OR "metal/oxide interface" OR "metal-oxide interface"
      OR "interface oxygen" OR spillover OR "back-spillover" OR anchoring OR "nucleation site")

C5 = ("27Al" OR "MAS NMR" OR infrared OR FTIR OR DRIFT OR DRIFTS OR EPR OR XANES
      OR "vibrational spectroscopy" OR "temperature-programmed desorption" OR "isotopic exchange")

C_ALL   = (C1 OR C2 OR C3 OR C4)
C_ALL+P = (C1 OR C2 OR C3 OR C4 OR C5)
```

라운드 1 → 2에서 추가한 어휘와 그 근거는 §3에 있다.
- C1: `F center`, `oxygen exchange`, `oxygen mobility`
- C2: `surface site`, `acid site`, `surface model`
- C3: `water-gas conversion`, `dehydroxylation`, `dehydration`

---

## 2. Query 변이별 측정 결과

**[측정]** seed 검출은 `filter=title_and_abstract.search:<query>,openalex_id:<seed id>`의 결과 수가 1인지로 판정했다.

| Query | 구성 | 결과 수 | 전체 27 | **core 21** | boundary 6 |
|---|---|---|---|---|---|
| Q1 | A_strict AND B AND C_ALL | 3,852 | 4 | **4** | 0 |
| Q3 | A_strict AND C_ALL | 4,873 | 6 | **6** | 0 |
| **Q11** | A_strict AND C_ALL (교정) | **5,758** | 6 | **6** | 0 |
| Q5 | A_strict 단독 | 18,487 | 7 | 7 | 0 |
| Q2 | A_broad AND B AND C_ALL | 52,397 | 12 | 9 | 3 |
| Q9 | A_broad AND B AND C_ALL (교정) | 56,350 | 14 | 11 | 3 |
| Q4 | A_broad AND C_ALL | 61,985 | 21 | 16 | 5 |
| **Q6** | A_broad AND C_ALL (교정) | **67,886** | 25 | **19** | 6 |
| Q8 | A_strict OR (A_broad AND C_ALL 교정) | 80,615 | 26 | 20 | 6 |
| Q7 | A_broad AND C_ALL+P | 82,261 | 26 | 20 | 6 |
| **Q10** | A_strict OR (A_broad AND C_ALL+P) | **93,857** | **27** | **21** | 6 |

**측정에서 바로 읽히는 것**
1. **γ 표기를 요구하면 core seed의 71%를 잃는다.** A_strict를 쓰는 변이는 모두 core 4–7편만 찾는다. 물질 facet 단독(Q5)도 7/21이다. 즉 병목은 현상 facet이 아니라 **물질 facet**이다. 대부분의 논문은 제목에서 자신을 그냥 "alumina"로 부른다. → **[판단]** γ상 판정은 screening 기준으로 옮긴다.
2. **Treatment facet은 손해다.** Q6 → Q9에서 결과는 17%만 줄지만(67,886 → 56,350), core 검출은 19 → **11**로 무너진다. 처리 조건은 본문 Experimental에 있기 때문이다. → **[판단]** 검색식에서 빼고 추출 필드로 다룬다.
3. **21/21 recall의 대가는 93,857건이다.** core 6 → 21편을 얻으려면 결과가 16배 늘어난다. 단일 Boolean query로는 쓸 만한 precision과 known-item recall을 동시에 얻을 수 없다.

---

## 3. Known-item 진단

정량 threshold는 쓰지 않았다. seed마다 원인 코드(정의는 [01_methodology.md D4](01_methodology.md#d4-완전성-평가와-중단))를 기록했다.

| 라운드 | Query | core 검출 | 조치 |
|---|---|---|---|
| R1 | Q4 | 16/21 | 미검출 5편 원인 분석 |
| R2 | Q6 | 19/21 | TERM·LOGIC 3편 해결 |
| R3 | Q7 | 20/21 | Morterra1996 해결 (결과 +21%) |
| 최종 | Q10 | 21/21 | Prins2020 해결 (물질어 단독 분기) |

| Seed | 원인 | 진단 | 조치 |
|---|---|---|---|
| Amenomiya 1978 | TERM | 제목이 "water-gas **conversion**"인데 어휘에는 "shift"만 있었다 | `water-gas conversion` 추가 |
| Knözinger 1978 | TERM | 제목이 "Surface **Models**… Surface **Sites**" | `surface site`, `acid site`, `surface model` 추가 |
| Ingram-Jones 1996 | LOGIC | `dehydroxylation`을 Treatment facet에만 두어 A AND C 질의에서 탈락 | C3에도 중복 배치 |
| Morterra 1996 | TERM+FIELD | 초록 없음 + 제목이 측정 수단 어휘 | probe facet(C5)으로만 검출 |
| **Prins 2020** | **FIELD** | 제목이 "On the structure of γ-Al₂O₃"**뿐**이고 초록이 없다 | **어떤 query로도 도달 불가** → citation chasing 전담 |
| Shablonin (boundary) | 비표적 | α상 조사손상 문헌 | 검출되지 않는 것이 정상 |

**교훈 [판단]**
- TERM 오류 2건은 모두 **근접 표현 변이**였다(shift vs conversion, defect site vs surface site).
- facet은 배타적 분할이 아니다.
- **FIELD 오류는 query로 교정할 수 없다.** 이것이 citation chasing을 보조가 아니라 **recall의 주 담당**으로 두는 직접 근거다.

**중단 판정 (R3) [판단].** 근거는 세 가지다.
1. 모든 미검출 seed에 원인과 조치가 기록되었다.
2. R2 → R3의 한계 수확이 core +1편에 결과 +14,375건(+21%)으로 급감했다.
3. 남은 1편은 FIELD 원인이라 query로 해결할 수 없다.

이 중단은 완전성을 보장하지 않는다.

---

## 4. 채택 — 2-tier 설계

### Tier 1 — 전수 screening 대상

```
filter=title_and_abstract.search:
  ("gamma-alumina" OR "γ-Al2O3" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina")
  AND (C1 OR C2 OR C3 OR C4)
```
= **Q11. 5,758건, core 6/21.** 재현 가능하고, 1인이 제목 수준에서 실제로 훑을 수 있는 규모다. 단 core의 71%를 놓치므로 **이것만으로는 절대 충분하지 않다.**

### Tier 2 — recall 담당

| 수단 | 근거 |
|---|---|
| ① **Citation chasing (주 담당)** | query로 도달할 수 없는 문헌이 실재한다 (FIELD) |
| ② 현상별 분할 검색 (A_strict AND Cn) | 각 집합이 전수 screening 가능한 규모다 (아래) |
| ③ **WoS·Scopus 보강 (필수)** | Elsevier 초록을 보유하므로 §0의 공백을 메운다 |
| ④ A_broad 전수 (Q10) | 93,857건은 1인이 screening할 수 없다. 기록만 하고 실행하지 않는다 |

**[측정] 현상별 분포 (A_strict AND Cn)**

| C1 reducibility | C3 OH 매개 | C2 defect 반응성 | C4 계면 |
|---|---|---|---|
| 3,482 | 1,675 | 1,195 | 539 |

**[판단]** 이 분포는 "어느 현상에 문헌이 많은가"의 1차 근사일 뿐, 증거 강도가 아니다. C1은 `oxygen storage`, `18O` 같은 어휘가 ceria 문맥을 끌어와 부풀려졌다. 그 안의 Tier A 증거는 희소하다(§5).

---

## 5. Tier A 표적 어휘의 생산성 시험

[Tier A 기준](02_evidence_framework.md#7-증거-등급-tier-abc)을 실제 query로 돌렸다. 목적은 **문헌이 희소한 것인지, 검색이 실패한 것인지** 판정하는 것이다.

| 표적 | Query 요지 | 결과 | 상위 결과 [측정] | 판정 [판단] |
|---|---|---|---|---|
| A1 H₂O 정량 | alumina AND (water formation OR H₂O evolution OR MS) AND TPR | **36** | 전부 담지금속계(MoNi/γ-Al₂O₃, Fe-Cu, Ni-Al₂O₃ 등) | **문헌 희소 확정** |
| A2 재산화·OSC | alumina AND (reoxidation OR oxygen uptake OR OSC) | 1,302 | ceria·Cu·Pd·Mn계 | **어휘 오염** — alumina 자체로 좁혀야 함 |
| A3 결함상태 분광 | alumina AND (defect state OR mid-gap OR F center OR XANES OR EPR) | 647 | 담지 Au·V·Cu의 XANES | 희소 + 어휘 오염 |
| A4 동위원소·MvK | alumina AND (18O OR isotopic labelling OR MvK) | 429 | ¹⁸O/SIMS로 α-Al₂O₃ 피막 성장을 추적한 연구(*Oxidation of Metals*, 1993) 등 | **인접 커뮤니티 발견** |
| 계면 경로 | alumina AND (metal/oxide interface OR interface oxygen OR perimeter site) | 326 | 양극산화 alumina(무관) + 모델 표면과학 리뷰(Surf. Sci. Rep.) | 모델 표면과학 커뮤니티 담당 |
| 도핑 | (doped alumina OR cation substitution) AND (oxygen vacancy OR reducibility) | 170 | 세라믹·유전체 | 생산성 낮음 |

**고온산화·산화피막 커뮤니티 [판단].** 이 분야는 금속이 고온에서 산화될 때 생기는 alumina **scale**(산화피막)의 산소 수송을, ¹⁸O 추적자와 **SIMS**(이차이온질량분석, 깊이별 동위원소 분포 측정)로 수십 년간 연구해 왔다. 즉 "alumina에서 산소가 어떻게 움직이는가"를 가장 직접 재온 커뮤니티가 촉매 분야 밖에 있다. 다음 탐색 대상은 *Oxidation of Metals*, *Corrosion Science*, *Acta Materialia* 계열이다. 단 α상 피막이므로 γ상 분말로 전이할 수 있는지는 따로 평가해야 한다.

---

## 6. 보강 경로용 query 변환

이 환경에서는 WoS·Scopus·SciFinder에 프로그램으로 접근할 수 없다. 그래서 사용자가 직접 실행할 형태로 둔다. **실행 후 아래 기록 양식을 채워야 결과를 쓸 수 있다.**

**Scopus (Advanced search).** `TITLE-ABS-KEY`는 저자 키워드까지 검색한다.
```
TITLE-ABS-KEY(("gamma-alumina" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina"))
AND TITLE-ABS-KEY((reducibility OR reducible OR "oxygen vacancy" OR "lattice oxygen"
   OR "oxygen removal" OR "temperature programmed reduction" OR "oxygen storage"
   OR reoxidation OR "oxygen exchange" OR "oxygen mobility"
   OR "Lewis acid" OR "coordinatively unsaturated" OR "penta-coordinated" OR "pentacoordinated"
   OR "defect site" OR heterolytic OR "surface site" OR "acid site"
   OR hydroxyl OR "surface hydroxyl" OR "water gas shift" OR "water-gas conversion"
   OR dehydroxylation OR formate OR carbonate
   OR "metal support interaction" OR "interface oxygen" OR spillover OR anchoring))
```

**Web of Science (Core Collection, Advanced).** `TS=`는 절단(`*`)을 지원하므로 변이를 한 번에 처리한다.
```
TS=(("gamma-alumina" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina")
AND (reducib* OR "oxygen vacanc*" OR "lattice oxygen" OR "oxygen removal"
   OR "temperature programmed reduction" OR "oxygen storage" OR reoxidation
   OR "oxygen exchange" OR "oxygen mobility" OR "Lewis acid"
   OR "coordinatively unsaturated" OR "penta-coordinated" OR "pentacoordinat*"
   OR "defect site*" OR heterolytic OR "surface site*" OR "acid site*"
   OR hydroxyl* OR "water gas shift" OR "water-gas conversion" OR dehydroxylation
   OR formate OR carbonate OR "metal support interaction" OR "interface oxygen"
   OR spillover OR anchoring))
```

**SciFinder / Reaxys.** 이 DB들은 화학 구조·반응 검색이 강점이다. 전구체·합성 경로(boehmite, gibbsite, aluminium alkoxide)는 구조 질의로 넣고, 현상 어휘는 텍스트 질의로 결합한다. 대체재가 아니라 보완재로 쓴다.

**PRISMA-S 기록 양식**

| 필드 | 값 |
|---|---|
| source / 플랫폼 | (예: Scopus via Elsevier) |
| 검색일 | YYYY-MM-DD |
| 전체 query 문자열 | 요약 금지, 그대로 붙일 것 |
| 적용 필터 | 문서유형 / 연도 / 언어 |
| 결과 수 | |
| export 파일명·형식 | (예: `scopus_2026-10-02.csv`) |
| 중복 제거 전/후 수 | |
| 비고 | 플랫폼이 query를 자동 변형했다면 그 내용 |

---

## 7. 버전 이력과 재검토 조건

| 버전 | 변경 | 근거 |
|---|---|---|
| v0.1 | 3-facet (A×B×C) 초안 | 방법론 D3 |
| v0.2 | B facet 제거 | core 19 → 11 |
| v0.3 | C 어휘 교정 | TERM·LOGIC 진단 |
| **v1.0 (채택)** | 2-tier 설계 | 16배 trade-off, FIELD 오류 |

**재검토 조건**
- Tier 1 screening의 포함률이 2% 미만이면 C 어휘가 과다하다고 보고 좁힌다.
- citation chasing에서 Tier 1 밖의 적격 논문이 계속 나오면, 현상별 분할 검색을 주 경로로 옮긴다.
