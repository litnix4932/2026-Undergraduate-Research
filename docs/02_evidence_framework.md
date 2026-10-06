# 증거 framework — 무엇을 reducibility 증거로 인정하는가

> **요약**
> - 문헌에서 **reducibility**는 "H₂를 소모한다"가 아니라 **격자 산소가 빠져나가 조성이 변하는 경향**이다. 대표 척도는 산소공공 생성 비용 E_Ovac다.
> - 처음의 선형 가설 `Processing → Al(V) → oxygen vacancy → reducibility`는 **Al(V) → oxygen vacancy 고리에서 끊어진다.** 이 고리에는 어느 방향으로도 측정 근거가 없다.
> - 연구 동기였던 Jeong 2020의 "267 °C TCD 피크 = Al 환원" 해석은 **인용 근거가 그 주장을 지지하지 않는다.**
> - 이를 반영해 framework를 **5축·2분기**로 개정했다. 증거는 **Tier A(인정) / B(보조) / C(불인정)**로 나눈다. 현재 γ-Al₂O₃에서 Tier A 증거는 0건이다.
>
> 라벨은 [README](../README.md#표기) 참조. 개념 문헌 18편은 [`reducibility_references.csv`](../data/reducibility_references.csv)에 있다. 그중 **9편은 초록을 읽었고, 9편은 서지만 검증했다**(`content_read` 열). 서지만 검증한 문헌(†)은 내용 주장 없이 "주제의 표준 참조"로만 인용한다.

---

## 1. Reducibility의 정의

### 1.1 정준 정의

**[문헌정의]** Ruiz Puigdollers et al. 2017 (ACS Catal., `10.1021/acscatal.7b01913`):
> *"Reducibility is an essential characteristic of oxide catalysts in oxidation reactions following the Mars–van Krevelen mechanism. A typical descriptor of the reducibility of an oxide is the cost of formation of an oxygen vacancy, which measures the tendency of the oxide to lose oxygen or to donate it to an adsorbed species with consequent change in the surface composition, from MnOm to MnOm–x."*

- **Mars–van Krevelen(MvK) 기구**: 반응물이 촉매의 **격자 산소**를 가져가 산화되고, 생긴 빈자리를 기상 O₂가 다시 채우는 산화 반응 기구.
- **산소공공(oxygen vacancy)**: 격자에서 O²⁻ 이온이 빠진 자리.
- **E_Ovac**: 산소공공 하나를 만드는 데 드는 에너지. 클수록 산소를 빼기 어렵다.

**[판단]** 정의의 핵심은 **산소가 빠져나가 조성이 MₙOₘ → MₙOₘ₋ₓ로 변하는 것**이다. H₂-TPR은 이를 측정하는 여러 수단 중 하나일 뿐, 정의에 들어 있지 않다.

### 1.2 Reducibility는 물질이 아니라 site의 속성이다

같은 논문의 원문은 다음과 같다: *"reducibility of the bulk material may differ completely from that of the metal/oxide surface"*. 계면에 대해서는 *"Oxygen atoms can be removed from interface sites at much lower cost than in other regions of the surface."*라고 쓴다. 따라서 올바른 질문은 "γ-Al₂O₃는 reducible한가?"가 아니라 **"γ-Al₂O₃의 어느 site·종결면·계면에서 산소 제거 비용이 얼마인가?"**다.

### 1.3 Reducible / non-reducible은 이분법이 아니다

Kumar et al. 2016 (`10.1021/acscatal.5b02657`)은 C–H 결합 활성화 에너지를 "surface reducibility"(E_Ovac, work function)와 상관시켰다. 원문은 *"The correlation includes several reducible and nonreducible metal-oxides, doped CeO 2, doped TiO 2, ZnO, and doped MgO"*다. **[판단]** 그러므로 reducibility는 범주 라벨이 아니라 **연속량**이다. "non-reducible"이라고 쓰면 연구가 닫히고, "E_Ovac이 매우 높은 산화물"이라고 쓰면 연구가 열린다. 본 연구는 후자의 어법을 쓴다.

### 1.4 Alumina가 스케일의 극단에 있는 이유

- Hinuma 2018 (`10.1021/acs.jpcc.8b11279`) **[측정]**: *"the band gap, bulk formation energy, and electron affinity are factors that strongly influence EOvac"*. 그리고 *"Electrons enter defect states after O desorption, and these states can be in the valence band, mid-gap, or in the conduction band."*
- Deml 2014 (`10.1039/c3ee43874k`) **[측정]** (페로브스카이트 La₁₋ₓSrₓBO₃ 계열): *"The energy to form a single, neutral oxygen vacancy decreases with both the oxide enthalpy of formation and the band gap energy"*.

**[판단]** Al₂O₃는 매우 안정하고(생성엔탈피가 큼) 밴드갭이 넓은 절연체다. 그래서 두 인자가 모두 E_Ovac을 올리는 쪽으로 작용한다. 단, Deml의 결과를 Al₂O₃에 적용하는 것은 외삽이다. 실제 값은 계산 문헌에서 와야 한다(§3).

### 1.5 조작적 정의 — 실무에서 "reducibility"로 측정되는 것

**조작적 정의**란 개념을 실제로 무엇을 재서 판단하는지로 정의한 것이다. 문헌에는 최소 7가지가 있다. 그중 여러 개는 산소 제거를 입증하지 않는다.

| | 조작적 정의 | 산소 제거를 입증하는가 | 근거 |
|---|---|---|---|
| (a) | 계산된 E_Ovac | 정의와 직접 대응 (단, 계산값) | RuizPuigdollers2017, Hinuma2018, Deml2014, Krcha2012† |
| (b) | 격자 산소의 반응 참여 (MvK) | **예 — 가장 강함** | RuizPuigdollers2017, Doornkamp2000† |
| (c) | **OSC**(oxygen storage capacity: 가역적으로 내놓고 다시 받는 산소량) | 예 | Madier1999, Li2018† |
| (d) | 산소 교환·이동성 (¹⁸O 교환, TPIE) | **아니오 — 간접** | Madier1999 |
| (e) | 양이온 산화수 변화 | 간접 (전자 쪽 증거) | Esch2005, Bharti2016 |
| (f) | TPR의 H₂(CO) 소모 | **아니오 — 가장 약함** | Hurst1982, Arnoldy1985†, Fierro1994† |
| (g) | 전자구조 지표 (work function) | 아니오 — 상관 지표 | Kumar2016 |

**(d)가 제거가 아닌 이유.** **¹⁸O 교환**(동위원소 ¹⁸O₂ 기체와 격자 ¹⁶O가 자리를 바꾸는 반응)에서는 산화물의 산소 수가 보존된다. **TPIE**(temperature-programmed isotopic exchange)는 이 교환을 승온하며 재는 실험이다. 따라서 이것은 산소의 **이동성(mobility)**을 재지, **제거 가능성(removability)**을 재지 않는다. Madier 1999(`10.1021/jp991270a`)는 이 둘을 같은 시료에서 **별개 측정으로 병행**했다: *"Modifications in oxygen storage capacity (OSC measurements), redox properties (CO TPR), and oxygen exchange processes (TPIE) were studied."* 이것이 모범 사례다. γ-Al₂O₃ 문헌에는 세 측정을 함께 적용한 사례가 없다.

**(f)가 가장 약한 이유.** H₂ 소모는 산소 제거 없이도 일어난다(§5). 그러므로 (f)는 reducibility의 충분조건이 아니다. 또 OH처럼 격자 산소가 아닌 산소가 빠지는 경우도 있어서 필요조건으로서도 애매하다.

### 1.6 환원의 두 부분 signature와 Al³⁺의 비대칭

**[측정]** Esch 2005(Science, `10.1126/science.1111568`): *"The high performance of ceria (CeO2) as an oxygen buffer and active support for noble metals in catalysis relies on an efficient supply of lattice oxygen at reaction sites governed by oxygen vacancy formation."* 그리고 *"Electrons left behind by released oxygen localize on cerium ions."*

**[판단]** 환원에는 두 부분의 신호가 있다. 하나는 **산소가 떠나는 것**, 다른 하나는 **남은 전자가 어딘가에 국재하는 것**이다. CeO₂는 두 번째를 Ce³⁺로, TiO₂는 Ti³⁺(XPS)로 직접 보여준다[Bharti 2016, `10.1038/srep32355`]. 그런데 **Al³⁺에는 산화물 격자에서 접근 가능한 낮은 산화수가 없다.** 그래서 alumina에서는 전자 쪽 증거를 양이온 신호로 잡을 수 없고, 입증 부담이 결함상태 분광으로 전부 넘어간다. γ-Al₂O₃ 촉매 문헌에는 그 분광 전통이 없다(§6). 이것이 γ-Al₂O₃ reducibility 논증이 **구조적으로** 어려운 이유다.

> ⚠ 이 논거는 무기화학 일반 지식에 기반한 판단이다. Al₂O₃ 격자 내 Al 환원 상태를 다룬 1차 문헌은 아직 찾지 못했다. 보고서에 쓸 때는 출처를 보강하거나 추론으로 표시한다.

---

## 2. 연구 framework

### 2.1 왜 개정했나

처음 framework는 `Processing → Structure → Oxygen behavior → Reducibility/Reactivity`의 4단 선형 사슬이었다. 여기에는 네 가지 결함이 있었다 **[판단]**.

1. **Reducibility와 Reactivity를 한 칸에 묶었다.** 가장 치명적인 결함이다. Joubert 2006의 25 °C H₂ 활성화는 반응성(reactivity)이지 환원성이 아니다. 한 칸에 두면 "반응성이 있으니 환원된다"는 오류가 구조에 내장된다.
2. **"Oxygen behavior"가 서로 다른 세 현상을 뭉쳤다.** Ammendola 2011(OH가 산소원)과 Martin 1996(격자 산소 교환)은 산소원이 다르다.
3. **선형 사슬은 site 특이성을 담지 못한다.** 금속이 있으면 산소 교환 온도가 수백 °C 내려가는데[Martin1996], 이런 계면 경로를 넣을 칸이 없다.
4. **종착점이 예/아니오 이분법을 유도한다**(§1.3).

### 2.2 개정 framework (5축 + 2분기)

```
[P] Processing / Pretreatment
      │   소성 · 환원 · 수열/steam · 진공 · 플라즈마 · 합성경로 · 전구체 · 도핑
      ▼
[S] Surface & defect structure
      │   Al 배위(IV/V/III) · OH 피복률·유형 · 종결면 · 양이온 공공(구조적)
      ▼
      ├──────────────────┬────────────────────┬───────────────────┐
[O1] OH / 물 화학      [O2] 격자 산소 이동    [O3] 산소 제거       │
     산소원 = OH            산소 수 보존 (교환)    산소 수 감소 (공공)   │
      ▼                     ▼                     ▼                │
[R1] Surface reactivity                    [R2] Reducibility       │
     H₂/CH₄ 활성화 · Lewis 산염기              산소 제거 + 전자 귀속   │
     anchoring · WGS · spillover               + 가역성              │
      ▲                                         ▲                  │
      └──────── [I] Metal/oxide interface ───────┴──────────────────┘
                (담지 금속이 있을 때만 열리는 병렬 경로)
```

| 노드 | 뜻 |
|---|---|
| [P] | 합성·후처리 조건 |
| [S] | 표면·결함 구조. **Al 배위수**(Al³⁺를 둘러싼 O 수. 벌크는 4·6배위, 표면에 5배위 Al(V)나 3배위 Al(III) 같은 저배위 site가 생긴다)와 OH |
| [O1] | 표면 OH·물이 산소원이 되는 화학 |
| [O2] | 격자 산소의 이동·교환 (산소 수 보존) |
| [O3] | 격자 산소의 실제 제거 (산소 수 감소) |
| [R1] | 표면 반응성 — 산소를 빼지 않고도 일어나는 반응 |
| [R2] | 환원성 — MvK 의미의 산소 제거 |
| [I] | 금속/산화물 계면 경로 |

**핵심은 세 가지다.** [R1]과 [R2]를 분리했고, [O]를 셋으로 나눴고, [I]를 병렬 경로로 올렸다. 이 구조를 명시한 선행 문헌은 없다(③신규). 단 [R2]의 정의와 [I]의 존재는 Ruiz Puigdollers 2017을 따른다.

### 2.3 연구 표적 — 아직 선택하지 않음

**[판단]** 원래 관심사인 "unusually reactive 또는 potentially reducible γ-Al₂O₃"는 실제로는 **서로 다른 현상들**이다. 각각 증거 기준도 검색 어휘도 다르다. 문헌에 이미 제안된 경로는 네 가지다.

| 경로 | 문헌 근거 | 재구성 |
|---|---|---|
| ① 금속/산화물 계면 | RuizPuigdollers2017 **[저자해석]**: *"Combining oxide nanostructuring with metal/oxide interfaces opens promising perspectives to turn hardly reducible oxides into reactive materials in oxidation reactions based on the Mars–van Krevelen mechanism."* | **가장 직접적이다.** 목표를 "γ-Al₂O₃/금속 계면에 산소가 싸게 빠지는 site를 만든다"로 바꾸면 문헌이 이미 지지한다. Jeong 2020(Al(V)에 ceria·금속 고정)도 이 범주로 읽을 수 있다 |
| ② 종결면·나노구조 제어 | Hinuma2020: θ-Al₂O₃에서 면에 따라 E_Ovac이 1.11 eV 차이 | facet(노출 결정면) 제어로 1 eV 규모 조절 여지. Liu2021(Al(V) 풍부 구조)이 실험 후보 |
| ③ 도핑 | Kumar2016, Deml2014 | E_Ovac을 움직이는 확립된 수단이나, γ-Al₂O₃ 도핑 문헌은 미탐색 |
| ④ OH 매개 산소 공급 | Ammendola2011, Amenomiya1978 | reducibility는 아니지만 **산소를 내주는 기능**은 한다. 이 경로라면 용어를 *OH-mediated oxygen transfer*로 바꿔야 한다 |

개정 framework는 네 경로를 모두 담는다. 그래서 표적을 정하지 않고도 mapping을 진행할 수 있다. 표적 선택은 지도교수와 논의할 과학적 결정이다.

---

## 3. Reducible oxide들은 무엇으로 판단하나

| 증거 축 | CeO₂ | TiO₂ | **γ-Al₂O₃ (현재)** |
|---|---|---|---|
| 산소 제거 정량 (H₂ 소모 + H₂O 생성) | 있음 | 있음 | **없음** |
| 재산화 적정 / 가역성 | 있음 (OSC) | 있음 | **없음** |
| 전자 귀속 | Ce³⁺ (STM/DFT, XPS)[Esch2005] | Ti³⁺ (XPS)[Bharti2016] | **양이온 신호 원리상 불가 + 결함상태 측정 전통 없음** |
| 격자 산소 반응 참여 (MvK, 동위원소) | 있음 | 있음 | **없음** |
| 산소 교환·이동성 | ~410 °C | 있음 | **620 °C** [Martin1996] |
| 계산 E_Ovac | 낮음 | 낮음 | **5.46 eV (θ상)** [Hinuma2020] |
| TPR 신호 | 있음 | 있음 | 있음 — **TCD 단독** (Jeong 2020) |

- **CeO₂**의 결함 구조조차 완결되지 않았다. Schmitt 2019(`10.1039/c9cs00588a`) **[저자해석]**: *"for undoped ceria and its solid solutions, the relationship between short range order and cation-oxygen-vacancy coordination remains a subject of active debate"*. 그러니 γ-Al₂O₃에 더 강한 확실성을 기대할 수 없다.
- **TiO₂**는 공기 플라즈마 처리 후 XPS로 Ti³⁺와 산소공공이 확인되었고, 밴드갭이 3.22 → 3.00 eV로 줄었다(Fe 도핑 시료)[Bharti2016].
- 표준 참조: TiO₂ 표면과학은 Diebold 2003†, 철산화물은 Parkinson 2016†, 산소공공 일반은 Ganduglia-Pirovano 2007†, MvK는 Doornkamp 2000†.
- **계산 기준선** [Hinuma2020, `10.1021/acs.jpcc.0c00994`]: 접근 가능한 표면 중 최저 E_Ovac은 θ-Al₂O₃ (201̄)에서 **5.46 eV**다. 비교 대상 β-Ga₂O₃ (101)은 3.04 eV다. 최안정면 대비 감소분은 각각 1.11 / 1.32 eV다. **[판단]** 이 결과의 의미는 두 가지다. ① 전이 alumina의 산소 제거 비용은 반응성 산화물 영역과 멀다. ② 그러나 **같은 물질 안에서 종결면만 바꿔도 약 1 eV가 움직인다.**

**[판단]** γ-Al₂O₃에서 채워진 칸은 Tier B 두 개(교환·계산)와 Tier C 하나(TCD)뿐이다.

---

## 4. 사례: 인용이 주장을 지지하지 않는다

이 사례는 Gate 3([01_methodology.md](01_methodology.md#gate-3--인용-지지-검증))을 신설한 계기다.

### 4.1 출발점 — Jeong 2020

Jeong et al., *Nat. Catal.* **3**, 368–375 (2020), `10.1038/s41929-020-0427-z`.
- **H₂-TPR 조건**: BELCAT-B 장비(MS + TCD 검출기 보유). Ar 250 °C 2 h 전처리 → 5% H₂/Ar, 10 °C/min, 800 °C까지.
- **[측정]** Supplementary Fig. 1: 신선 γ-alumina의 **TCD** 신호가 **267 °C에서 큰 피크, 661 °C에서 작은 피크**를 보인다.
  - **TCD(thermal conductivity detector)**: 기체 열전도도 변화를 재는 검출기. 어떤 기체가 변했는지 **구별하지 못한다**.
  - 그림에는 H₂ 소모 정량값도 MS 질량 추적도 없다.
  - **[판단]** 이 그림이 본 연구의 출발점이다. 원래 목표 관측은 "reducible γ-Al₂O₃를 만들면 200–300 °C에서 큰 H₂ 소모 신호가 나온다"였다.
- **[저자해석]** 캡션: *"The peaks at 267 and 661 °C indicate the reduction of weakly coordinated surface aluminum and the reduction of strongly coordinated bulk aluminum, respectively."* 근거로 SI 참고문헌 1, 2를 든다. 본문에는 *"A temperature of 350 ºC, at which the reduction of surface Al is complete, was chosen."*이라고 쓴다.
- SI 참고문헌 2(Zheng et al., Appl. Catal. B 202, 51–63, 2017)는 제목상 LaFeO₃/CeO₂ 산소운반체 연구다. alumina 근거가 아니다(원문 미열람).

### 4.2 인용된 근거 — Ammendola 2011 원문 확인

Ammendola et al., *Surf. Sci.* **605**, 1812–1817 (2011), `10.1016/j.susc.2011.06.018`. 이 논문은 Jeong 2020 **SI에만** 인용되어 있어서 OpenAlex 자동 BWC로는 잡히지 않았다.

**[측정] 실험**
- 이 논문은 **CO-TPR**이다. **맨 alumina의 H₂-TPR은 논문에 없다**(H₂-TPR은 Pt 촉매 1건에만 수행).
- 시료: La/γ-Al₂O₃와 γ-Al₂O₃, 그리고 Pt·Cu 담지 촉매. 모두 공기 800 °C 3 h 전처리.
- CO/N₂, 10 °C/min, 800 °C까지 승온. CO·CO₂는 적외선 검출기, H₂는 TCD, O₂는 상자성 셀로 동시 정량.
- 순수 지지체의 CO 소모는 약 400 °C에서 시작해 **594 °C(La/γ-Al₂O₃) / 602 °C(γ-Al₂O₃)**에서 최대다.

| 시료 | CO 소모 (μmol/g) | CO₂ 생성 | H₂ 생성 | H₂/CO₂ |
|---|---|---|---|---|
| La/γ-Al₂O₃ | 191 | 181 | 184 | 1.02 |
| γ-Al₂O₃ | 229 | 216 | 205 | 0.95 |
| 1 wt% Pt/La/γ-Al₂O₃ | 589 | 589 | 424 | 0.80* |
| 8 wt% Cu/γ-Al₂O₃ | 1802 | 1805 | 705 | 0.70* |

\*금속 환원 기여분을 뺀 값. Pt²⁺ 완전환원 상당 56 μmol/g, Cu 60% 환원 상당 794 μmol/g.

- **DRIFT**(확산반사 적외선 분광): CO-TPR 후 bridged OH(3737 cm⁻¹)와 linear OH(3840 cm⁻¹) 밴드가 크게 감소했고, 3840 cm⁻¹ 밴드는 소멸했다. 흡착수(1684)·carbonate(1530) 밴드가 사라지고 1590 cm⁻¹ 밴드가 나타났다.
- **TPO**(승온 산화): CO₂ 주 피크가 240 °C로 코크 연소로 보기엔 너무 낮다. 550 °C의 작은 피크가 코크 상당(약 1.6 μmol/g)인데, CO 소모량에 비해 무시할 만하다 → **Boudouard 반응**(2CO → C + CO₂) 배제.

**[저자해석]** CO 소모는 **표면 OH와 CO의 water-gas shift(WGS) 반응**으로 귀속된다.
- vicinal linear OH 두 개가 축합해 물을 만들고, 그 물이 CO와 반응한다: `CO + H₂O → CO₂ + H₂` (H₂/CO₂ = 1).
- linear OH가 소진되면 bridged OH가 반응한다: `CO + OH → CO₂ + ½H₂` (H₂/CO₂ = 0.5).
- 금속이 있으면 금속에 흡착된 CO의 **spillover**(금속 위 흡착종이 지지체로 옮겨가는 현상)로 WGS가 가속된다.
- 결론 원문: *"Pure and La-stabilized γ-Al₂O₃ reacted with CO at T ≥ 400 °C through a WGS reaction involving surface OH groups producing CO₂ and H₂."* 그리고 *"the alumina contribution to CO TPR, a method typically used as a characterisation technique to investigate metal oxide-supported catalysts, was significant. Thus, quantitative results must be carefully analysed by taking into account hydrogen production associated with the WGS reaction."*

### 4.3 판정

| | Jeong 2020 SI Fig. 1의 주장 | Ammendola 2011이 보고한 것 |
|---|---|---|
| 실험 | H₂-TPR | **CO-TPR** |
| 온도 | **267** / 661 °C | 개시 ~400, 최대 **594 / 602 °C** |
| 귀속 | surface / bulk Al의 환원 | **표면 OH와 CO의 WGS** (산소원 = OH) |
| Al 환원 언급 | 핵심 주장 | **없음** |
| 함의 | alumina가 환원된다 | alumina의 OH 화학이 **TPR 정량을 오염**시키므로 보정해야 한다 |

**[판단]** 인용 방향이 반대다. 서지는 정확하므로 Gate 1·2로는 잡히지 않는다.

단, 이 판정은 **"γ-Al₂O₃는 환원되지 않는다"를 증명하지 않는다.** 증명하는 것은 "이 주장이 기대는 인용이 그 주장을 지지하지 않는다"뿐이다. 267 °C 피크의 정체는 열려 있다.

**[판단] 267 °C 피크의 후보 설명**
- 전처리가 Ar 250 °C였다. Digne 2004 DFT에 따르면 이 온도대에서 표면 OH는 상당량 남는다. (110)면은 500–1000 K에서 3.0 OH/nm², (111)면은 1000 K에서도 9.8 OH/nm²다.
- TCD는 H₂ 소모와 **H₂O 발생을 구분하지 못한다**. 물은 오히려 큰 TCD 응답을 준다.
- H₂ 분위기에서도 OH 축합에 의한 **dehydroxylation**(인접 OH 두 개가 물로 빠져나가는 탈수산기)은 독립적으로 진행된다.

→ 267 °C 피크가 격자 산소 제거인지, H₂ 해리흡착인지, spillover인지, 탈수산기인지는 이 그림만으로 **판별할 수 없다.** 판별 설계는 §5에 있다. SI Fig. 1 원 데이터에 MS 채널이 기록되었는지를 교신저자에게 문의하는 편이 문헌검색보다 빠를 수 있다. 이것은 문헌연구 범위 밖의 선택지다.

---

## 5. H₂ 분위기 신호의 판별

**[판단]** H₂ 분위기 승온에서 TCD·H₂ 소모 신호를 만드는 과정은 최소 여섯 가지다. **그중 격자 산소를 제거하는 것은 하나뿐이다.**

| # | 현상 | 격자 산소 제거? | 판별 수단 | 관련 문헌 |
|---|---|---|---|---|
| 1 | **격자 산소 제거 (진짜 환원)** | **예** | H₂O **정량** + O₂ 재산화 적정 + ¹⁸O + TGA | Martin1996, Hinuma2020, Carrasco2004, Ostrovski2010 |
| 2 | **H₂ heterolytic dissociation** (H₂가 Al–O 쌍에서 H⁻와 H⁺로 갈라져 Al–H, O–H를 만듦) | 아니오 | IR의 Al–H 밴드, 가역성, site 수에 비례한 포화 | Joubert2006, Wischert2012 |
| 3 | 해리흡착 + spillover | 아니오 | 금속 유/무 대조, 동위원소 추적 | Kramer1979, Kalamaras2008, Shi2020 |
| 4 | dehydroxylation / OH 축합 | 아니오 (산소는 H₂O로 나감) | **MS m/z 18 추적**, IR OH 영역, 전처리 온도 의존성 | Knozinger1978, Morterra1996, Digne2004 |
| 5 | OH 기반 WGS (CO 존재 시) | 아니오 (산소원 = OH) | CO₂/H₂ 화학량비, DRIFT OH 소모 | Ammendola2011, Amenomiya1978, Fottinger2008 |
| 6 | 금속 전구체·잔류물 환원 | alumina 아님 | 맨 지지체 blank 대조 | 실험 설계 |

**최소 판별 조합 [판단]**
1. H₂ 소모와 **H₂O 생성을 MS로 동시 정량**한다.
2. TPR 후 **O₂ 재산화**로 결손 산소량을 적정한다.
3. 전처리 온도를 올려(예: 700 °C) OH를 줄인 뒤 피크가 줄어드는지 본다.
4. **금속 없는 맨 alumina**로 대조한다.

이 네 가지를 갖춘 문헌이 있는지가 전면 수집의 핵심 검색 과제다.

---

## 6. 사슬 고리별 증거 감사

각 고리를 **전제하지 않고** 현재 확보한 근거만으로 평가했다.

| 고리 | 상태 | 근거 |
|---|---|---|
| ① Processing → Al(V) 생성 | **강함** | Kwak2007: 21.1 T, 23 kHz에서 Al(V) 1.56 mol%, 표면 국재. Jeong2020: 350 °C H₂ 처리 후 Al(V) 출현. Liu2021: 합성으로 Al(V) 풍부 구조. **caveat**: ²⁷Al MAS NMR(고체 NMR. 시료를 고속 회전시켜 Al 배위수별 피크를 분리) 정량은 자기장과 회전속도에 민감하다(Kwak: 23 kHz 1.56% vs 15 kHz 3.3%). 그래서 Jeong(9.4 T)과 Kwak(21.1 T)의 값은 직접 비교할 수 없다 |
| ② **Al(V) → oxygen vacancy** | **독립 증거 없음** | Al(V)는 **양이온의 배위 상태**이고 oxygen vacancy는 **O²⁻의 결손**이다. 어떤 문헌도 "Al(V)를 만들면 산소가 빠진다"를 측정하지 않았다. 오히려 Wischert2012는 반응성 site가 **부분 dehydroxylation으로 생기는 Al(III)**라고 본다. 즉 배위수 감소의 원인은 OH 제거다. Wang2022·Shi2020은 Al(V)·산소공공을 함께 **주장**하지만 인과를 측정하지 않았다 |
| ③ oxygen vacancy → 제거 용이성 | **중간, 전부 "어렵다" 방향** | Hinuma2020: θ상 5.46 eV. Carrasco2004: α-Al₂O₃ 등 이온성 산화물의 공공 생성·이동 장벽. Martin1996: ¹⁸O 교환 최대 620 °C(CeO₂ 410 °C). Ostrovski2010: 벌크 환원에는 **탄소열 조건**이 필요하고, 생성물은 Al₄C₃와 Al·Al₂O 증기다. 어느 것도 200–300 °C 산소 제거를 지지하지 않는다 |
| ④ 267 °C TCD → 산소 제거 | **근거 없음** | §4 |

**혼동 주의 — cation vacancy ≠ oxygen vacancy.** Prins 2020이 말하는 γ-Al₂O₃의 "vacancy"는 **양이온 공공**(Al³⁺ 자리의 빈자리)이다. 이는 스피넬형 구조가 Al:O = 2:3 화학량을 맞추려고 **원래 가진 정상 구조**다. 구조식은 (Al_T)(Al_O)₅ᐟ₃(V_O)₁ᐟ₃(O)₄다(T = 사면체, O = 팔면체 자리, V = 공공). 환원으로 생기는 산소공공과는 다른 개념이다. 둘을 "defect"로 묶으면 "원래 vacancy가 많으니 환원이 쉽다"는 잘못된 추론이 나온다.

**고리 연결별 정리**

| 연결 | 담당 문헌 | 강도 |
|---|---|---|
| Processing → Al 배위 변화 | Kwak2007, Jeong2020, Liu2021 | 강함 (NMR 조건 caveat) |
| Processing → OH 변화 | Digne2004, Knozinger1978, Morterra1996, Choi2022, Shi2020 | 강함 |
| OH 제거 → 저배위 Al site | Wischert2012, Joubert2006 | 중간 |
| 저배위 Al → H₂·CH₄ 활성화 | Joubert2006, Wischert2012 | 중간~강함 |
| **Al 배위 변화 → 산소공공** | 없음 | **공백** |
| 산소공공 → 제거 용이성 | Hinuma2020, Carrasco2004, Martin1996 | 중간 ("어렵다") |
| **H₂ 신호 → 산소 제거** | 없음 | **공백** — 대안 설명만 존재 |
| 벌크 환원의 실제 조건 | Ostrovski2010 | 강함 (금속공학 조건) |

### 증거는 촉매 문헌 밖에 있다 [판단]

같은 패턴이 독립적으로 세 번 확인되었다. γ-Al₂O₃ 촉매 커뮤니티는 결함을 Al 배위수와 OH로 기술하고, 산소공공을 직접 재지 않는다. 이것은 **"산소공공이 없다"가 아니라 "그 측정 전통이 없다"**는 뜻이다.

| 증거 | 보유 커뮤니티 | 전이 가능성 |
|---|---|---|
| 산소공공 분광 (**F-center**: 산소공공에 전자가 갇힌 결함. EPR·광흡수로 검출) | 핵재료·광학 (중성자 조사 α-Al₂O₃ 단결정) | 상·시료가 달라 개별 평가 필요 |
| 벌크 환원 조건 | 금속공학 (탄소열 환원, Ostrovski2010) | 조건이 촉매 영역과 동떨어짐 |
| ¹⁸O/SIMS 산소 수송 추적 | 고온산화·산화피막 (금속 표면의 alumina **scale**) | α상 피막 → γ상 분말 전이 가능성 개별 평가 |

---

## 7. 증거 등급 Tier A/B/C

전체 기준표(각 기준이 무엇을 입증하고 **무엇을 입증하지 못하는지**)는 [`reducibility_evidence_criteria.csv`](../data/reducibility_evidence_criteria.csv)에 있다.

**Tier A — reducibility 증거로 인정**

| ID | 요구 측정 | 입증하는 것 |
|---|---|---|
| A1 | H₂(CO) 소모와 **H₂O(CO₂) 생성을 동시 정량**하고 화학량 일치 | 산소가 실제로 제거됨 (단독으로는 격자 산소인지 OH 유래인지 구분 못함) |
| A2 | 환원 후 **O₂ 재산화로 소모 산소량 적정** + 사이클 재현성 | 산소 결손이 생기고 되돌릴 수 있음 |
| A3 | 환원된 양이온 또는 **mid-gap 결함상태**(밴드갭 중간의 전자 준위)를 XPS/XANES/EPR/광학으로 확인 | 빠져나간 산소가 남긴 전자의 위치 |
| A4 | **¹⁸O 표지 격자 산소가 생성물에 나타남** (MvK) | 그 산소가 반응에 쓰였음 — 최강 |

**인정 최소 조건: A1 + (A2 또는 A3).** A4가 있으면 가장 강한 주장이 가능하다. 이 조합은 ceria·titania 관행에서 역산한 **본 프로젝트의 제안**이다(③신규). 이를 요구한 guideline 문헌은 찾지 못했다.

**Tier B — 보조 지표 (단독으로 "reducible하다" 주장 불가)**

| ID | 측정 | 말할 수 있는 것 | γ-Al₂O₃ 현황 |
|---|---|---|---|
| B1 | OSC류 산소 흡·방출량 | 용량 | 미발견 |
| B2 | ¹⁸O 교환 / CO 과도응답 | 이동성 (≠ 제거 용이성) | Martin1996: 620 °C |
| B3 | 계산 E_Ovac | 그 면의 제거 비용 | Hinuma2020: θ상 5.46 eV |

**Tier C — 불인정**

| ID | 유형 | 이유 |
|---|---|---|
| C1 | TCD 단독 TPR 피크 | H₂ 소모, H₂O 발생, 탈수산기를 구분할 수 없다. **Jeong 2020 SI Fig. 1이 여기 해당** |
| C2 | H₂ 소모량 단독 | 해리흡착·spillover로도 같은 신호가 난다 |
| C3 | Al 배위수·OH 변화 관측 | [S] 증거일 뿐이다 |
| C4 | ceria·Pt 등과 함께 있는 시료의 환원 신호 | alumina 자체로 귀속할 수 없다. 금속은 교환·WGS를 수백 °C 가속한다 |
| C5 | 산소 제거 없는 표면 반응성 | **[R1] 증거로는 유효**하지만 [R2] 증거는 아니다 |

**불변 규칙**
- Tier C만으로 "γ-Al₂O₃가 환원된다"는 서술을 만들지 않는다. Tier C 문헌은 측정한 것을 그대로 쓴다. 예: "H₂ 승온에서 267 °C에 TCD 피크가 관측되었다 — 저자는 표면 Al 환원으로 해석".
- Al(V), 저배위 Al, 표면 결함, 산소공공의 보고는 그 자체로 reducibility 증거가 아니다.

**현황 [판단]: Tier A 0건, Tier B 2건, Tier C 다수.** 이것은 "없다"가 아니라 "아직 찾지 못했다"이다. Tier A 조건이 곧 다음 검색의 표적이다. 표적별 검색 결과는 [04_query.md §5](04_query.md#5-tier-a-표적-어휘의-생산성-시험)에 있다.

---

## 8. 남은 한계

1. 개념 문헌 18편 중 9편은 서지만 검증했다(Ganduglia-Pirovano 2007, Doornkamp 2000 등). Gate 3 기준을 스스로 적용하면, 이들에 기대는 개념 주장은 원문 확인 전까지 잠정적이다.
2. Tier A 최소 조건은 본 프로젝트의 제안이다.
3. Al³⁺ 저산화수 논거(§1.6)는 추론이며 1차 문헌 보강이 필요하다.
4. 산소공공 생성에너지 계산은 θ상(Hinuma2020)과 α상(Carrasco2004)만 있다. **γ상 표면 계산은 미확보**다.
