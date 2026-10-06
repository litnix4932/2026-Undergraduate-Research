# Seed Set v2 — 비판적 재검토
### Ammendola 2011 원문 검증 · Oxygen behavior / Reducibility 보강 · KEEP·OPTIONAL·REMOVE 재분류

**선행 문서**: `seed_set_analysis.md` (v1, 16편) · `literature_methodology.md` (방법론 v1)
**검증**: 본 문서에 등장하는 모든 논문은 Crossref API로 서지 대조 검증 완료 (36/36)
**목표 재확인**: reducible γ-Al₂O₃가 존재함을 **증명하는 것이 아니라**, 편향 없이 조사할 수 있는 검색 query를 검증하기 위한 seed set을 만드는 것.

### 표기 규약

| 표기 | 의미 |
|---|---|
| **[측정]** | 논문이 실제로 측정·계산한 값 |
| **[저자해석]** | 저자가 그 측정으로부터 끌어낸 해석 |
| **[판단]** | Claude의 판단 — 논문의 주장이 아님 |

> ⚠ **본 문서 전체의 규칙**: TCD peak 또는 H₂ consumption 자체를 oxygen removal의 직접 증거로 취급하지 않는다.

---

## 1. Ammendola et al. 2011 원문 검증 — 이번 재검토의 핵심 결과

`10.1016/j.susc.2011.06.018` · Surface Science 605 (2011) 1812–1817 · Ammendola, Barbato, Lisi, Ruoppolo, Russo (CNR / Università di Napoli Federico II)

### 1.1 이 논문이 실제로 한 실험

**[측정]**
- 실험은 **H₂-TPR이 아니라 CO-TPR**이다. 시료: La/γ-Al₂O₃(CK-300, Akzo, 5 wt% La₂O₃ 안정화)와 구형 γ-Al₂O₃(Sasol). 각각 1 wt% Pt/La/γ-Al₂O₃, 8 wt% Cu/γ-Al₂O₃ 촉매도 함께. 모든 시료는 측정 전 **공기 중 800 °C에서 3 h** 처리.
- 승온 10 °C/min으로 800 °C까지, CO/N₂ 혼합가스. CO·CO₂·H₂·O₂를 **적외선 검출기(CO, CO₂) + TCD(H₂) + 상자성 셀(O₂)**로 동시 정량.
- **순수 지지체의 결과**: CO 소모가 **약 400 °C에서 시작**, 모든 곡선이 **594 °C**(La/γ-Al₂O₃) 및 **602 °C**(γ-Al₂O₃)에서 최대.
- 정량값 (800 °C에서 100 min 후 적분):

| 시료 | CO 소모 (μmol/g) | CO₂ 생성 (μmol/g) | H₂ 생성 (μmol/g) | H₂/CO₂ |
|---|---|---|---|---|
| La/γ-Al₂O₃ | 191 | 181 | 184 | 1.02 |
| γ-Al₂O₃ | 229 | 216 | 205 | 0.95 |
| 1 wt% Pt/La/γ-Al₂O₃ | 589 | 589 | 424 | 0.80* |
| 8 wt% Cu/γ-Al₂O₃ | 1802 | 1805 | 705 | 0.70* |

  *금속 환원 기여분을 뺀 값. Pt²⁺ 완전환원 상당량 56 μmol/g, Cu 60% 환원 상당량 794 μmol/g.
- **DRIFT**: 소성 시료의 3737 cm⁻¹(bridged OH)·3840 cm⁻¹(linear OH) 밴드가 CO-TPR 후 **크게 감소하고 3840 cm⁻¹는 소멸**. 흡착수(1684)·carbonate(1530) 밴드 소멸, 1590 cm⁻¹ 밴드 출현.
- **TPO(후속 산화)**: CO₂ 주 피크 240 °C(코크 연소로 보기엔 너무 낮음), 550 °C의 매우 작은 피크가 코크 상당(**약 1.6 μmol/g**) — CO 소모량 대비 무시 가능 → **Boudouard 반응 배제**.
- H₂-TPR은 **Pt 촉매 1건에만** 수행되어 Pt 환원량(56 μmol/g) 산정에 쓰였다. **맨 alumina에 대한 H₂-TPR은 이 논문에 없다.**

### 1.2 저자의 해석

**[저자해석]** CO 소모·CO₂·H₂ 생성은 **표면 OH기와 CO 사이의 Water-Gas Shift 반응**으로 귀속된다.
- 두 개의 vicinal linear OH가 축합해 생성된 물이 CO와 반응: `CO + H₂O → CO₂ + H₂` (H₂/CO₂ = 1)
- 고온에서 linear OH가 소진되면 bridged OH가 반응: `CO + OH → CO₂ + ½H₂` (H₂/CO₂ = 0.5)
- 금속(Pt, Cu)이 있으면 금속에 강하게 흡착된 CO의 **spillover**로 이 WGS가 가속된다.
- 결론 원문: *"Pure and La-stabilized γ-Al₂O₃ reacted with CO at T ≥ 400 °C through a WGS reaction involving surface OH groups producing CO₂ and H₂."* 그리고 *"the alumina contribution to CO TPR, a method typically used as a characterisation technique to investigate metal oxide-supported catalysts, was significant. Thus, quantitative results must be carefully analysed by taking into account hydrogen production associated with the WGS reaction."*

### 1.3 판정

**[판단] Jeong 2020 Supplementary Fig. 1의 인용은 그 근거 문헌에 의해 지지되지 않는다.**

| 항목 | Jeong 2020 SI Fig. 1 캡션의 주장 | Ammendola 2011이 실제로 보고한 것 |
|---|---|---|
| 실험 종류 | H₂-TPR | **CO-TPR** (맨 alumina의 H₂-TPR은 없음) |
| 신호 위치 | **267 °C**, 661 °C | CO 소모 개시 ~400 °C, 최대 **594 / 602 °C** |
| 귀속 | weakly coordinated **surface Al의 환원** / strongly coordinated **bulk Al의 환원** | **표면 OH기와 CO의 WGS 반응** (산소원은 OH/H₂O) |
| Al의 환원 언급 | 핵심 주장 | **없음** |
| 논문의 함의 | alumina가 환원된다 | alumina의 **OH 화학이 TPR을 오염**시키므로 보정해야 한다 |

즉 인용 방향이 **반대**다. Ammendola 2011은 "alumina가 환원된다"는 근거가 아니라, **"지지체의 표면 화학 때문에 TPR 정량을 환원으로 읽으면 안 된다"는 경고문**이다. 온도대(594–602 °C vs 267 °C)와 기체(CO vs H₂)도 일치하지 않는다.

SI 참고문헌 2(Zheng et al., Appl. Catal. B 202, 51–63, 2017)는 검증된 제목 기준 **LaFeO₃ 담지 CeO₂ 산소운반체**에 관한 연구로, γ-Al₂O₃의 알루미늄 환원에 대한 근거가 아니다(원문 미열람 — 제목·서지만 확인).

**[판단] 다만 다음은 분명히 구분해야 한다.** 이 판정은 *"γ-Al₂O₃는 환원되지 않는다"*를 증명하지 않는다. 증명하는 것은 **"현재 이 주장이 의지하고 있는 인용이 그 주장을 지지하지 않는다"**는 것뿐이다. 267 °C 피크의 정체는 여전히 열려 있고, 그것을 규명하는 것이 본 연구의 실질적 과제가 되었다.

### 1.4 267 °C 피크에 대해 Ammendola가 실제로 시사하는 바

**[판단]** Ammendola를 읽고 나면 267 °C 피크의 후보 설명이 오히려 늘어난다.
- Jeong 2020의 H₂-TPR 전처리는 **Ar, 250 °C, 2 h**였다. Digne 2004의 DFT 값([Digne2004], 아래 §3)에 따르면 이 온도에서 표면 OH는 상당량 남아 있다 — (110)면은 500–1000 K 구간에서 3.0 OH/nm², (111)면은 1000 K에서도 9.8 OH/nm². 따라서 **267 °C 피크 구간에서 시료는 여전히 OH를 다량 보유한 상태**다.
- TCD는 H₂ 소모와 **H₂O 발생을 구분하지 못한다**(열전도도가 크게 다르므로 물은 오히려 큰 TCD 응답을 준다).
- Ammendola의 WGS는 CO가 환원제였지만, H₂ 분위기에서도 OH 축합에 의한 탈수(dehydroxylation)는 독립적으로 진행된다.

→ 267 °C 피크가 (a) 격자 산소 제거, (b) H₂ 해리·흡착, (c) spillover, (d) 탈수/OH 축합 중 무엇인지는 **이 그림만으로 판별 불가능**하다. §2가 그 판별 설계다.

---

## 2. H₂ 처리에서 관찰되는 현상의 판별 (요청 2)

**[판단]** H₂ 분위기 승온에서 TCD/H₂ 소모 신호를 만들 수 있는 과정은 최소 다섯 가지이고, **그중 산소를 제거하는 것은 하나뿐**이다.

| # | 현상 | 산소 제거? | 남기는 흔적 | 판별 수단 | 관련 seed |
|---|---|---|---|---|---|
| 1 | **격자 산소 제거 (진짜 환원)** | **O** | H₂O 생성, 산소 결손 축적, 재산화 시 O₂ 소모, 질량 감소 | H₂O **정량** + O₂ 재산화 적정 + ¹⁸O 교환 + TGA | Martin1996, Hinuma2020, Carrasco2004, Ostrovski2010 |
| 2 | H₂ heterolytic dissociation (Al–O 쌍) | X | Al–H / O–H 생성, 가역적, site 수에 비례하여 포화 | IR의 Al–H 밴드, 가역성, site 적정 | **Joubert2006**, Wischert2012 |
| 3 | 해리흡착 + spillover | X | 지지체 상 H 축적, 금속 유무에 강하게 의존 | 금속 유/무 대조, 동위원소 추적, back-spillover | **Kramer1979**, Kalamaras2008, Shi2020 |
| 4 | 탈수화 / OH 축합 | X (산소는 H₂O로) | H₂O 발생, OH 밴드 감소, 비가역 | **MS m/z 18 추적**, IR OH 영역, 전처리 온도 의존성 | Knozinger1978, Morterra1996, Digne2004 |
| 5 | OH 기반 WGS·carboxy 경로 (CO 존재 시) | X (산소원은 OH) | CO₂ + H₂ 동시 생성, 화학량비 0.5–1 | CO₂/H₂ 화학량비, DRIFT OH 소모 | **Ammendola2011**, Amenomiya1978, Fottinger2008 |
| 6 | 금속 전구체·잔류물 환원 | X (alumina 아님) | H₂ 소모 | **blank / bare support 대조** | 실험설계 항목 |

**[판단] 최소 판별 조합**: ① H₂ 소모와 **H₂O 생성을 동시에 정량**(MS), ② 1차 TPR 후 **O₂ 재산화**로 결손 산소량 적정, ③ 전처리 온도를 올려(예: 700 °C) OH를 줄인 뒤 피크가 **줄어드는지** 확인, ④ **금속 없는 맨 alumina** 대조. 이 네 가지가 모두 갖춰진 문헌이 있는지가 전면 수집 단계의 핵심 검색 과제다.

---

## 3. Al(V) → oxygen vacancy → reducibility 세 고리의 독립 증거 감사 (요청 3)

각 고리를 **전제하지 않고**, 현재 확보된 근거만으로 평가했다.

| 고리 | 독립 증거 상태 | 근거 |
|---|---|---|
| **① Processing → Al(V) 생성** | ✅ **강함** | [측정] Kwak2007: 21.1 T, 23 kHz에서 Al(V) 1.56 mol%, T₁<8 ms(표면). [측정] Jeong2020: 350 °C H₂ 처리 후 Al(V) 피크 출현. [측정] Liu2021: 합성경로로 Al(V) 풍부 구조. **단 caveat** — Jeong2020의 NMR은 9.4 T, Kwak2007은 21.1 T로, Kwak 자신이 Al(V) 정량이 자장·스피닝 속도에 민감함(23 kHz 1.56% vs 15 kHz 3.3%)을 보였으므로 두 값은 직접 비교 불가. |
| **② Al(V) → oxygen vacancy** | ❌ **독립 증거 없음** | Al(V)는 ²⁷Al NMR로 본 **양이온(Al³⁺)의 배위수 상태**이고, oxygen vacancy는 **O²⁻의 결손**이다. 확보한 어떤 문헌도 "Al(V)를 만들면 산소가 빠진다"를 측정하지 않았다. 오히려 [저자해석] Wischert2012은 반응성 site가 **부분 탈수화(물 제거)**로 생기는 tricoordinate Al(III)이며 (100)면의 Al(V)로는 반응성을 설명할 수 없다고 본다 — 즉 Al 배위수 감소의 원인은 **OH 제거**이고 격자 산소 제거가 아니다. Wang2022는 Al(V)와 "Al₂O₃ 상 산소공공"을 **함께 주장**하지만 둘의 인과를 측정하지 않았다. |
| **③ oxygen vacancy → reducibility** | ◐ **정량 근거는 있으나 방향이 불리** | [계산] Hinuma2020: 접근가능 표면 중 최저 표면 산소공공 생성에너지가 **θ-Al₂O₃ (201̄)에서 5.46 eV**, 비교 대상 β-Ga₂O₃ (101)은 3.04 eV. [계산] Carrasco2004: α-Al₂O₃를 포함한 이온성 산화물의 공공 생성에너지·이동장벽을 Madelung 전위로 설명. [측정] Martin1996: γ-Al₂O₃의 ¹⁸O 교환 최대속도 **620 °C**(CeO₂ 410 °C). [측정] Ostrovski2010: 벌크 alumina 환원은 **탄소열 조건**에서 Al₄C₃와 Al·Al₂O 증기를 생성. → 어느 것도 200–300 °C에서의 산소 제거를 지지하지 않는다. |
| **④ (motivation) 267 °C TCD = 산소 제거** | ❌ **현재 근거 없음** | §1.3 — 인용된 근거가 다른 실험(CO-TPR)·다른 온도(594–602 °C)·다른 귀속(OH의 WGS)이다. |

**[판단] 종합**: 사슬이 **②에서 끊어져 있다.** Al(V)는 잘 측정되고, 산소공공의 비용은 계산으로 높게 나오고, 산소 교환은 고온에서만 일어난다. 그런데 "Al(V)가 곧 산소공공"이라는 연결에는 어느 쪽 방향으로도 측정 근거가 없다. 이 공백이 본 연구가 실제로 조사해야 할 지점이며, seed set은 이 공백을 **메우는 쪽이 아니라 드러내는 쪽**으로 구성되어야 한다.

---

## 4. 독립 검색으로 추가 확보한 [C]·[D] 근거 (요청 1·4)

기존 seed의 citation network와 **분리된** 경로로 OpenAlex를 직접 검색했다(`title_and_abstract.search` + Boolean). 기존 seed를 인용하지도, 기존 seed가 인용하지도 않는 문헌을 의도적으로 노렸다.

### 4.1 검색 축과 성과

| 검색 축 | 질의 요지 | 성과 |
|---|---|---|
| 산소 동위원소 교환 | `(alumina OR "Al2O3") AND ("18O exchange" OR "oxygen isotope exchange")` | Martin1996 재검출(독립 확인). 그 외 대부분 지구화학·운석 문헌 — **촉매 분야에 이 측정이 희소함을 확인** |
| 산소공공 생성에너지 | `("Al2O3" OR alumina) AND ("oxygen vacancy formation energy")` | **Carrasco2004 (PRL)**, **Hinuma2020 (JPCC)** 신규 확보 |
| 맨 지지체 TPR | `(alumina OR "Al2O3") AND ("bare support" OR blank) AND ("H2-TPR")` | 유효 결과 **5건 뿐** — 맨 alumina의 H₂-TPR을 주제로 삼은 문헌이 희소함을 시사 |
| 탈수화·물 탈착 | `(alumina OR "Al2O3") AND (dehydroxylation OR "water desorption") AND (TPD OR TPR)` | 직접 해당 문헌 희소. §2-④의 판별 수단이 문헌에서 잘 쓰이지 않음 |
| OH 기반 WGS | `("water gas shift") AND (alumina) AND (hydroxyl)` | Olympiou2007·Kalamaras2008·Serre1993 확보 |
| spillover | `(alumina) AND ("back-spillover" OR "hydrogen spillover")` | **Kramer1979 독립 재검출**, **Shi2020** 신규 |
| Al(V)↔산소공공 | `(alumina) AND ("penta-coordinated" OR "Al(V)") AND ("oxygen vacancy" OR reducib)` | **Wang2022**, **Ishizaki2003** 신규. 결과 수 자체가 매우 적음 → §3-②의 공백을 독립 검색이 재확인 |
| 환원 열역학 | `("Al2O3") AND ("hydrogen reduction") AND (thermodynamic OR suboxide)` | **Ostrovski2010** 신규. 나머지는 제철·보크사이트 잔류물 문헌 |

**[판단] 이 검색 자체가 하나의 결과다.** "맨 γ-Al₂O₃의 H₂-TPR" 과 "Al(V)와 산소공공의 관계"는 **검색이 잘 안 되는 것이 아니라 문헌이 희소하다.** 반면 "alumina + 산소공공"으로 검색하면 (i) 조사손상된 α상 세라믹, (ii) 산소공공을 CeO₂·TiO₂에서 빌려온 담지촉매 문헌이 결과를 채운다. 이 비대칭을 알고 query를 설계해야 한다.

### 4.2 신규 핵심 후보

| Candidate | Year | Group | Study type | Treatment | 측정된 것 / 주장 | 고유 기여 | Verification |
|---|---|---|---|---|---|---|---|
| **Amenomiya** | 1978 | Amenomiya | exp. (kinetics + IR) | — | **[측정]** alumina 상 water-gas conversion, formate 중간체 | alumina가 **스스로** OH 기반 CO/H₂ 화학을 한다는 기원 문헌. 1970년대 어휘 | `10.1016/0021-9517(78)90207-5` |
| **Kalamaras** | 2008 | Efstathiou (Cyprus) | exp. (operando SSITKA-DRIFTS-MS) | WGS 조건 | **[측정]** Pt/γ-Al₂O₃ WGS의 과도상태 동위원소 추적 | **동위원소로 OH/H 이동을 추적** — TCD로 불가능한 판별의 모범 사례 | `10.1016/j.cattod.2008.06.010` |
| **Hinuma** | 2020 | Hinuma 외 (일본) | computational (DFT + GA) | — | **[계산]** 접근가능 표면 최저 E_Ovac: β-Ga₂O₃ (101) **3.04 eV** vs **θ-Al₂O₃ (201̄) 5.46 eV**; 최안정면 대비 감소분 1.32 / 1.11 eV | **전이 alumina(θ상) 표면**의 산소공공 비용을 정량. γ에 가장 가까운 상에서의 계산 기준 | `10.1021/acs.jpcc.0c00994` |
| **Carrasco** | 2004 | Carrasco, Lopez, Illas | computational (DFT) | — | **[계산]** MgO·CaO·**α-Al₂O₃**·ZnO의 중성 산소공공 생성에너지, 공공–공공 상호작용, 이동장벽을 ionicity·Madelung 전위·격자 완화로 설명 | 산소공공의 **생성 + 확산**을 산화물 계열로 비교하는 독립 기준 | `10.1103/physrevlett.93.225502` |
| **Shi** | 2020 | Shi 외 | exp. | **H₂ / O₂ 플라즈마 처리** | **[측정/저자해석]** H₂ 플라즈마 후 표면 산소공공(SOV) 증가, O₂ 플라즈마 후 OH 증가·SOV 감소; OH가 수소 spillover 촉진 | 처리로 **산소공공을 양방향 조절했다고 주장**하는 드문 사례. 새 처리축(플라즈마) | `10.1021/acscatal.0c03091` |
| **Ostrovski** | 2010 | Ostrovski | exp. (금속공학) | 탄소열 환원 (Ar/He/H₂) | **[측정]** alumina 환원 생성물에 **Al₄C₃**와 **Al·Al₂O 증기**가 포함되고, 반응기 밖에서 Al₄O₄C로 재산화 | **벌크 Al₂O₃를 실제로 환원시키려면 어떤 조건이 필요한지**의 기준선 | `10.1002/srin.201000177` |
| **Wang** | 2022 | Wang 외 | exp. | MOF 유래 합성 + 소성 | **[저자해석]** penta-coordinated Al³⁺ 고정 site + "Al₂O₃ 상 산소공공"과 수소 spillover가 코크 저항에 기여 | **Al(V)·산소공공·spillover를 한 문장에 묶는 주장 패턴**의 대표 사례 → 증거가 아니라 **검증 대상** | `10.1002/aic.17998` |
| Föttinger | 2008 | Rupprechter, Schlögl | exp. (표지 분광) | — | **[측정]** 표지 CO/CO₂ 분광: Pd–alumina의 carbonate는 CO와 지지체 **OH**의 'oxygen down' 반응으로 생성, Pd 상 CO 해리는 배제 | 표지 실험으로 OH 경로를 확정 | `10.1039/b713161e` |
| Serre | 1993 | Maire 외 (Strasbourg) | exp. (CO-TPR) | — | Pt/Al₂O₃·Pt-CeO₂/Al₂O₃의 CO 산화 반응성 | CO-TPR→WGS 귀속의 초기 관측 (Ammendola가 요약 인용) | `10.1006/jcat.1993.1113` |
| Ishizaki | 2003 | Ishizaki 외 | exp. (EPR) | sol–gel | sol–gel alumina 막의 결함 EPR | 조사손상이 아닌 **재료화학 맥락의 EPR** 경로 | `10.1016/s0022-3697(02)00377-3` |
| Haneda | 2000 | Duprez 외 | exp. | — | **[측정]** Ga₂O₃–Al₂O₃ 상 OH와 CO 반응으로 수소 생성 | OH→H₂의 직접 증거이나 혼합 산화물 | `10.1246/cl.2000.974` |

모든 DOI는 Crossref 대조 검증을 통과했으며 `seed_set_v2.csv`의 `doi` 열과 일치한다.

---

## 5. 전체 재분류 — KEEP / OPTIONAL / REMOVE

기존 16편과 신규 후보를 **동일 기준**으로 평가했다. 기준은 하나다: **known-item testing에서 이 논문이 다른 논문으로 대체되지 않는 고유 진단 역할을 갖는가.**
전체 표(역할·고유 기여·사유·DOI)는 `seed_set_v2.csv`.

### 5.1 KEEP — 18편

| # | 논문 | 고리 | 고유 진단 역할 |
|---|---|---|---|
| 1 | Kwak 2007 | [A]→[B] | Al(V) 표면 국재의 1차 측정(T₁<8 ms, BaO 1:1) |
| 2 | Prins 2020 | [B] | 양이온 공공 ≠ 산소 공공 — 용어 혼동 차단 |
| 3 | Jeong 2020 | [A]→[B], [D] 주장 | motivation + **인용이 주장을 지지하지 않는** 검증 사례 |
| 4 | Knözinger 1978 | [B] | 검색 어휘의 정의 출처 |
| 5 | Morterra 1996 | [B]→[C] 경계 | IR 축 + "전이 alumina의 CO 반응은 T≥400 °C에서 시작" |
| 6 | Digne 2004 | [A]→[B] 계산 | OH 피복률의 정량 기준(처리온도 ↔ OH 밀도) |
| 7 | **Joubert 2006** | **[D′]** | H₂ 소모 ≠ 산소 제거의 정량 증거(25 °C, 0.043–0.069 site/nm²) |
| 8 | **Wischert 2012** | **[B]→[D′]** | Al(V) 전제의 반증(반응성 site는 Al(III), 원인은 탈수화) |
| 9 | **Martin 1996** | **[C]** | 격자 산소 이동성의 유일한 직접 실험(620 °C) |
| 10 | **Ammendola 2011** | **[D] 출처** | 인용된 근거의 실제 내용 — WGS, Al 환원 아님 |
| 11 | Kramer 1979 | [D′] | spillover에 의한 H 축적 |
| 12 | **Amenomiya 1978** | [C]/[D′] 기원 | alumina 자체의 water-gas 전환 |
| 13 | **Kalamaras 2008** | **[D′]** | 동위원소 operando로 OH/H 이동 추적 |
| 14 | **Hinuma 2020** | **[C]** 계산 | θ-Al₂O₃ 표면 산소공공 5.46 eV |
| 15 | **Carrasco 2004** | **[C]** 계산 | 산화물 간 공공 생성·이동 비교(α-Al₂O₃ 포함) |
| 16 | **Shi 2020** | **[A]→[C]** 주장 | 플라즈마로 SOV를 양방향 조절했다는 주장 |
| 17 | **Ostrovski 2010** | **[D]** 기준 | 벌크 환원의 실제 조건(Al₄C₃, Al·Al₂O 증기) |
| 18 | **Wang 2022** | claim-pattern | Al(V)+산소공공+spillover 동시 주장 — 검증 대상 |

굵게 표시한 11편이 [C]·[D]·[D′] 보강분이다. v1에서 이 영역은 3편(Martin1996, Ammendola2011, Kramer1979 + Joubert·Wischert)뿐이었다.

### 5.2 OPTIONAL — 9편

| 논문 | 유보 사유 |
|---|---|
| **Choi 2022** (초기 4편) | Jeong2020과 **동일 그룹**이고 [C]·[D] 기여가 0. 다만 `hydrothermal pre-treatment`·`aging`·`durability` 어휘는 고유해, 그 어휘 영역의 recall을 시험하려면 유지 가치가 있다 |
| Chen 1992 | Al 배위↔산성도의 선행 근거이나 Knözinger1978·Morterra1996과 부분 중복 |
| Ingram-Jones 1996 | 전구체×가열방식 축. [A]→[B]가 이미 과포화 |
| Liu 2021 | 합성경로로 Al(V) 생성. [A]→[B] 과포화, 합성 어휘는 고유 |
| Ishizaki 2003 | 비(非)조사 EPR 경로이나 시료가 sol–gel **박막** |
| Föttinger 2008 | 표지 실험은 가치 있으나 Ammendola·Kalamaras와 메시지 중복 |
| Serre 1993 | 내용이 Ammendola 2011에 요약되어 중복 |
| Haneda 2000 | OH→H₂ 직접 증거이나 Ga₂O₃–Al₂O₃ 혼합 산화물 |
| Shablonin 2021 | α상·조사손상 — query **precision 탐침**으로만 |

### 5.3 REMOVE — 6편

| 논문 | 제거 사유 |
|---|---|
| **Kwak 2008** (v1 S16) | [A]→[B] 과포화 + PNNL 그룹 중복. 고온 상전이 질문은 [C]·[D]보다 후순위 |
| Kwak 2009 (Science) | Kwak2007과 개념·그룹 중복 |
| Arrouvel 2004 | Digne2004와 동일 그룹·방법·메시지 |
| Dropsch 1997 | alumina-OH 메시지를 Ammendola·Föttinger가 더 직접 전달 |
| Olympiou 2007 | 동일 그룹의 Kalamaras2008(operando 동위원소)로 대체 |
| Iordan 2004 | Ammendola의 기전 논의에 흡수 |

**[판단] 초기 4편 중 1편(Choi 2022)이 KEEP에서 내려왔다.** 나쁜 논문이기 때문이 아니라, 같은 그룹의 Jeong 2020이 이미 그 어휘·응용 영역을 대표하고 Choi 2022는 본 연구질문의 취약 고리([C]·[D])에 기여하지 않기 때문이다.

---

## 6. Coverage Matrix

### 6.1 Chain 단계별 검증 seed

| 단계 | 직접 측정으로 담당 | 계산으로 담당 | 저자해석 수준 | 반증·대안 담당 | 상태 |
|---|---|---|---|---|---|
| **[A] Processing condition** | Kwak2007 (소성 500 °C) · Jeong2020 (H₂ 350 °C) · Shi2020 (플라즈마) · *Choi2022 (수열)* · *IngramJones1996 (전구체×가열)* · *Liu2021 (합성)* | Digne2004 (온도↔OH) | — | — | **과포화** |
| **[B] Structural change** | Kwak2007 (Al(V) 정량) · Morterra1996 (IR OH·산점) · Knozinger1978 (OH 유형) · *Chen1992* · *Ishizaki2003 (EPR)* | Prins2020 (구조·양이온공공) · Wischert2012 (Al(III)) | Jeong2020 (Al(V) 생성) | **Wischert2012** (Al(V)는 반응성 site 아님) | **충분** |
| **[C] Oxygen behavior** | **Martin1996** (¹⁸O 교환 620 °C) | **Hinuma2020** (θ상 5.46 eV) · **Carrasco2004** (α상 + 이동장벽) | **Shi2020** (SOV 증감) · **Wang2022** (산소공공 주장) | Prins2020 (양이온공공 구분) | **보강됨 — 실험 1편은 여전히 얇음** |
| **[D] Reducibility** | **Ammendola2011** (CO-TPR 정량 → WGS) · **Amenomiya1978** (water-gas 전환) · **Ostrovski2010** (탄소열 환원 생성물) | — | **Jeong2020** (TCD 267/661 °C = Al 환원) | **Ammendola2011** (= 인용 반증) | **보강됨** |
| **[D′] 대안 설명·반증** | **Joubert2006** (H₂ 해리 25 °C 정량) · **Kramer1979** (spillover) · **Kalamaras2008** (동위원소 추적) · *Fottinger2008* · *Haneda2000* | Wischert2012 | — | — | **확보** |

*기울임*은 OPTIONAL.

### 6.2 고리 연결(transition)별 검증 상태 — 가장 중요한 표

| 연결 | 담당 seed | 증거 등급 **[판단]** |
|---|---|---|
| Processing → Al 배위 변화 | Kwak2007, Jeong2020, Liu2021, Kwak2008(제거) | **강함** (단 자장·스피닝 의존 정량 caveat) |
| Processing → OH 변화 | Digne2004, Knozinger1978, Morterra1996, Choi2022, Shi2020 | **강함** |
| OH 제거 → 저배위 Al site 생성 | Wischert2012, Joubert2006 | **중간** (계산+분광 병행) |
| 저배위 Al site → H₂·CH₄ 활성화 | Joubert2006, Wischert2012 | **중간~강함** (정량 site 밀도 있음) |
| **Al 배위 변화 → 산소공공** | **없음** | **❌ 공백** — Wang2022·Shi2020은 주장만, 인과 측정 없음 |
| 산소공공 → 산소 제거 용이성 | Hinuma2020, Carrasco2004, Martin1996 | **중간** (전부 '어렵다'는 방향) |
| **H₂ 신호 → 산소 제거** | **없음** | **❌ 공백** — Joubert2006·Kramer1979·Ammendola2011이 모두 대안 설명 제시 |
| 벌크 환원의 실제 조건 | Ostrovski2010 | **강함** (단 금속공학 조건) |

### 6.3 축별 분포 (KEEP 18편 기준)

| 축 | 분포 |
|---|---|
| Period | 1978 · 1978 · 1979 · 1996 · 1996 · 2004 · 2004 · 2006 · 2007 · 2008 · 2010 · 2011 · 2012 · 2020 · 2020 · 2020 · 2022 → 1970년대~2020년대 연속 |
| Group | 17개 독립 그룹 (PNNL · ETH · KAIST · Knözinger · Morterra · IFP-Lyon · Copéret–Sautet ×2 · Martin–Duprez · CNR Napoli · Kramer · Amenomiya · Efstathiou · Hinuma · Carrasco–Illas · Shi · Ostrovski · Wang) |
| 분야 커뮤니티 | 촉매화학 · 표면과학 · 계산재료 · **금속공학(Ostrovski)** · 플라즈마처리 — v1의 촉매 편중을 완화 |
| Study type | 실험 12 · 계산 3 · 계산+실험 2 · review 1 |
| Characterization | ²⁷Al NMR · IR/DRIFT · **CO-TPR 정량(CO/CO₂/H₂ 동시)** · **¹⁸O 동위원소 교환** · **operando SSITKA-MS** · H₂ 적정 · DFT · EPR(optional) · TPO · 플라즈마 |
| 산소 관련 측정 보유 | Martin1996(교환) · Ammendola2011(CO₂/H₂ 정량) · Kalamaras2008(동위원소) · Hinuma2020·Carrasco2004(계산) · Ostrovski2010(환원생성물) → v1 대비 **1편 → 6편** |

---

## 7. 남은 공백과 다음 단계

### 7.1 여전히 비어 있는 것 — 검색으로 채워야 할 목표

1. **맨 γ-Al₂O₃의 H₂-TPR을 주제로 한 1차 문헌.** 독립 검색에서도 유효 결과가 5건뿐이었다. 전면 수집 단계에서 `"bare"`/`"blank"`/`"support alone"` + `"H2-TPR"` 조합과 함께, **TPR 그림이 SI에 묻힌 경우**를 찾기 위해 본문 외 자료 검색이 필요하다.
2. **H₂ 소모와 H₂O 생성을 동시 정량한 문헌** (§2의 최소 판별 조합 ①). 현재 KEEP 중 어느 것도 γ-Al₂O₃에 대해 이를 수행하지 않았다.
3. **1차 환원 후 O₂ 재산화로 결손 산소를 적정한 문헌** (§2-②). 미발견.
4. **Al(V) 분율과 산소 결손량을 같은 시료에서 동시 측정한 문헌** (§3-② 공백의 직접 해소). 미발견 — 존재하지 않을 가능성도 있다.
5. γ상(θ·δ 아님) 표면의 산소공공 생성에너지 계산. Hinuma2020은 θ상, Carrasco2004는 α상이다.

### 7.2 Jeong 2020 저자 문의 가능성 **[판단]**

267 °C 피크의 정체는 문헌만으로 닫히지 않을 수 있다. SI Fig. 1의 원 데이터에 MS 채널이 함께 기록되어 있었는지(장비는 MS와 TCD를 모두 갖췄다고 methods에 기술됨)가 결정적이므로, 교신저자 문의가 문헌검색보다 빠른 경로일 수 있다. 이는 문헌연구의 범위를 넘는 선택지로만 남긴다.

### 7.3 방법론 문서(v2)에 반영할 항목

1. **인용 검증은 서지 검증과 별개 단계다.** Gate 1(서지)·Gate 2(claim)에 더해, **"인용된 문헌이 실제로 그 주장을 지지하는가"**를 확인하는 절차가 필요하다. 본 재검토에서 Gate 1·2를 모두 통과한 인용이 내용적으로 주장을 지지하지 않는 사례가 확인되었다.
2. SI 참고문헌 수동 확인 (v1에서 도출, 이번에 그 가치가 입증됨).
3. 필드 제한 Boolean을 query 기본형으로.
4. **"희소성"과 "검색 실패"의 구분**: 결과가 적을 때 query를 의심하기 전에, 독립 경로로 같은 주제를 재검색해 문헌 자체가 희소한지 판정한다(§4.1).

