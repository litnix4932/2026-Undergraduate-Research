# Query v1 — 설계·시험·채택 기록
### γ-Al₂O₃ 문헌검색용 검색식과 known-item diagnostic 결과

**선행 문서**: `literature_methodology.md` (방법론 v1) · `seed_set_v2_review.md` (seed 27편) · `reducibility_criteria.md` (Tier A/B/C 기준)
**시험 대상 seed**: KEEP 18 + OPTIONAL 9 = **27편** (core 21 / boundary 6)
**검색 엔진**: OpenAlex `filter=title_and_abstract.search:` (필드 제한 Boolean)
**진단 결과 전체**: `known_item_diagnostic.csv`

### 표기 규약

| 표기 | 의미 |
|---|---|
| **[측정]** | 이번 시험에서 실제로 측정된 값 |
| **[판단]** | Claude의 판단 |

---

## 0. 설계 전제를 뒤집은 관측 — OpenAlex abstract 보유율

query를 쓰기 전에 검색 대상 텍스트가 실제로 존재하는지부터 측정했다.

**[측정] seed 27편**: OpenAlex 레코드는 27/27 존재하나 **abstract는 12/27에만 존재**.

**[측정] 코퍼스 표본 600편** (제목에 γ-Al₂O₃ 표기를 포함하는 문헌):

| 출판사 | abstract 보유율 | 표본 편수 |
|---|---|---|
| **Elsevier BV** | **2.6%** | **422** |
| American Chemical Society | 100.0% | 96 |
| Springer Science+Business Media | 4.8% | 21 |
| Royal Society of Chemistry | 100.0% | 16 |
| Wiley | 93.8% | 16 |
| **전체** | **27.2%** | **600** |

연도별로도 1970년대 20.8% · 2000년대 21.1% · 2010년대 28.3%로 **구 문헌 문제가 아니다.**

**[판단] 이것이 본 분야 검색 설계의 1차 제약이다.** γ-Al₂O₃ 문헌의 중심 저널은 거의 전부 Elsevier다(Journal of Catalysis, Applied Catalysis A/B, Catalysis Today, Surface Science, Journal of Molecular Catalysis). 그런데 OpenAlex에서 그 abstract를 볼 수 없으므로, **이 분야에서 abstract 기반 Boolean 검색은 코퍼스의 약 73%에 대해 제목만 긁는 검색으로 퇴화한다.** 제목은 짧으므로 facet을 여러 개 AND로 묶는 설계는 구조적으로 실패한다 — §2의 측정이 이를 그대로 보여준다.

이 관측은 `seed_set_analysis.md`에서 인용한 Culbert 2025의 "OpenAlex가 abstract를 더 적게 수집한다"는 보고가 **본 분야에서 얼마나 치명적인지를 정량화**한 것이다.

---

## 1. Facet 정의

### 1.1 4-facet 구조

| Facet | 역할 | 비고 |
|---|---|---|
| **A. Material** | 대상 물질 | 두 형태 — `A_strict`(γ 표기 요구) / `A_broad`(alumina·Al₂O₃ 포함) |
| **B. Treatment** | 합성·후처리 조건 | §2의 측정 결과 **검색식에서 제외**하고 screening/추출 단계로 이전 |
| **C. Phenomenon** | 네 현상의 분류축 | C1 reducibility / C2 defect-site 반응성 / C3 OH 매개 / C4 계면 |
| **C5. Probe** | 측정 수단 | 선택적 — 포함 시 recall +1, 결과 +21% |

**현상 facet을 4분기로 둔 이유 [판단]**: `reducibility_criteria.md` §4.3에서 네 현상이 서로 다른 것으로 분리되었고, 프로젝트 원칙이 "결론을 미리 정하지 않는다"이므로 **어느 현상을 연구할지를 query로 미리 결정하지 않고 분류축으로 넣어 증거 분포가 결과로 나오게** 했다.

### 1.2 Facet 어휘 (최종)

```
A_strict = ("gamma-alumina" OR "γ-Al2O3" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina")

A_broad  = A_strict 에 OR "alumina" OR "Al2O3" 추가

B        = (calcination OR calcined OR dehydroxylation OR dehydration OR "thermal treatment"
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

C_ALL = (C1 OR C2 OR C3 OR C4)
C_ALL+P = (C1 OR C2 OR C3 OR C4 OR C5)
```

굵은 변경점(라운드 1 → 2): C1에 `F center`·`oxygen exchange`·`oxygen mobility` 추가, C2에 `surface site`·`acid site`·`surface model` 추가, C3에 **`water-gas conversion`**·**`dehydroxylation`**·`dehydration` 추가. 각 추가의 근거는 §3의 미검출 진단이다.

---

## 2. Query 변이별 측정 결과 (recall / precision trade-off)

**[측정]** 각 변이의 전체 결과 수와 seed 검출 수. seed 검출 판정은 `filter=title_and_abstract.search:<query>,openalex_id:<seed id>`의 결과 수가 1인지로 확인했다(정확 판정, 페이징 불필요).

| Query | 구성 | 결과 수 | seed 전체 | **core 21** | boundary 6 |
|---|---|---|---|---|---|
| Q1 | A_strict AND B AND C_ALL | 3,852 | 4/27 | **4/21** | 0/6 |
| Q3 | A_strict AND C_ALL | 4,873 | 6/27 | **6/21** | 0/6 |
| **Q11** | A_strict AND C_ALL(fixed) | **5,758** | 6/27 | **6/21** | 0/6 |
| Q5 | A_strict 단독 | 18,487 | 7/27 | 7/21 | 0/6 |
| Q2 | A_broad AND B AND C_ALL | 52,397 | 12/27 | 9/21 | 3/6 |
| Q9 | A_broad AND B AND C_ALL(fixed) | 56,350 | 14/27 | 11/21 | 3/6 |
| Q4 | A_broad AND C_ALL | 61,985 | 21/27 | 16/21 | 5/6 |
| **Q6** | A_broad AND C_ALL(fixed) | **67,886** | 25/27 | **19/21** | 6/6 |
| Q8 | A_strict OR (A_broad AND C_ALL fixed) | 80,615 | 26/27 | 20/21 | 6/6 |
| Q7 | A_broad AND C_ALL+P | 82,261 | 26/27 | 20/21 | 6/6 |
| **Q10** | A_strict OR (A_broad AND C_ALL+P) | **93,857** | **27/27** | **21/21** | 6/6 |

### 2.1 측정에서 바로 읽히는 세 가지

**① γ 표기를 query에 요구하면 core seed의 71%를 잃는다 [측정]**
`A_strict`를 쓰는 모든 변이(Q1·Q3·Q11·Q5)는 core 21편 중 **4–7편**만 검출한다. 물질 facet 단독(Q5)으로도 7/21이다. 즉 **phenomenon facet이 아니라 material facet이 지배적 병목**이다. 대부분의 관련 논문은 검색 가능한 텍스트(대개 제목)에서 자신을 "alumina" 또는 "Al₂O₃"로만 부른다.
→ **[판단] γ상 지정은 검색식이 아니라 screening 기준으로 옮겨야 한다.** `seed_set_analysis.md` §8의 추출 항목에 "γ상 확인 여부와 그 근거" 필드를 이미 만들어 둔 것이 여기서 쓰인다.

**② Treatment facet은 비용 대비 손실이 크다 [측정]**
Q6(A_broad AND C) → Q9(A_broad AND B AND C): 결과 수는 67,886 → 56,350으로 **17%만 줄고**, core seed 검출은 19/21 → **11/21로 급감**한다.
→ **[판단] B facet을 검색식에서 제외한다.** 처리 조건은 제목·초록에 거의 등장하지 않고 본문 Experimental에 있으므로, 검색이 아니라 **추출 단계의 필드**로 다루는 것이 옳다.

**③ 27/27 recall의 가격은 93,857건이다 [측정]**
core 6/21(5,758건) → core 21/21(93,857건). seed 검출을 6에서 21로 올리는 데 결과 수가 **16배** 늘어난다. 이 분야에서 **단일 Boolean query로 쓸 만한 precision과 known-item recall을 동시에 달성하는 것은 불가능하다.**

---

## 3. Known-item diagnostic — 미검출 원인별 진단

정량 threshold는 사용하지 않았다(`literature_methodology.md` 결정 ④). seed 개별로 원인코드와 조치를 기록했다. 전체는 `known_item_diagnostic.csv`.

### 3.1 라운드 진행

| 라운드 | query | core 검출 | 조치 |
|---|---|---|---|
| R1 | Q4 (A_broad AND C_ALL) | 16/21 | 미검출 5편 원인 분석 |
| R2 | Q6 (C 어휘 교정) | 19/21 | TERM·LOGIC 3편 해결 |
| R3 | Q7 (+ probe facet) | 20/21 | Morterra1996 해결 (결과 +21%) |
| 최종 | Q10 (union) | 21/21 | Prins2020 해결 (물질어 단독 분기) |

### 3.2 원인코드별 진단 [측정 + 판단]

| seed | 원인코드 | 진단 | 조치 |
|---|---|---|---|
| **Amenomiya1978** | **TERM** | 제목이 "Water-gas **conversion** on alumina" — C3는 `water-gas shift`만 보유. **근접 어휘 변이 누락** | C3에 `water-gas conversion` 추가 → 검출 |
| **Knozinger1978** | **TERM** | "Surface **Models** and Characterization of Surface **Sites**" — C2에 해당 어휘 부재 | C2에 `surface site`·`acid site`·`surface model` 추가 → 검출 |
| **IngramJones1996** | **LOGIC** | `dehydroxylation`을 Treatment facet(B)에만 배치 → 2-facet 질의(A AND C)에서 탈락. **facet 배정 오류** | `dehydroxylation`·`dehydration`을 C3에도 중복 배치 → 검출 |
| **Morterra1996** | **TERM+FIELD** | abstract 없음 + 제목 어휘가 `surface chemistry`/`vibrational spectroscopy` → phenomenon facet 밖 | probe facet(C5) 포함 시에만 검출. 결과 +21% 비용 |
| **Prins2020** | **FIELD** | 제목이 "On the structure of γ-Al₂O₃"**뿐**이고 abstract 없음 → 내용어가 `structure` 하나. **어떤 phenomenon facet으로도 도달 불가** | query로 해결 불가. 물질어 단독 분기(A_strict) 또는 **citation chasing 전담** |
| Shablonin2020 | **의도적 비표적** | α-Al₂O₃ 중성자 조사손상 — precision 탐침용 boundary seed | 검출되지 않는 것이 정상 동작 |

**[판단] 세 가지 교훈**
1. **TERM 오류 2건은 모두 "근접 변이"였다** — `shift` vs `conversion`, `defect site` vs `surface site`. 동의어 수확을 할 때 개념어의 **표현 변이**까지 열거해야 한다는 뜻이다.
2. **LOGIC 오류 1건은 facet 배정 문제였다** — 한 용어가 두 facet에 속할 수 있다(dehydroxylation = 처리 + OH 현상). facet은 배타적 분할이 아니다.
3. **FIELD 오류는 교정 불가다** — Prins2020처럼 제목이 짧고 abstract가 없으면 검색으로 도달할 수 없다. 이것이 §0의 abstract 제약이 구체적으로 드러난 사례이고, **citation chasing이 보조가 아니라 recall의 주 담당자여야 하는 직접적 근거**다.

### 3.3 중단 판정

`literature_methodology.md` §4.5의 pragmatic stopping criterion을 적용한다.

> **[판단] R3에서 중단한다.** 근거: (i) 모든 미검출 seed에 원인코드와 조치가 기록되었다(§3.2). (ii) R2 → R3의 한계 수확은 **core seed +1편(19→20)에 결과 수 +14,375건(+21%)**으로, 추가 어휘 투입의 수확이 급격히 떨어졌다. (iii) 남은 1편(Prins2020)의 원인은 TERM·LOGIC이 아니라 FIELD이므로 **query 수정으로 해결될 수 없다.**
> 이 중단은 **문헌의 완전성을 보장하지 않는다.** 추가 iterative search의 한계 수확에 근거한 실용적 판단일 뿐이다.

---

## 4. 채택 query — 2-tier 설계

**[판단] 단일 query를 고르지 않고 두 층으로 나눈다.** §2.1-③에서 측정된 trade-off가 단일 선택을 허용하지 않기 때문이다.

### Tier 1 — Core retrieval set (전수 title/abstract screening 대상)

```
filter=title_and_abstract.search:
  ("gamma-alumina" OR "γ-Al2O3" OR "gamma-Al2O3" OR "g-Al2O3" OR "transition alumina")
  AND (C1 OR C2 OR C3 OR C4)
```
**= Q11. [측정] 5,758건, core seed 6/21.**
- 역할: **재현 가능하고 전수 screening이 가능한 기준 집합.** 1인 연구가 제목 수준에서 실제로 훑을 수 있는 규모다.
- 한계: core seed의 71%를 놓친다. 이 집합만으로는 **절대 충분하지 않다**는 것이 측정으로 확인되었다.

### Tier 2 — Recall 담당 (Tier 1으로 못 메우는 부분)

| 수단 | 근거 |
|---|---|
| **① Citation chasing (주 담당)** | §3.2의 FIELD 오류 — query로 도달 불가한 문헌이 실재한다. `literature_methodology.md` §4.4에서 이미 필수로 규정 |
| **② 현상별 분할 검색** | A_strict AND Cn 각각: **[측정]** C1 reducibility 3,482 · C3 OH 매개 1,675 · C2 defect 반응성 1,195 · C4 계면 539건. 현상별로 나누면 각 집합이 전수 screening 가능한 규모가 된다 |
| **③ WoS / Scopus 보강 (필수로 격상)** | §0 — Elsevier abstract가 OpenAlex에 없다. 구독 DB는 그것을 보유하므로, **abstract 기반 screening을 하려면 보강이 선택이 아니라 필수**다 |
| ④ A_broad 전수 미사용 | Q10의 93,857건은 1인 연구가 screening할 수 없다. 기록으로만 남기고 실행하지 않는다 |

### 4.1 현상별 분포 [측정]

| 현상 | A_strict AND Cn | 비고 |
|---|---|---|
| C1 reducibility | **3,482** | 가장 큼 — 단 `oxygen storage`·`18O` 등이 ceria 문맥을 끌어옴 |
| C3 OH 매개 | 1,675 | |
| C2 defect-site 반응성 | 1,195 | |
| C4 계면 | 539 | 가장 작음 |

**[판단] 이 분포 자체는 "어느 현상에 문헌이 많은가"의 1차 근사일 뿐 증거 강도가 아니다.** C1이 가장 크지만 §5의 Tier A 시험이 보여주듯 그 안에 Tier A 증거는 희소하다.

---

## 5. Tier A 표적 어휘의 생산성 시험

`reducibility_criteria.md` §6.1의 표적을 실제 query로 돌려 **문헌이 희소한 것인지 검색이 실패한 것인지** 판정했다.

| 표적 | query 요지 | 결과 수 | 상위 결과의 성격 [측정] | 판정 [판단] |
|---|---|---|---|---|
| **A1** H₂O 정량 | alumina AND (water formation OR H₂O evolution OR MS) AND TPR | **36** | 전부 담지금속계(MoNi/γ-Al₂O₃, Fe-Cu, Ni-Al₂O₃ 등) — 맨 alumina 아님 | **문헌 희소 확정.** Tier A1을 만족하는 γ-Al₂O₃ 문헌은 사실상 없다 |
| **A2** 재산화·OSC | alumina AND (reoxidation OR oxygen uptake OR OSC) | 1,302 | 상위가 ceria·Cu·Pd·Mn 계 — `oxygen storage capacity`가 ceria 문맥을 끌어옴 | **검색어 오염.** alumina 자체 측정으로 좁히려면 추가 제한 필요 |
| **A3** 결함상태 분광 | alumina AND (defect state OR mid-gap OR F center OR XANES OR EPR) | 647 | 상위가 담지된 Au·V·Cu의 XANES — **alumina의** 결함상태가 아님 | **문헌 희소 + 어휘 오염.** `seed_set_analysis.md` §4.3의 관찰을 재확인 |
| **A4** 동위원소·MvK | alumina AND (18O OR isotopic labelling OR MvK) | 429 | **1993 "¹⁸O/SIMS characterization of the growth mechanism of doped and undoped α-Al₂O₃" (Oxidation of Metals)** 등 | **신규 커뮤니티 발견 — 아래 §5.1** |
| ① 계면 경로 | alumina AND (metal/oxide interface OR interface oxygen OR perimeter site) | 326 | 양극산화 alumina 세공 배열(무관) + "Metal deposits on well-ordered oxide films", "Interaction of nanostructured metal overlayers with oxide surfaces" (Surf. Sci. Rep.) | **모델 표면과학 커뮤니티**가 이 영역을 담당 |
| ③ 도핑 | (doped alumina OR cation substitution) AND (oxygen vacancy OR reducibility) | 170 | 세라믹·유전체 문헌 위주 | 생산성 낮음 |

### 5.1 새로 발견한 커뮤니티 — 고온 산화/산화피막 분야 [판단]

A4 표적에서 **¹⁸O/SIMS로 α-Al₂O₃ 피막의 성장 기구를 추적한 문헌**(Oxidation of Metals 저널)이 나왔다. 이 분야는 금속의 고온 산화로 생기는 alumina **scale**의 산소 수송을 ¹⁸O 추적자로 수십 년간 연구해 왔다. 즉 **"alumina에서 산소가 어떻게 움직이는가"를 가장 직접적으로 측정해 온 커뮤니티가 촉매 분야 밖에 존재한다.**

이것은 `seed_set_analysis.md` §4.3(산소공공 분광은 핵재료·광학 커뮤니티에 있다)과 `reducibility_criteria.md`(금속공학 Ostrovski2010)에 이어 **세 번째로 확인되는 같은 패턴**이다 — γ-Al₂O₃의 산소 거동에 관한 증거는 촉매 문헌이 아니라 인접 커뮤니티에 축적되어 있다.

→ **다음 단계의 우선 탐색 대상**: `Oxidation of Metals`, `Corrosion Science`, `Acta Materialia` 계열에서 alumina scale의 ¹⁸O 추적·산소 수송 문헌. 단 이들은 α상·피막이므로 γ상 분말로의 전이 가능성은 별도 평가가 필요하다.

---

## 6. 보강 경로용 query 변환과 기록 양식

이 환경에서는 WoS·Scopus·SciFinder에 프로그램 접근이 불가하므로, 사용자가 직접 실행할 수 있는 형태로 변환해 둔다. **실행 후 아래 양식을 채워야 결과를 사용할 수 있다**(`literature_methodology.md` §2.4).

### 6.1 Scopus (Advanced search)

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
Scopus의 `TITLE-ABS-KEY`는 **저자 키워드까지** 포함하므로, OpenAlex가 놓친 Elsevier 문헌의 개념어를 포착할 수 있다 — §0의 제약을 메우는 핵심 수단이다 **[판단]**.

### 6.2 Web of Science (Core Collection, Advanced)

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
WoS `TS=`는 절단(`*`)을 지원하므로 `reducib*`·`pentacoordinat*`로 변이를 한 번에 처리한다. OpenAlex는 절단을 지원하지 않아 변이를 전부 열거해야 했다 **[판단]**.

### 6.3 SciFinder / Reaxys

구조·반응 기반 검색이 강점이므로 **전구체·합성 경로**(boehmite, gibbsite, aluminium alkoxide 등)를 구조 질의로 넣고, 위 phenomenon 어휘를 텍스트 질의로 결합한다. `seed_set_analysis.md`의 Baykoucheva 2011 근거대로 CAPLUS는 MEDLINE과 중복이 20–24%에 불과한 **보완재**이므로, 대체가 아니라 추가 수확 목적으로만 쓴다.

### 6.4 PRISMA-S 기록 양식 (실행 시 채울 것)

| 필드 | 값 |
|---|---|
| source / 플랫폼 | (예: Scopus via Elsevier) |
| 검색일 | YYYY-MM-DD |
| 전체 query 문자열 | (복사해 붙일 것 — 요약 금지) |
| 적용 필터 | 문서유형 / 연도 / 언어 |
| 결과 수 | |
| export 파일명·형식 | (예: `scopus_2026-10-02.csv`) |
| 중복 제거 전/후 수 | |
| 비고 | 플랫폼이 query를 자동 변형했다면 그 내용 |

---

## 7. 버전 이력

| 버전 | 변경 | 근거 |
|---|---|---|
| v0.1 | 3-facet(A×B×C) 초안 | `literature_methodology.md` 결정 ③ |
| v0.2 | B facet 제거 | §2.1-② 측정 (core 19→11) |
| v0.3 | C 어휘 교정 (`water-gas conversion`, `surface site`, `dehydroxylation` C3 중복 배치) | §3.2 TERM·LOGIC 진단 |
| **v1.0 (채택)** | **2-tier 설계** — Tier 1 = Q11(5,758건, 전수 screening) / Tier 2 = citation chasing + 현상별 분할 + WoS·Scopus 필수 보강 | §2.1-③ trade-off 측정, §3.2 FIELD 오류 |

**재검토 trigger**: Tier 1 screening에서 포함률이 2% 미만이면 어휘 과다 포함을 의심해 C 어휘를 좁힌다. 반대로 citation chasing에서 Tier 1 미포함 적격 논문이 계속 나오면 Tier 1의 역할을 축소하고 현상별 분할 검색으로 주 경로를 옮긴다.
