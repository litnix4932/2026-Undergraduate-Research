# "Reducibility" 개념의 문헌적 검증과 증거 인정 기준
### γ-Al₂O₃ 문헌연구에서 무엇을 reducibility evidence로 인정할 것인가

**선행 문서**: `seed_set_v2_review.md` · `seed_set_analysis.md` · `literature_methodology.md`
**근거 문헌**: 18편 (전부 Crossref 대조 검증 통과 — `reducibility_references.csv`)
**이 단계의 목적**: γ-Al₂O₃ seed를 더 모으는 것이 아니라, **앞으로 어떤 증거를 reducibility 증거로 인정할지 기준을 먼저 확정**하는 것.

### 표기 규약

| 표기 | 의미 |
|---|---|
| **[문헌정의]** | 문헌이 명시적으로 내린 정의 |
| **[측정]** | 논문이 실제로 측정·계산한 값 |
| **[저자해석]** | 저자의 해석 |
| **[판단]** | Claude의 판단 — 문헌의 주장이 아님 |

### ⚠ 근거의 열람 수준 명시

18편 중 **9편은 초록을 열람**했고, **9편은 제목·저널·저자·DOI만 검증**했다(OpenAlex·Crossref에 초록이 없고 closed access). 후자(Ganduglia-Pirovano 2007, Doornkamp 2000, Hurst 1982, Arnoldy 1985, Fierro 1994, Li 2018, Mullins 2015, Diebold 2003, Parkinson 2016, Krcha 2012)에 대해서는 **내용 주장을 하지 않고 "해당 주제의 표준 참조"로만 인용**한다. 열람 상태는 `reducibility_references.csv`의 `content_read` 열에 기록했다.

---

## 1. 문헌에서 reducibility는 무엇을 의미하는가 (질문 1)

### 1.1 정준 정의

가장 명시적인 정의는 Ruiz Puigdollers et al. 2017 (ACS Catalysis, `10.1021/acscatal.7b01913`)에 있다.

**[문헌정의]** 원문: *"Reducibility is an essential characteristic of oxide catalysts in oxidation reactions following the Mars–van Krevelen mechanism. A typical descriptor of the reducibility of an oxide is the cost of formation of an oxygen vacancy, which measures the tendency of the oxide to lose oxygen or to donate it to an adsorbed species with consequent change in the surface composition, from MnOm to MnOm–x."*

이 한 문장에 세 가지가 들어 있다.

| 요소 | 내용 |
|---|---|
| **무엇에 대한 속성인가** | Mars–van Krevelen 기구를 따르는 **산화 반응**에서의 산화물 촉매 특성 |
| **물리적 내용** | 산화물이 **산소를 잃거나 흡착종에 내주는 경향**, 그 결과 표면 조성이 MₙOₘ → MₙOₘ₋ₓ로 변함 |
| **대표 척도** | **산소 공공 생성 비용**(E_Ovac) |

**[판단] 여기서 중요한 것은 reducibility가 "H₂를 소모한다"로 정의되지 않는다는 점이다.** 정의의 핵심은 **산소가 산화물에서 빠져나가 조성이 변한다**는 데 있다. H₂-TPR은 그것을 측정하는 여러 수단 중 하나일 뿐이고, 정의 자체에 등장하지 않는다.

### 1.2 reducibility는 물질 속성이 아니라 site 속성이다

같은 논문이 명시한다. **[문헌정의/저자해석]** *"reducibility of the bulk material may differ completely from that of the metal/oxide surface"*, 그리고 금속/산화물 계면에 대해 *"Oxygen atoms can be removed from interface sites at much lower cost than in other regions of the surface."*

**[판단]** 따라서 "γ-Al₂O₃는 reducible한가?"라는 질문은 문헌의 용법에 비추면 **덜 잘 정의된 질문**이다. 올바른 형태는 **γ-Al₂O₃의 어떤 site/종결면/계면에서 산소 제거 비용이 얼마인가**다. 이것은 뒤의 framework 수정(§4)으로 직결된다.

### 1.3 reducible / non-reducible은 이분법이 아니다

Kumar et al. 2016 (ACS Catalysis, `10.1021/acscatal.5b02657`)은 **[측정]** *"Density functional theory calculations are used to correlate the C–H bond activation energy to the surface reducibility (oxygen vacancy formation energy, work function)"* 이며, 그 상관이 *"The correlation includes several reducible and nonreducible metal-oxides, doped CeO 2, doped TiO 2, ZnO, and doped MgO"* 라고 보고한다.

**[판단]** reducible 산화물과 non-reducible 산화물이 **하나의 연속적 상관관계 위에 함께 놓인다.** 즉 reducibility는 범주 라벨이 아니라 **E_Ovac이라는 연속량의 값**이다. γ-Al₂O₃를 "non-reducible"로 분류하는 것과 "E_Ovac이 매우 높은 산화물"로 기술하는 것은 전자가 연구를 닫고 후자가 연구를 여는 차이다. 본 연구는 후자의 어법을 채택해야 한다.

### 1.4 E_Ovac을 결정하는 것

- Hinuma et al. 2018 (JPCC, `10.1021/acs.jpcc.8b11279`) **[측정]** *"the band gap, bulk formation energy, and electron affinity are factors that strongly influence EOvac"*, 그리고 *"Electrons enter defect states after O desorption, and these states can be in the valence band, mid-gap, or in the conduction band."*
- Deml et al. 2014 (Energy Environ. Sci., `10.1039/c3ee43874k`) **[측정]** 페로브스카이트 La₁₋ₓSrₓBO₃ 계열에서 *"The energy to form a single, neutral oxygen vacancy decreases with both the oxide enthalpy of formation and the band gap energy"*.

**[판단]** 두 결과를 합치면 **왜 alumina가 스케일의 극단에 있는지**가 설명된다. Al₂O₃는 생성엔탈피가 매우 큰(= 매우 안정한) 넓은 밴드갭 절연체이므로, Deml의 관계식 양쪽 항이 모두 E_Ovac을 **올리는** 방향으로 작용한다. 또한 Hinuma의 지적대로 산소가 빠지면 전자가 어딘가의 결함상태로 들어가야 하는데, 넓은 밴드갭 절연체에서는 그 상태가 비싸다. 단 **Deml의 연구 대상은 페로브스카이트이므로 Al₂O₃로의 외삽은 나의 추론**이며, 실제 정량값은 계산 문헌에서 직접 와야 한다(§3.4의 Hinuma 2020 값).

---

## 2. reducibility는 반드시 lattice oxygen removal을 뜻하는가 (질문 2)

**결론: 정의상으로는 그렇다. 그러나 실무에서 쓰이는 조작적 정의(operational definition)는 최소 7가지이고, 그중 몇 개는 산소 제거를 입증하지 않는다.**

| # | 조작적 정의 | 산소 제거를 입증하는가 | 근거 문헌 |
|---|---|---|---|
| (a) | **산소 공공 생성 비용 E_Ovac** (계산) | 정의상 직접 대응 — 단 계산값 | RuizPuigdollers2017, Hinuma2018, Deml2014, Krcha2012† |
| (b) | **격자 산소의 반응 참여** (MvK) | **예 — 가장 강한 증거** | RuizPuigdollers2017, Doornkamp2000† |
| (c) | **산소 저장 용량 (OSC)** | 예 — 가역적 방출·흡수량 | Madier1999, Li2018† |
| (d) | **산소 교환·이동성** (¹⁸O, TPIE) | **아니오 — 간접** | Madier1999 |
| (e) | **양이온 산화수 변화** | 간접 — 전자 쪽 증거 | Esch2005, Bharti2016 |
| (f) | **H₂(또는 CO) 소모 in TPR** | **아니오 — 가장 약함** | Hurst1982†, Arnoldy1985†, Fierro1994† |
| (g) | **전자구조 지표** (work function) | 아니오 — 상관 지표 | Kumar2016 |

† 제목·서지만 검증(원문 미열람) — 주제 표준 참조로만 인용.

### 2.1 (d) 산소 교환이 산소 제거가 아닌 이유

**[판단]** ¹⁸O₂/¹⁶O 교환은 격자 산소와 기상 산소가 **자리를 바꾸는** 과정으로, 산화물의 산소 수는 보존된다. 즉 교환은 **산소의 이동성(mobility)**을 측정하지 **제거 가능성(removability)**을 측정하지 않는다. 두 성질은 상관되지만 동일하지 않다 — 이동성이 높아도 제거 비용은 높을 수 있다.

Madier et al. 1999 (JPC B, `10.1021/jp991270a`)은 이 둘을 실제로 **별개 측정으로 분리해 병행**한다. **[측정]** *"Modifications in oxygen storage capacity (OSC measurements), redox properties (CO TPR), and oxygen exchange processes (TPIE) were studied."* 그리고 **[저자해석]** *"All mixed oxides are able to exchange very large amounts of oxygen compared to ceria, implying the participation of bulk oxygen."*

**[판단]** 이것이 모범 사례다 — 같은 시료에 **OSC(용량) + CO-TPR(환원) + TPIE(교환)** 세 측정군을 모두 적용해야 "redox properties"를 말할 수 있다. 본 연구의 γ-Al₂O₃ 문헌에는 이 세 가지가 함께 적용된 사례가 없다(§3.5).

### 2.2 (f) H₂ 소모가 가장 약한 이유

`seed_set_v2_review.md` §2에서 이미 정리했듯 H₂ 분위기 승온에서 신호를 만드는 경로는 최소 6가지이고 그중 산소를 제거하는 것은 하나다. 여기에 문헌적 근거를 더하면:

- Joubert et al. 2006 (`10.1021/jp0641841`) **[측정]** γ-alumina가 **약 25 °C**에서 H₂와 heterolytic splitting으로 반응하며(Al–H, O–H 생성) defect 밀도가 0.043–0.069 site/nm²다 → **산소 제거 없는 H₂ 소모**.
- Kramer & Andre 1979 (`10.1016/0021-9517(79)90266-5`) — spillover에 의한 alumina 상 원자수소 흡착.
- Ammendola et al. 2011 (`10.1016/j.susc.2011.06.018`) **[측정]** 맨 γ-Al₂O₃가 CO와 반응해 CO₂·H₂를 생성하는데 그 산소원은 **표면 OH**이며(H₂/CO₂ ≈ 0.95–1.02), 저자는 TPR 정량을 환원으로 읽지 말라고 명시적으로 경고한다.

**[판단]** 따라서 (f)는 reducibility의 **필요조건도 충분조건도 아니다.** 산소가 빠지면 H₂가 소모되지만(필요), H₂ 소모가 산소 제거를 뜻하지는 않는다(불충분). 그리고 OH 경로처럼 **산소가 빠지지만 격자 산소가 아닌** 경우도 있어 필요조건조차 애매해진다.

### 2.3 (e) 양이온 산화수 변화 — alumina에서 가장 중요한 비대칭

Esch et al. 2005 (Science, `10.1126/science.1111568`) **[측정]** *"The high performance of ceria (CeO2) as an oxygen buffer and active support for noble metals in catalysis relies on an efficient supply of lattice oxygen at reaction sites governed by oxygen vacancy formation."* 그리고 결정적으로 *"Electrons left behind by released oxygen localize on cerium ions."*

**[판단] 환원에는 2부 signature가 있다 — 산소가 나가고(산소 쪽), 전자가 어딘가에 들어간다(전자 쪽).** ceria는 두 번째를 Ce³⁺로, titania는 Ti³⁺로 직접 관측할 수 있다(Bharti2016). 그런데 **Al³⁺에는 산화물 격자에서 접근 가능한 저산화수 상태가 없다.** 따라서 alumina에서는 전자 쪽 증거를 양이온 신호로 잡을 수 없고, Hinuma2018이 말한 **결함상태(valence band / mid-gap / conduction band)** 쪽으로 입증 부담이 전부 넘어간다. 그리고 넓은 밴드갭 절연체에서 그 상태를 분광학적으로 잡는 전통이 γ-Al₂O₃ 촉매 문헌에는 없다(`seed_set_analysis.md` §4.3에서 확인).

→ **이것이 γ-Al₂O₃ reducibility 논증이 구조적으로 어려운 핵심 이유다.** CeO₂·TiO₂가 쓰는 가장 결정적인 증거 유형이 원리적으로 사용 불가능하다.

---

## 3. 대표적 reducible oxide는 무엇을 근거로 reducibility를 판단하는가 (질문 3)

### 3.1 CeO₂ — 가장 완비된 증거 패키지

| 증거 축 | 측정 | 근거 |
|---|---|---|
| 산소 공급과 공공 생성 | 격자 산소가 반응 site에 공급되는 것이 성능의 근거이며 산소공공 생성이 그것을 지배 | Esch2005 **[측정/저자해석]** |
| **전자 귀속** | 방출된 산소가 남긴 전자가 **Ce 이온에 국재**; 2개 이상 공공 클러스터는 환원된 Ce 이온만 노출 | Esch2005 **[측정]** (고분해능 STM + DFT) |
| 용량 | OSC 측정 | Madier1999, Li2018† |
| 환원 거동 | CO-TPR | Madier1999 |
| 산소 교환 | TPIE (¹⁸O) | Madier1999 |
| 국소 결함 구조 | 열역학 해석 + Raman + XAFS. **[저자해석]** 이 국소 구조는 비주기적이어서 통상적 X선 분말회절로는 검출되지 않음 | Schmitt2019 |

**[판단] 주목할 점**: ceria조차 결함 구조가 완결되지 않았다. Schmitt et al. 2019 (Chem Soc Rev, `10.1039/c9cs00588a`)는 **[저자해석]** *"for undoped ceria and its solid solutions, the relationship between short range order and cation-oxygen-vacancy coordination remains a subject of active debate"* 라고 적는다. 가장 잘 연구된 reducible 산화물에서도 "결함 구조 ↔ 공공 배위"의 관계는 논쟁 중이라는 것 — γ-Al₂O₃에 대해 더 강한 확실성을 기대할 수 없다는 의미다.

### 3.2 TiO₂ — 양이온 신호 + 광학 변화

Bharti et al. 2016 (Sci. Rep., `10.1038/srep32355`) **[측정]** 공기 플라즈마 처리로 TiO₂ 박막의 Ti³⁺와 산소공공이 **XPS로 확인**되며 처리시간 증가에 따라 증가, 밴드갭이 Fe-도핑 시료에서 3.22 → 3.00 eV로 적색 이동.

**[판단]** TiO₂의 증거 패키지 = **양이온 산화수 변화(XPS Ti³⁺) + 전자구조 변화(광학/밴드갭)**. §2.3에서 말한 전자 쪽 증거가 직접 관측되는 전형이다. 표면과학 쪽 표준 참조는 Diebold 2003 (Surf. Sci. Rep., `10.1016/s0167-5729(02)00100-0`)†.

### 3.3 철산화물

표준 참조는 Parkinson 2016 (Surf. Sci. Rep., `10.1016/j.surfrep.2016.02.001`)†. 산화수 변화(Fe³⁺/Fe²⁺)가 자명하게 접근 가능한 계라는 점에서 CeO₂·TiO₂와 같은 범주에 속한다 **[판단]**.

### 3.4 계산 기준선

- Hinuma 2018 **[측정]** 절연성·반도체성 산화물의 E_Ovac을 계열로 산출하고, 밴드갭·벌크 생성에너지·전자친화도가 강한 결정 인자임을 통계적으로 확인.
- Hinuma 2020 (`10.1021/acs.jpcc.0c00994`, `seed_set_v2_review.md`에서 확보) **[측정]** 접근가능 표면 중 최저 E_Ovac이 **θ-Al₂O₃ (201̄)에서 5.46 eV**, 비교 대상 β-Ga₂O₃ (101)은 3.04 eV. **최안정면 대비 감소분은 1.11 eV.**
- Kumar 2016 **[측정]** E_Ovac·work function을 "surface reducibility"로 조작화하고 C–H 활성화 에너지와 선형 상관.

**[판단]** 이 세 결과의 결합이 본 연구에 주는 실질적 정보는 두 가지다. ① θ상(전이 alumina) 표면의 산소 제거 비용은 5.46 eV로, 반응성 산화물 영역과 멀다. ② 그러나 **같은 물질 안에서 종결면만 바꿔도 1.11 eV가 움직인다** — 즉 "물질 전체의 환원성"이 아니라 "어떤 면·어떤 site인가"가 1 eV 규모의 차이를 만든다.

### 3.5 γ-Al₂O₃ 문헌과의 대조

| 증거 축 | CeO₂ | TiO₂ | **γ-Al₂O₃ (현 seed set 기준)** |
|---|---|---|---|
| 산소 제거 정량 (H₂ 소모 + H₂O 생성) | 있음 | 있음 | **없음** |
| 재산화 적정 / 가역성 | 있음 (OSC) | 있음 | **없음** |
| 전자 귀속 (양이온 or 결함상태) | Ce³⁺ (STM/DFT, XPS) | Ti³⁺ (XPS) | **원리적으로 양이온 신호 불가 + 결함상태 측정 전통 없음** |
| 격자 산소 반응 참여 (MvK, 동위원소) | 있음 | 있음 | **없음** |
| 산소 교환·이동성 | TPIE, 410 °C급 | 있음 | **있음** — Martin1996: 620 °C |
| 계산 E_Ovac | 낮음 | 낮음 | **5.46 eV (θ상)** |
| TPR 신호 | 있음 | 있음 | 있음 — **단 TCD 단독 (Jeong2020 SI Fig. 1)** |

**[판단]** γ-Al₂O₃ 쪽에서 채워진 칸은 **Tier B 두 개(교환·계산)와 Tier C 하나(TCD)**뿐이다. Tier A는 전부 비어 있다. 이것이 현 상태의 정확한 서술이다.

---

## 4. Framework 평가와 수정안 (질문 4)

### 4.1 현 framework의 문제

현재: `Processing → Structure → Oxygen behavior → Reducibility/Reactivity`

**[판단]** 네 가지 결함이 있다.

| # | 문제 | 왜 문제인가 |
|---|---|---|
| 1 | **"Reducibility/Reactivity"를 한 칸에 묶었다** | 가장 치명적. Joubert2006의 25 °C H₂ 활성화는 **reactivity이지만 reducibility가 아니다**(산소 제거 없음). 한 칸에 두면 "반응성이 있으므로 환원성이 있다"는 추론이 framework 자체에 내장된다 — 본 연구가 피하려는 바로 그 오류 |
| 2 | **"Oxygen behavior"가 세 현상을 뭉쳤다** | v2에서 Ammendola2011(OH 화학)과 Martin1996(격자 산소 교환)을 같은 [C]에 넣었는데 이 둘은 산소원이 다른 별개 현상이다. OH 화학 / 격자산소 이동 / 산소 제거를 분리해야 한다 |
| 3 | **선형 사슬이 site-specificity를 담지 못한다** | §1.2 — reducibility는 물질 속성이 아니라 site·계면 속성이다. 선형 사슬에는 "금속이 담지되었을 때 계면에서만 열리는 경로"를 넣을 칸이 없다. 그런데 Martin1996은 Rh가 있으면 교환온도가 200–300 °C 내려간다고, Ammendola2011은 금속이 WGS를 가속한다고 보고했다 |
| 4 | **종착점이 이분법을 유도한다** | §1.3 — 문헌의 조작적 정의는 E_Ovac이라는 연속량이다. "Reducibility"를 종착점에 두면 연구질문이 "환원되는가 예/아니오"로 축소된다 |

### 4.2 수정안 — 5축 + 2분기

```
[P] Processing / Pretreatment
      │   소성·환원·수열·진공·플라즈마·합성경로·전구체
      ▼
[S] Surface & defect structure
      │   Al 배위(IV/V/III) · OH 피복률·유형 · 종결면 · 양이온 공공(구조적)
      ▼
      ├────────────────────┬─────────────────────┬────────────────────┐
[O1] OH / 물 화학        [O2] 격자산소 이동      [O3] 산소 제거        │
     (산소원 = OH)            (수 보존, 교환)        (수 감소, 공공 생성)  │
      │                        │                      │               │
      ▼                        ▼                      ▼               │
[R1] Surface reactivity                      [R2] Reducibility        │
     H₂/CH₄ 활성화, Lewis 산염기,                  (MvK 의미: 산소 제거   │
     anchoring, WGS·spillover                     + 전자 귀속 + 가역성) │
      ▲                                            ▲                  │
      └──────── [I] Metal/oxide interface 경로 ─────┘                  │
                (담지 금속이 있을 때만 열리는 경로) ◄────────────────────┘
```

**핵심 변경 3가지**

1. **[R1]과 [R2]를 분리한다.** [R1](표면 반응성)과 [R2](환원성)는 서로를 함의하지 않는다. 현 seed set의 Joubert2006·Wischert2012는 [R1]의 강한 증거이고 [R2]의 증거가 아니다.
2. **[O]를 [O1]/[O2]/[O3]로 쪼갠다.** 산소원이 OH인지 격자인지, 산소 수가 보존되는지 감소하는지가 판별 기준이다. Ammendola2011 → [O1], Martin1996 → [O2], (현재 공석) → [O3].
3. **[I] 금속/산화물 계면을 별도 경로로 올린다.** 선형 사슬의 중간 단계가 아니라, [S]에서 분기해 [R1]·[R2] 양쪽으로 들어가는 **병렬 경로**다.

### 4.3 다른 경로의 가능성 (요청: "다른 경로가 있을 가능성도 확인")

**[판단]** 문헌을 읽은 결과, 본 연구의 목표를 달성하는 경로가 "bulk γ-Al₂O₃를 reducible하게 만든다" 하나가 아니다. 최소 네 가지 대안이 문헌에 이미 제안되어 있다.

| 경로 | 문헌 근거 | 본 연구에 주는 재구성 |
|---|---|---|
| **① 금속/산화물 계면** | RuizPuigdollers2017 **[저자해석]** *"Combining oxide nanostructuring with metal/oxide interfaces opens promising perspectives to turn hardly reducible oxides into reactive materials in oxidation reactions based on the Mars–van Krevelen mechanism."* 또한 계면 site에서 산소가 *"at much lower cost"*로 제거된다 | **가장 유망하고 가장 직접적이다.** 목표를 "reducible γ-Al₂O₃를 만든다"에서 ***γ-Al₂O₃/금속 계면에 산소가 싸게 빠지는 site를 만든다***로 재정의하면, 문헌이 이미 지지하는 경로가 된다. Jeong2020이 실제로 한 일(ceria/금속을 Al(V)에 고정)도 이 범주로 읽을 수 있다 |
| **② 종결면·나노구조 제어** | Hinuma2020 **[측정]** θ-Al₂O₃에서 접근가능 표면 간 E_Ovac 차 **1.11 eV**; RuizPuigdollers2017은 nanostructuring을 수단으로 명시 | facet·형태 제어로 E_Ovac을 1 eV 규모 낮출 수 있다는 계산적 여지. Liu2021(flower-like, Al(V) 풍부)이 이 범주의 실험 후보 |
| **③ 도핑·치환** | Kumar2016 **[측정]** 상관이 doped CeO₂·doped TiO₂·doped MgO를 포함; Deml2014 **[측정]** E_Ovac이 생성엔탈피·밴드갭으로 결정 | 도핑은 E_Ovac을 움직이는 확립된 수단. γ-Al₂O₃ 도핑 문헌은 현 seed set에 없음 → 탐색 대상 |
| **④ OH 매개 산소 공급** | Ammendola2011 **[측정]** OH가 산소원으로 CO₂·H₂ 생성; Amenomiya1978 (water-gas conversion on alumina) | **reducibility는 아니지만 "산소를 공급하는" 기능은 한다.** 연구의 실질 관심이 "산소를 내주는 alumina"라면 이 경로가 실제 답일 수 있다. 단 그때는 용어를 reducibility가 아니라 **OH-mediated oxygen transfer**로 바꿔야 한다 |

**[판단] ④가 특히 중요하다.** 프로젝트의 원래 관심사는 "unusually reactive 또는 potentially reducible γ-Al₂O₃"였다. 그런데 reducibility(§1.1 정의)와 defect-site Lewis 산염기 반응성(Wischert2012, Joubert2006)과 OH 매개 산소 전달(Ammendola2011)은 **서로 다른 세 현상이고, 증거 기준도 검색 어휘도 다르다.** 어느 것을 연구하는지 지금 결정하면 이후 query 설계가 완전히 달라진다. 이것은 과학적 선택이므로 지도교수와 논의할 사항으로 남긴다.

---

## 5. 증거 인정 기준 (이 단계의 실질 산출물)

전체 표는 `reducibility_evidence_criteria.csv`. 요약하면:

### Tier A — reducibility 증거로 **인정**

| ID | 요구 측정 | 확립하는 것 |
|---|---|---|
| **A1** | H₂(또는 CO) 소모와 **H₂O(또는 CO₂) 생성을 동시 정량**, 화학량 일치 | 격자 산소가 실제로 제거되었다 |
| **A2** | 1차 환원 후 **O₂ 재산화로 소모 산소량 적정** + 사이클 재현성 | 산소 결손이 생기고 되돌릴 수 있다 (OSC의 본질) |
| **A3** | 환원된 양이온 또는 **mid-gap 결함상태**를 XPS/XANES/EPR/광학으로 확인 | 산소와 함께 나간 전자의 귀속 |
| **A4** | **¹⁸O 라벨 격자 산소가 생성물에 출현** (MvK) | 그 산소가 실제 반응에 쓰였다 — **최강** |

> **인정 최소 조건**: **A1 + (A2 또는 A3)**. A4가 있으면 가장 강한 주장이 가능하다. A1 단독은 격자 산소인지 OH 유래인지 구분하지 못하므로 불충분하다.

### Tier B — **보조 지표** (단독으로는 reducibility 주장 불가)

| ID | 측정 | 말할 수 있는 것 | γ-Al₂O₃ 현황 |
|---|---|---|---|
| B1 | OSC류 산소 흡·방출량 | 용량 수준 | 측정 미발견 |
| B2 | ¹⁸O 교환 / CO 과도응답 | **이동성** 수준 (≠ 제거 용이성) | Martin1996: 620 °C |
| B3 | 계산 E_Ovac | 그 면의 산소 제거 비용 | Hinuma2020: θ상 5.46 eV |

### Tier C — reducibility 증거로 **불인정**

| ID | 유형 | 왜 불인정인가 |
|---|---|---|
| **C1** | **TCD 단독 TPR 피크** | H₂ 소모·H₂O 발생·탈수화를 구분 불가. **Jeong2020 SI Fig. 1이 여기 해당** |
| **C2** | H₂ 소모량 단독 | H₂ 해리·흡착·spillover로도 동일 신호 (Joubert2006, Kramer1979) |
| **C3** | Al 배위수·OH 변화 관측 | [S] 증거일 뿐. Al(V)는 양이온 배위상태이며 산소 결손이 아니다 |
| **C4** | ceria·Pt 등이 함께 있는 시료의 환원 신호 | alumina 자체로 귀속 불가. 금속은 교환·WGS를 수백 °C 가속 |
| **C5** | 산소 제거 없는 표면 반응성 | **[R1] 증거로는 유효하나 [R2] 증거가 아니다** |

**[판단]** 이 기준을 현 seed set에 적용하면: **Tier A 0건, Tier B 2건, Tier C 다수.** 즉 *현재 γ-Al₂O₃의 reducibility를 지지하는 Tier A 증거는 문헌에서 한 건도 확인되지 않았다.* 이것은 "없다"가 아니라 "아직 찾지 못했다"이며, Tier A 조건이 곧 다음 단계 검색의 표적이 된다.

---

## 6. 다음 단계에 주는 직접적 결과

### 6.1 검색 표적이 구체화되었다

Tier A 조건을 그대로 검색 표적으로 바꾸면:

| 표적 | 검색해야 할 어휘 |
|---|---|
| A1 | `"water formation"`, `"H2O evolution"`, `"mass spectrometry"` + `TPR` + alumina |
| A2 | `"reoxidation"`, `"oxygen uptake"`, `"redox cycle"`, `"oxygen storage capacity"` + alumina |
| A3 | `"defect state"`, `"mid-gap"`, `"F-center"`, `XANES`, `EPR` + (γ- OR transition) alumina |
| A4 | `"18O"`, `"isotopic labelling"`, `"Mars-van Krevelen"` + alumina |
| ① 계면경로 | `"metal/oxide interface"`, `"interface oxygen"`, `"perimeter site"` + alumina |
| ③ 도핑 | `"doped alumina"`, `"cation substitution"` + (`"oxygen vacancy"` OR `reducibility`) |

### 6.2 seed set에 대한 함의

**[판단]** `seed_set_v2_review.md`의 KEEP 18편은 이 기준에서도 유지된다. 단 역할 라벨을 바꿔야 한다.

| seed | v2 라벨 | 수정 라벨 |
|---|---|---|
| Joubert2006, Wischert2012 | [D′] 대안설명 | **[R1] 표면 반응성 — 양성 증거** (단순 '대안'이 아니라 독자적 현상) |
| Ammendola2011, Amenomiya1978 | [D] 출처·기원 | **[O1] OH 매개 산소 공급** |
| Martin1996 | [C] 직접측정 | **[O2] 격자산소 이동 (Tier B2)** |
| Hinuma2020, Carrasco2004 | [C] 계산 | **[O3] 산소 제거 비용 (Tier B3)** |
| Jeong2020 | [D] 주장 | **[R2] 주장 — Tier C1 (불인정)** |
| Kramer1979, Kalamaras2008 | [D′] | **[R1]/[I] — spillover·계면 경로** |

새로 추가할 후보는 이번 단계에서 확보한 reducibility 개념 문헌 중 **RuizPuigdollers2017**(계면 경로와 정의), **Esch2005**(환원의 2부 signature), **Madier1999**(세 측정군 병행 모범), **Kumar2016**(연속량 조작화) 4편이다. 이들은 γ-Al₂O₃ 논문이 아니므로 **reference-standard seed**(비교 기준군)로 별도 분류하는 것이 맞다 — known-item testing의 대상이 아니라 증거 기준의 근거다.

### 6.3 남은 한계

1. 18편 중 9편은 **초록을 열람하지 못했다**(§0). Ganduglia-Pirovano 2007과 Doornkamp 2000은 각각 산소공공·MvK의 표준 리뷰이므로, 기준을 확정 발표하기 전에 기관 접근으로 확인하는 것이 바람직하다.
2. Tier A의 "최소 조건(A1 + A2/A3)"은 ceria·titania 문헌의 관행에서 역산한 **나의 제안**이며, 이 조합을 명시적으로 요구한 guideline 문헌을 찾지는 못했다.
3. Al³⁺에 접근 가능한 저산화수 상태가 없다는 §2.3의 논거는 무기화학 일반 지식에 기반한 **나의 판단**이다. Al₂O₃ 격자 내 Al의 환원 상태를 다룬 1차 문헌을 찾지 못했으므로, 이 주장을 보고서에 쓸 때는 출처를 보강하거나 추론으로 표시해야 한다.

