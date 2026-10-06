# γ-Al₂O₃ Literature Search — Seed Set v1 구축
### Initial 4편 분석 → coverage/bias 진단 → gap 정의 → candidate 탐색 → 최종 seed set

**목적**: 논문을 많이 모으는 것이 아니라, 이후 검색식(query)을 시험할 수 있는 **대표성·다양성을 갖춘 소규모 seed set**을 만드는 것.
**방법론 근거**: `literature_methodology.md`의 결정 ③(known-item diagnostic)·④(citation chasing)
**서지 검증**: 본 문서에 등장하는 모든 논문은 OpenAlex에서 발견하고 **Crossref API로 대조 검증**했다 (21/21 통과). 서지 필드를 기억이나 추정으로 쓴 곳은 없다.

---

## 표기 규약 — 세 가지를 섞지 않는다

| 표기 | 의미 |
|---|---|
| **[측정]** | 논문이 실제로 측정·계산한 값 또는 관측 |
| **[저자해석]** | 저자가 그 측정으로부터 끌어낸 해석 |
| **[판단]** | seed 선정을 위한 **나의** 판단 — 논문의 주장이 아님 |

> ⚠ **본 문서 전체에 적용되는 금지 규칙**: Al(V), low-coordinate Al, oxygen vacancy가 보고되었다는 사실만으로 γ-Al₂O₃의 reducibility가 입증되었다고 간주하지 않는다. 아래 분석에서 각 논문이 **실제로 다루지 않은 고리는 공란으로 남긴다.**

---

## 1. Initial 4편 분석

연구 chain은 다음 네 고리로 본다.

```
[A] Processing condition → [B] Structural change → [C] Oxygen behavior → [D] Reducibility / Reactivity
```

---

### 1.1 Kwak 2007 — Al(V)가 표면에만 있다는 1차 근거

| 항목 | 내용 |
|---|---|
| DOI | `10.1016/j.jcat.2007.06.029` |
| Title | Penta-coordinated Al³⁺ ions as preferential nucleation sites for BaO on γ-Al₂O₃: An ultra-high-magnetic field ²⁷Al MAS NMR study |
| Year / Journal | 2007 / Journal of Catalysis 251, 189–194 |
| 연구그룹 | Pacific Northwest National Laboratory (PNNL) — J.H. Kwak, J.Z. Hu, D.H. Kim, J. Szanyi, C.H.F. Peden |
| γ-Al₂O₃의 역할 | **연구 대상 그 자체** (지지체의 표면 구조를 규명) |
| Synthesis / post-treatment | 상용 γ-alumina (200 m²/g, Condea). BaO는 incipient wetness로 담지 후 120 °C 건조 → **500 °C, 20% O₂/N₂, 2 h 소성**. Ba 담지량 0.5–20 wt% |
| 주요 characterization | 고체 ²⁷Al MAS NMR **21.1 T**, spinning 15 / 23 kHz; ²⁷Al 스핀-격자 완화시간(T₁) 측정 |

**[측정]**
- ~23 ppm에 Al(V) 신호가 분리되어 관측됨 (0 ppm = 팔면체 기준, ~59 ppm = 사면체).
- T₁: 사면체·팔면체 약 **120 ms**, penta는 **8 ms 미만**.
- Al(V) 분율: 23 kHz에서 **1.56 mol%**, 15 kHz에서 약 **3.3%** (spinning rate 의존).
- 2 wt% BaO 담지 시 잔존 Al(V) 1.56 → **0.92 mol%** (소모 0.64 mol%), 담지된 Ba량 **0.68 mol%**.
- 8%, 20% BaO에서 23 ppm 신호 거의 소멸. 23 ppm 세기는 BaO 담지량에 **선형** 감소.

**[저자해석]** Al(V)는 벌크 결함이 아니라 **표면에만** 존재하며, BaO가 이 자리에 1:1로 우선 anchoring한다. 이것이 γ-Al₂O₃가 활성상을 잘 분산시키는 이유일 수 있다. 다만 "이 현상의 일반성은 아직 확립되지 않았다"고 스스로 유보한다.

**chain 커버리지**

| [A]→[B] | [B]→[C] | [C]→[D] |
|---|---|---|
| ✅ 소성 500 °C 조건에서 Al(V) 표면 국재를 정량 | ⬜ **다루지 않음** | ⬜ **다루지 않음** |

추가로 [B]→반응성 고리를 BaO anchoring이라는 **화학적 반응성** 측면에서만 다룬다(산소 거동이 아님).

**seed로서의 중요성**: Al(V)의 표면 국재라는 전제의 1차 출처. 이후 모든 Al(V) 논의가 이 측정을 기준으로 삼는다.
**[판단]** 이 논문에서 논문이 인용한 선행 결과 중 주목할 것: Pecharroman 등이 **950 °C 이상 가열 시 Al(V) 신호가 완전히 소멸**한다고 보고했다는 서술 — 처리온도 상한을 정의하는 단서다(S16으로 연결).

---

### 1.2 Prins 2020 — 구조 논쟁의 정리, 그리고 'vacancy'의 정체

| 항목 | 내용 |
|---|---|
| DOI | `10.1016/j.jcat.2020.10.010` |
| Title | On the structure of γ-Al₂O₃ |
| Year / Journal | 2020 / Journal of Catalysis 392, 336–346 (**mini-review**) |
| 연구그룹 | ETH Zürich — Roel Prins (단독 저자) |
| γ-Al₂O₃의 역할 | **연구 대상 그 자체** (벌크 및 표면 구조) |
| Synthesis / post-treatment | 1차 실험 없음. boehmite(γ-AlOOH) / bayerite / gibbsite의 **탈수화 경로**를 문헌 기반으로 정리. 수증기압·입자크기·승온속도가 γ / η / χ 상 선택을 좌우 |
| 주요 method | 문헌 종합: XRD, 중성자 회절, ²⁷Al 및 **¹⁷O NMR**, DFT, TEM, SAED |

**[측정 — 원 문헌들의 값을 Prins가 종합]**
- 고해상 ²⁷Al NMR 3건에서 팔면체 Al 비율 **65%**, ¹⁷O NMR로부터 **62.5%**.
- → 양이온 공공의 약 **80%가 팔면체 위치(V_O)**. 구조식 **(Al_T)(Al_O)₅ᐟ₃(V_O)₁ᐟ₃(O)₄**.
- boehmite 탈수화 시 산소 음이온의 **25%** 손실, bayerite는 **50%**.
- TEM: (110) 표면은 원자적으로 평평하지 않고 나노스케일 (111) facet을 형성.

**[저자해석]** γ-Al₂O₃는 스피넬 구조 모델로 보는 것이 타당하고 non-spinel 모델은 재검토가 필요하다. 표면은 강하게 재구성된다.

> ⚠ **용어 경고 — 본 연구에서 가장 중요한 구분 [판단]**
> 이 논문의 "vacancy"는 **양이온 공공(cation vacancy, Al³⁺ 자리의 빈자리)**이며, γ-Al₂O₃의 스피넬형 구조가 Al:O = 2:3 화학량을 맞추기 위해 **정상적으로 보유하는 구조적 특성**이다.
> 이것은 환원으로 산소가 빠져나가 생기는 **산소 공공(oxygen vacancy)과 전혀 다른 개념**이다. 두 개념을 "defect"라는 한 단어로 묶으면 "γ-Al₂O₃는 원래 vacancy가 많으니 환원되기 쉽다"는 **잘못된 추론**이 만들어진다. 이 혼동을 차단하는 것이 이 seed의 주된 기능이다.

**chain 커버리지**

| [A]→[B] | [B]→[C] | [C]→[D] |
|---|---|---|
| ✅ 전구체·수증기압·승온속도 → 상·구조 (review 수준) | ⬜ **다루지 않음** | ⬜ **다루지 않음** |

---

### 1.3 Jeong 2020 — 본 연구의 motivation이 들어 있는 유일한 seed

| 항목 | 내용 |
|---|---|
| DOI | `10.1038/s41929-020-0427-z` |
| Title | Highly durable metal ensemble catalysts with full dispersion for automotive applications beyond single-atom catalysts |
| Year / Journal | 2020 / Nature Catalysis 3, 368–375 |
| 연구그룹 | KAIST — H. Jeong, O. Kwon, B.-S. Kim, J. Bae, S. Shin, H.-E. Kim, J. Kim, **H. Lee** (교신) |
| γ-Al₂O₃의 역할 | **지지체이지만, 그 표면을 의도적으로 개조하는 대상** |
| Synthesis / post-treatment | 상용 γ-alumina를 **H₂ pre-reduction(사전환원)으로 활성화** → `rAl₂O₃`. 이후 ceria 담지 → 금속(Pt/Pd/Rh) 함침(40–90 °C) → 500 °C 소성·환원 |
| 주요 method | ²⁷Al MAS NMR (**9.4 T / 400 MHz**), H₂-TPR (BELCAT-B, **MS + TCD**, Ar 250 °C 2 h 전처리 후 5% H₂/Ar, 10 °C/min, 800 °C까지), DRIFTS-CO, EXAFS/XANES, XPS, HAADF-STEM, XRD, BET, DFT(ceria 위 CO 진동수 한정) |

**[측정]**
- **Supplementary Fig. 1**: fresh γ-alumina의 H₂-TPR에서 TCD 신호가 **267 °C에서 큰 피크**, **661 °C에서 작은 피크**를 보임 (아래 캡션 원문 참조).
- 사전환원 **350 °C** 처리 후 ²⁷Al MAS NMR에 **Al(V) 피크가 나타남**; ceria 담지 후 그 피크가 사라짐 (Supplementary Fig. 7).
- BET: fresh 66.8 → 사전환원 후 64.1 → ceria 담지 후 46.8 m²/g.
- 잔존 Al(V) 수가 ceria 담지량과 **선형 상관**, 저담지에서 점유된 Al(V) 수 ≈ 담지된 Ce 수.
- XPS: CeO₂–rAl₂O₃ 및 ESC에서 Ce³⁺/Ce⁴⁺ 비가 CeO₂–Al₂O₃보다 **높음**.

**[저자해석]** — Supplementary Fig. 1 캡션 (원문): *"The peaks at 267 and 661 °C indicate the reduction of weakly coordinated surface aluminum and the reduction of strongly coordinated bulk aluminum, respectively."* 이 해석은 SI 참고문헌 **1, 2**를 근거로 제시된다. 본문에서는 *"A temperature of 350 ºC, at which the reduction of surface Al is complete, was chosen."* 라고 쓴다. 즉 **저자는 이 TCD 신호를 알루미늄 자체의 환원으로 해석한다.**

**[판단] — 이것이 왜 중요하고, 동시에 왜 검증이 필요한가**
1. 이 캡션은 본 연구 전체의 출발점이다. **"reducible γ-Al₂O₃를 만들면 200–300 °C에서 큰 H₂ 소모 신호가 나온다"**는 목표 관측이 바로 이 그림이다.
2. 그러나 이 그림이 보여주는 **측정**은 "H₂ 분위기에서 승온할 때 TCD 신호가 267 °C에서 최대가 된다"는 것뿐이다. TCD는 **종(species) 선택성이 없는** 검출기이므로, 이 신호 자체는 H₂ 소모·물 탈착·수산기 축합 등을 구분하지 못한다. 이 그림에는 H₂ 소모량의 정량값이나 MS 질량 추적이 함께 제시되어 있지 않다.
3. 따라서 `interpretation_level`은 **`author_interpretation`**이며, `measured_fact`는 "TCD 피크 267 / 661 °C"까지다. 이 구분을 유지하는 것이 Gate 2의 핵심 적용 사례다.
4. **SI 참고문헌 1 = Ammendola et al., Surf. Sci. 605, 1812–1817 (2011)** 이 이 해석의 출처다. → 이 논문은 반드시 seed에 포함해야 한다(S12). (SI 참고문헌 2 = Zheng et al., Appl. Catal. B 202, 51–63 (2017)로, LaFeO₃/CeO₂ 산소운반체 연구이며 alumina 특정 근거가 아니다.)

**chain 커버리지**

| [A]→[B] | [B]→[C] | [C]→[D] |
|---|---|---|
| ✅ H₂ 350 °C 사전환원 → Al(V) 생성 | ◐ **간접** — Al(V) → defective ceria, Ce³⁺ 증가. 단 이것은 **ceria의** 산소 거동이지 alumina의 산소 거동이 아니다 | ◐ **주장 있음** — H₂-TPR TCD 피크를 Al 환원으로 해석. 측정은 TCD 신호에 한정 |

---

### 1.4 Choi 2022 — 처리 축을 '환원'에서 '수열/OH'로 바꾼 대조군

| 항목 | 내용 |
|---|---|
| DOI | `10.1016/j.apcatb.2022.122325` |
| Title | Anchoring catalytically active species on alumina via surface hydroxyl group for durable surface reaction |
| Year / Journal | 2023 (online 2022-12-23) / Applied Catalysis B: Environmental 325, 122325 |
| 연구그룹 | KAIST — Y. Choi, G. Kim, J. Kim, S. Lee, J.-C. Kim, R. Ryoo, **H. Lee** (교신) |
| γ-Al₂O₃의 역할 | **지지체이자 표면 개조 대상** |
| Synthesis / post-treatment | γ-Al₂O₃를 Al(NO₃)₃·9H₂O + urea 수열합성(**100 °C, 24 h**) → 80 °C 건조 → **750 °C, 5 h 소성**. 이후 **10% H₂O/air 분위기에서 500 °C 또는 750 °C, 10 h 수열 전처리**(`500A`, `750A`). 그 다음 ceria(10/20/30 wt%) + Pt(1 wt%) 담지 → 500 °C 소성 → 500 °C 2 h, 10% H₂ 환원. 내구성 시험: **800 °C, 25 h, 10% H₂O** |
| 주요 method | **¹H MAS NMR**(400 MHz, 진공 250 °C 전처리), DRIFTS-CO, H₂-TPR(800 °C까지), HAADF-STEM/EDS, XRD, XPS, BET, CO 화학흡착 |

**[측정]** 수열 전처리 온도(500/750 °C)에 따라 표면 OH가 달라지고, bare alumina에서는 800 °C aging 후 ceria·Pt가 심하게 소결되나 전처리된 alumina에서는 표면 구조가 거의 변하지 않음.

**[저자해석]** 표면 OH기가 활성종의 anchoring site로 작동해 고온 내구성을 만든다.

**chain 커버리지**

| [A]→[B] | [B]→[C] | [C]→[D] |
|---|---|---|
| ✅ 수열 전처리 온도 → 표면 OH 생성 | ⬜ alumina에 대해서는 **다루지 않음** (ceria의 oxygen transfer는 서론에서 선행문헌으로만 언급) | ⬜ alumina의 환원은 **측정하지 않음** (H₂-TPR은 Ce/Pt 거동 평가에 사용) |

---

### 1.5 Initial 4편 종합 — chain 고리별 충족도

| 고리 | Kwak2007 | Prins2020 | Jeong2020 | Choi2022 |
|---|---|---|---|---|
| [A] Processing condition | 소성 500 °C | 전구체 탈수화 (review) | **H₂ 환원 350 °C** | **수열 10% H₂O 500/750 °C** |
| [B] Structural change | **Al(V) 표면 국재 정량** | 양이온 공공·표면 재구성 | Al(V) 생성 | 표면 OH 생성 |
| [C] Oxygen behavior | ⬜ | ⬜ (양이온 공공 ≠ 산소 공공) | ◐ ceria 한정 | ⬜ |
| [D] Reducibility / Reactivity | ◐ BaO anchoring | ⬜ | ◐ **TCD 해석** | ◐ 내구성 |

**결론 [판단]**: initial 4편은 **[A]→[B] 고리는 잘 덮지만, [B]→[C]와 [C]→[D] 고리는 사실상 비어 있다.** 전체 seed set에서 alumina 자체의 산소 거동을 측정한 논문은 **0편**이고, 환원 거동을 주장하는 근거는 **Supplementary 파일의 그림 1장**뿐이며 그 근거 논문조차 seed에 없다.

---

## 2. 현재 seed set의 coverage와 bias

### 2.1 축별 분포

| 축 | 현재 상태 | 진단 |
|---|---|---|
| **Publication period** | 2007, 2020, 2020, 2022 | 2007년 1편 외 전부 2020년 이후. **1970–2000년대 foundational 문헌 0편** |
| **Research group** | PNNL / ETH / **KAIST ×2** | 실질 3그룹. 4편 중 2편이 동일 교신저자(H. Lee) |
| **지역** | 미국 1, 스위스 1, 한국 2 | 유럽 실험·계산 커뮤니티(Lyon, IFP, Torino, Napoli) 부재 |
| **Experimental vs computational** | 실험 3, review 1, **primary computational 0** | Jeong2020의 DFT는 ceria 위 CO 진동수 계산으로, alumina 표면 계산이 아님 |
| **Treatment 종류** | 소성, 전구체 탈수화(review), **H₂ 환원**, **수열/steam** | 진공 열처리(vacuum activation), 탈수화 온도 시리즈, 합성경로 변화, 도핑 부재 |
| **Characterization** | ²⁷Al NMR ×2, ¹H NMR, H₂-TPR(TCD), DRIFTS-CO, EXAFS/XANES, XPS, STEM, XRD | **NMR 편중**. IR 중심 표면화학 부재, EPR·PL 등 결함 분광 부재, **동위원소 교환 부재**, 열분석 부재 |
| **Property** | Al 배위(Al(V)), 양이온 공공, 표면 OH | **oxygen vacancy 부재**, **oxygen mobility 부재**, Lewis 산점 정량 부재 |
| **Direct reducibility evidence** | Jeong2020 SI Fig. 1 **단 1건** (저자해석) | 1차 근거(Ammendola 2011) 부재, 반증·대안설명 문헌 **0편** |

### 2.2 이 4편만으로 seed set을 만들면 생기는 search bias

**[판단]** — known-item testing의 진단력이 다음 방향으로 왜곡된다.

1. **용어 편향 (가장 심각)** — seed의 어휘는 `penta-coordinated Al³⁺`, `Al³⁺penta`, `coordinatively unsaturated`, `surface hydroxyl`에 집중된다. 이 어휘로 수확한 query는 `oxygen vacancy`, `anion vacancy`, `F-center`, `lattice oxygen`, `oxygen mobility`, `isotopic exchange`, `hydrogen spillover`, `heterolytic splitting`, `Lewis acid–base pair`를 쓰는 문헌군을 **구조적으로 놓친다**. 그런데 [C]·[D] 고리의 증거는 바로 그 어휘를 쓴다.
2. **그룹·응용 편향** — 4편 중 2편이 KAIST, 그리고 3편이 '귀금속 분산/automotive TWC' 응용 프레임이다. query가 자동차 배가스 촉매 문헌으로 끌려가고, alumina 자체를 촉매로 다루는 문헌(Claus 반응, 알코올 탈수, 이성질화)이나 재료·세라믹 커뮤니티 문헌은 누락된다.
3. **방법 편향** — NMR 어휘(`MAS`, `chemical shift`, `T1`)가 과대 대표되어 IR·EPR·동위원소·열분석 문헌의 recall이 낮아진다.
4. **시대 편향** — 2020년 이후 편중으로, 표면 모델과 용어를 만든 1978–1996년 문헌이 검색식에 반영되지 않는다. 이들은 oxide 표면 용어의 **정의 출처**이므로 누락 비용이 크다.
5. **확증 편향 (evidence-type 편향)** — 모든 seed가 "Al(V)/OH = 좋은 anchoring site"라는 한 방향 서술을 공유한다. **Al(V)가 반응성의 주체가 아니라는 반대 증거**, 그리고 **저온 H₂ 신호를 환원이 아닌 것으로 설명하는 문헌**이 seed에 없다. 이 상태의 seed로 query를 만들면 가설을 지지하는 문헌만 잘 찾는 검색식이 만들어진다 — 본 프로젝트가 명시적으로 피하려는 실패 모드다.
6. **chain 편향** — [A]→[B]에 최적화된 query가 만들어지고, 정작 연구질문의 핵심인 [C]·[D] 고리는 검색식이 약한 상태로 고정된다.

---

## 3. 부족한 seed category (실제 분석에서 도출)

아래 category는 §1–2의 분석 결과에서만 도출했다. 일반적인 "오래된 논문이 없다" 류의 예시를 그대로 가져오지 않았다.

| ID | Category | 왜 필요한가 (근거) | 우선도 |
|---|---|---|---|
| **G1** | Foundational surface model (OH 유형·Lewis 산점·탈수화) | 2.2-(1)(4): 검색 어휘의 정의 출처가 seed에 없음 | 높음 |
| **G2** | Primary computational study of γ-Al₂O₃ surface/defect | 2.1: primary DFT 0편. 처리온도→OH 피복률→site 생성을 계산으로 잇는 기준 모델 부재 | 높음 |
| **G3** | alumina **자체**의 산소 제거·산소 이동 직접 측정 (TPR 정량, 동위원소 교환) | 1.5: [C] 고리 0편, [D]의 1차 근거 부재 | **최고** |
| **G4** | 결함 상태의 분광학적 검출 (EPR·PL·UV-vis) | 2.1: oxygen vacancy를 직접 보는 수단이 seed에 전무 | 중간 |
| **G5** | 처리온도 시리즈 × 구조 정량 | 1.1의 '950 °C에서 Al(V) 소멸' 단서가 seed 내부에 1차 근거 없이 남아 있음 | 높음 |
| **G6** | 합성 경로/전구체가 defect를 만드는 경우 | 2.1: 4편 모두 기성 alumina 후처리. '합성으로 만들 수 있는가'라는 분기 부재 | 중간 |
| **G7** | 반증·대안 설명 (비환원성, spillover, TPR 해석 오류) | 2.2-(5): 확증 편향 차단에 필수 | **최고** |
| **G8/G9** | H₂·CH₄가 alumina 표면에서 하는 일 (defect site 반응성) | 1.3-[판단]: 저온 H₂ 신호의 경쟁 가설이 필요 | **최고** |

---

## 4. Candidate seed paper 탐색

### 4.1 탐색 경로와 수확량

| 경로 | 구현 | 결과 |
|---|---|---|
| **Backward citation** | 4편의 `referenced_works` 합집합 (OpenAlex) | 190 레코드 |
| **Forward citation** | 4편을 인용한 문헌 (`cites:` 필터, 주제어 + 피인용 상위) | 151 레코드 |
| **Seed 내부 provenance 추적** | Jeong2020 **Supplementary 참고문헌 목록**에서 TCD 해석의 근거 2편을 직접 추출 | 2 레코드 (**가장 가치 높음**) |
| **Terminology 기반 검색 1차** | OpenAlex 기본 `search` (자연어 질의) | 150 레코드 — **대부분 무관** |
| **Terminology 기반 검색 2차** | `title_and_abstract.search` + Boolean 구문으로 전환 | 330 레코드 — 유효 후보 다수 |
| 합계 (중복 제거) | | **727 레코드** |

**[판단] 탐색 과정에서 얻은 방법론적 교훈 2개 — `literature_methodology.md` v2에 반영할 것**

1. **OpenAlex의 기본 `search`는 본 주제에 쓸 수 없다.** 자연어 질의(`"temperature programmed reduction alumina hydrogen consumption quantification"`)는 지구화학·수소경제·CO₂ 수소화 문헌으로 표류했다. 반면 필드 제한 Boolean(`title_and_abstract.search:(alumina OR "Al2O3") AND ("oxygen exchange" OR "18O")`)으로 바꾸자 목표 문헌이 즉시 상위에 올라왔다. → **결정 ③의 query 설계에서 "필드 제한 + 명시적 Boolean"을 기본형으로 고정해야 한다.**
2. **Supplementary 파일의 참고문헌 목록이 backward citation 경로에서 누락된다.** Jeong2020의 TCD 해석 근거인 Ammendola 2011은 본문 참고문헌이 아니라 **SI 참고문헌**에 있어서, OpenAlex의 `referenced_works`에 포함되지 않았다. 자동 citation chasing만으로는 **핵심 전제의 출처를 놓친다.** → 본 연구의 가장 중요한 주장이 SI에 근거할 경우 **SI 참고문헌 수동 확인을 절차로 넣어야 한다.**

### 4.2 Candidate 평가표

전체 21편의 평가는 `seed_candidates.csv`에 있다. 아래는 핵심 후보만 발췌한다 (diversity contribution 기준 — "좋은 논문인가"가 아니라 "이 논문을 seed에 넣으면 기존 4편으로는 닿지 않는 영역에 닿는가").

| Candidate | Year | Group | Study type | Treatment | Property / Evidence | Initial seeds와 다른 점 | Seed로 추가할 이유 | Verification |
|---|---|---|---|---|---|---|---|---|
| **Martin & Duprez** | 1996 | Martin, Duprez | exp. (¹⁸O₂/¹⁶O 온도프로그램 교환) | 200–900 °C 산소교환 | **[측정]** γ-Al₂O₃ 최대 교환속도 **620 °C**; 순위 CeO₂ 410 ≫ CeO₂–Al₂O₃ 480 ≈ MgO 490 > ZrO₂ 530 ≫ **γ-Al₂O₃ 620** ≫ SiO₂ 850 °C. Rh 담지 시 최대속도 온도 **200–300 °C 하강**(저자: Rh→지지체 산소 spillover) | 4편에 없는 **[C] 고리의 직접 측정**. 또한 alumina를 환원성 산화물과 **정량 비교** | γ-Al₂O₃의 격자 산소가 교환은 되지만 ceria보다 **210 °C 높은** 온도를 요구함을 수치로 고정. 동시에 "금속이 있으면 수백 °C 내려간다"는 교란 요인을 미리 경고 | Crossref 통과 `10.1021/jp9531568` |
| **Joubert et al.** | 2006 | Copéret · Sautet (Lyon/ETH) | DFT + IR/NMR | **500 °C 고진공** | **[측정]** H₂가 **약 25 °C**에서 Al(III)/Al(IV) defect와 반응해 Al(IV)–H, Al(V)–H 생성; H₂ 적정 defect 밀도 25 °C **0.043**, 150 °C **0.069 site/nm²** (OH는 4/nm²); CH₄는 100–150 °C에서 Al(III)에만 반응(0.030 site/nm²) | 4편 중 **H₂가 alumina 표면에서 무엇을 하는지** 다룬 논문이 없음 | **저온 H₂ 소모가 산소 제거 없이 일어날 수 있음**을 정량적으로 보임 → Jeong2020의 267 °C TCD 피크에 대한 **경쟁 가설**. 본 연구에서 가장 중요한 추가 | Crossref 통과 `10.1021/jp0641841` |
| **Wischert et al.** | 2012 | Copéret · Sautet | DFT + 분광 | **부분 탈수화, 최적 700 °C** | **[측정/계산]** (110) 면의 **tricoordinate Al(III)**가 'defect' site이며 N₂ 배위와 CH₄·H₂ heterolytic splitting을 담당. **(100) 면의 5배위 Al로는 관측된 반응성을 설명할 수 없다** | initial 4편의 **Al(V) 중심 서술과 정면 충돌** | Al(V) = 반응성 site라는 전제를 **반증**. 상충 증거를 seed 단계부터 내장해 확증 편향을 차단 | Crossref 통과 `10.1021/ja3042383` |
| **Ammendola et al.** | 2011 | Ammendola, Lisi 외 (Napoli) | exp. (TPR + IR) | TPR 승온 | alumina 자체의 CO 산화 기여를 TPR·IR로 분석 | **Jeong2020 SI Fig. 1 해석이 인용한 바로 그 문헌** | 본 연구 motivation의 **provenance**. 이것을 읽지 않으면 핵심 전제가 미검증으로 남는다 | Crossref 통과 `10.1016/j.susc.2011.06.018` ⚠ **closed access — 본 환경에서 전문 입수 불가** |
| **Kramer & Andre** | 1979 | Kramer, Andre | exp. | H₂ 노출 | alumina 상 **원자수소 흡착(hydrogen spillover)** | H₂ 흡수를 환원 이외로 설명하는 문헌이 4편에 없음 | 저온 H₂ 신호의 **또 다른 대안 설명**. 1970년대 문헌이라 현재 query로는 도달 불가 | Crossref 통과 `10.1016/0021-9517(79)90266-5` |
| **Digne et al.** | 2004 | IFP · Lyon (Digne, Raybaud, Sautet, Toulhoat) | **computational (DFT)** | 탈수화 온도별 OH 피복률 | (110)/(100) 표면의 OH 밀도와 산·염기 site를 열역학 모델로 연결 | **primary DFT 0편** 문제를 해결 | 처리온도 → 표면 OH 피복률 → site 생성의 계산적 **기준 모델**. 이후 DFT 문헌의 허브 | Crossref 통과 `10.1016/j.jcat.2004.04.020` |
| **Knözinger & Ratnasamy** | 1978 | Knözinger, Ratnasamy | exp./review | 탈수화 온도별 OH | 표면 OH 유형 분류, Lewis/Brønsted 산점 모델 | 1970년대 foundational — **검색 어휘의 정의 출처** | 이 논문의 어휘 없이는 1980–2000년대 문헌을 query로 끌어올 수 없다 | Crossref 통과 `10.1080/03602457808080878` |
| **Chen, Davis & Fripiat** | 1992 | Chen, Davis, Fripiat | exp. (²⁷Al NMR + 산성도) | transition alumina 열처리 | Al 배위수 ↔ **Lewis acidity** 상관 | Kwak2007보다 **15년 앞서** 같은 연결을 제시, PNNL과 독립 | "Al 배위–반응성 연결은 최근 발견"이라는 시대 편향을 교정 | Crossref 통과 `10.1016/0021-9517(92)90239-e` |
| **Morterra & Magnacca** | 1996 | Morterra, Magnacca (Torino) | exp. (**IR 중심**) | calcination/dehydration 온도 | 표면 OH·산점의 IR 지문 | 4편은 NMR·TPR 중심 — **IR 기반 표면화학 전무** | characterization 축을 IR로 확장. IR 문헌은 NMR 어휘로 검색되지 않음 | Crossref 통과 `10.1016/0920-5861(95)00163-8` |
| **Ingram-Jones et al.** | 1996 | Ingram-Jones, Slade 외 | exp. (열분석/구조) | **gibbsite vs boehmite, soak vs flash 가열** | 전구체·가열방식별 탈수화 경로 차이 | Prins2020은 review 수준으로만 언급 — 1차 데이터 없음 | 전구체 × 가열방식이라는 treatment 축을 1차 문헌으로 확보 | Crossref 통과 `10.1039/jm9960600073` |
| **Liu et al.** | 2021 | Liu, Yang 외 | exp. | **합성 경로 제어** | 불포화 pentacoordinate Al³⁺가 풍부한 구조 안정화 | 4편 모두 **기성 alumina 후처리** — 합성으로 Al(V)를 만든 사례 없음 | '후처리로 만드는가 / 합성으로 만드는가' 분기를 seed에 포함 | Crossref 통과 `10.1016/j.apcatb.2021.120171` |
| **Kwak et al.** | 2008 | PNNL | exp. (²⁷Al NMR) | **고온 상전이 영역** | Al(V)의 고온 상전이 역할 | Kwak2007과 같은 그룹이나 **온도축을 상한까지 확장** | §1.1의 '950 °C에서 Al(V) 소멸' 단서에 1차 근거를 부여 | Crossref 통과 `10.1021/jp802631u` |
| Shablonin et al. | 2021 | Lushchik 외 (Tartu) | exp. (광학/EPR) | 중성자 조사 + 열처리 | **α-Al₂O₃ 단결정의 dimer F center (산소 공공)** | 물질(α상)·커뮤니티(조사손상·세라믹)가 모두 다름 | **core 부적합** — 단, query precision을 시험하는 **boundary probe**로는 유용 | Crossref 통과 `10.1016/j.jnucmat.2020.152600` |

### 4.3 G4(결함 분광)에서 발견한 구조적 사실 — [판단]

`oxygen vacancy` / `F-center` / `EPR` 어휘로 alumina를 검색하면 상위 결과가 거의 전부 **중성자 조사된 α-Al₂O₃ 단결정 또는 세라믹**의 방사선 손상 문헌이다(핵재료·광학 커뮤니티). 즉:

> **γ-Al₂O₃ 촉매 커뮤니티에는 '산소 공공'을 분광학적으로 직접 측정한 문헌 전통이 사실상 없고, 대신 'Al 배위수'와 'OH기'로 결함을 기술한다.** 산소 공공을 직접 보는 전통은 다른 물질상·다른 커뮤니티에 존재한다.

이것은 본 연구의 중요한 중간 결론이자 gap이다. 다만 **"γ-Al₂O₃에 산소 공공이 없다"는 뜻이 아니라 "그 측정 전통이 없다"는 뜻**이다. 두 진술을 혼동해서는 안 된다. 따라서 α상 문헌은 core seed에서 제외하되, 검색식이 이 경계를 넘어 표류하는지 확인하는 precision 시험용으로만 남긴다.

### 4.4 제외한 후보와 사유

| 제외 | 사유 |
|---|---|
| Kwak 2009 (Science, `10.1126/science.1176745`) | 개념(Al(V) anchoring)·그룹(PNNL) 모두 Kwak2007과 중복. 피인용은 매우 높으나 coverage 추가 없음 |
| Trueba & Trasatti 2005 | review 역할이 Prins2020·Knözinger1978과 중복 |
| Soled 1983 | γ-Al₂O₃를 defect oxyhydroxide로 보는 모델 — Prins2020이 이 논쟁을 이미 평가 |
| Samain 2014 / Kovarik 2014 | 구조 정밀화 축이 Prins2020과 중복 (Kovarik은 PNNL 그룹 중복도 추가) |
| Pigeon 2021 (`10.1016/j.jcat.2021.11.011`) | Digne2004와 동일 연구 계보(IFPEN). **단, 최신 표면 모델이 필요해지면 v2 보강 1순위** |
| Cholewinski 2018 / Dixit 2018 | defect reactivity 축이 Joubert2006·Wischert2012와 중복 |

---

## 5. 최종 seed set 제안 (16편)

편수를 미리 고정하지 않고, §2.1의 각 축에 빈 칸이 남지 않는 최소 조합을 구성한 결과 **16편**이 되었다. 전체 표는 `seed_set_final.csv`.

### 5.1 유지 — initial 4편 (전부 유지)

| ID | 논문 | 왜 이 논문이 필요한가 (한 문장) |
|---|---|---|
| **S1** | Kwak 2007 | Al(V)가 표면에만 존재한다는 1차 근거이므로, 빠지면 structure 축의 기준점 자체가 사라진다. |
| **S2** | Prins 2020 | 'vacancy'가 **양이온** 공공이지 산소 공공이 아님을 못박아 주는 구조 기준으로, 본 연구에서 가장 위험한 용어 혼동을 차단한다. |
| **S3** | Jeong 2020 | 재현 목표인 Supplementary Fig. 1(267 / 661 °C TCD)을 담고 있어 본 연구의 motivation 그 자체다. |
| **S4** | Choi 2022 | 처리 방식을 '환원'이 아닌 '수열·OH 생성'으로 바꾼 동일 그룹 내 대조군으로, treatment 축의 두 번째 분기를 담당한다. |

### 5.2 추가 — 12편

| ID | 논문 | DOI | 왜 이 논문이 필요한가 (한 문장) |
|---|---|---|---|
| **S5** | Knözinger & Ratnasamy 1978 | `10.1080/03602457808080878` | 표면 OH·산점 어휘의 정의 출처로, 이 어휘 없이는 1980–2000년대 문헌을 query로 끌어올 수 없다. |
| **S6** | Chen, Davis & Fripiat 1992 | `10.1016/0021-9517(92)90239-e` | Al 배위–반응성 연결이 2007년 이후의 발견이라는 시대 편향을 독립 그룹의 선행 근거로 교정한다. |
| **S7** | Morterra & Magnacca 1996 | `10.1016/0920-5861(95)00163-8` | characterization을 IR로 확장해, NMR 어휘로는 도달하지 않는 분광 문헌군의 입구를 연다. |
| **S8** | Digne et al. 2004 | `10.1016/j.jcat.2004.04.020` | 처리온도 → 표면 OH 피복률 → site 생성을 계산으로 연결하는 유일한 기준 모델이다. |
| **S9** | Joubert et al. 2006 | `10.1021/jp0641841` | 저온 H₂ 소모가 **산소 제거 없이** 일어날 수 있음을 정량적으로 보여, S3의 TCD 해석에 대한 경쟁 가설을 제공한다. |
| **S10** | Wischert et al. 2012 | `10.1021/ja3042383` | (100)면 Al(V)로는 반응성을 설명할 수 없다고 보고해, seed set의 지배적 전제를 반증하는 축을 담당한다. |
| **S11** | Martin & Duprez 1996 | `10.1021/jp9531568` | alumina 격자 산소의 이동성을 직접 측정한 유일한 seed이며, 금속에 의한 spillover 교란도 함께 정량한다. |
| **S12** | Ammendola et al. 2011 | `10.1016/j.susc.2011.06.018` | S3의 'surface Al 환원' 해석이 인용한 근거 문헌이므로, 전제의 provenance 추적에 반드시 필요하다. |
| **S13** | Kramer & Andre 1979 | `10.1016/0021-9517(79)90266-5` | H₂ 흡수를 환원이 아닌 spillover로 설명하는 고전 근거로, 반증 경로를 확보한다. |
| **S14** | Ingram-Jones et al. 1996 | `10.1039/jm9960600073` | 전구체 × 가열방식(soak/flash) 축을 1차 실험으로 담당한다(S2는 review 수준에서만 언급). |
| **S15** | Liu et al. 2021 | `10.1016/j.apcatb.2021.120171` | Al(V)를 후처리가 아니라 **합성**으로 만드는 경로를 담당한다(나머지 15편은 모두 후처리 계열). |
| **S16** | Kwak et al. 2008 | `10.1021/jp802631u` | 처리온도를 상전이까지 밀었을 때 Al(V)가 어떻게 되는지를 담당해 온도축의 상한을 정의한다. |

### 5.3 선택적 — boundary probe (core 아님)

| ID | 논문 | 용도 |
|---|---|---|
| (B1) | Shablonin et al. 2021, `10.1016/j.jnucmat.2020.152600` | **recall 시험용이 아니라 precision 시험용.** query가 α-Al₂O₃ 조사손상 문헌으로 표류하는지 확인하는 경계 탐침. 포함 여부는 query 1차 시험 후 결정. |

---

## 6. 각 seed가 담당하는 coverage

### 6.1 Chain 고리별

| 고리 | 담당 seed | 상태 |
|---|---|---|
| **[A] Processing → [B] Structure** | S1 (소성), S2 (전구체, review), S3 (H₂ 환원), S4 (수열), S8 (탈수화 온도, 계산), S14 (전구체×가열방식), S15 (합성경로), S16 (고온 상전이) | 충분 |
| **[B] Structure → surface reactivity** | S5, S6, S7 (OH·Lewis 산점), S9, S10 (defect site의 H₂·CH₄ 반응성) | 충분 |
| **[C] Oxygen behavior** | **S11 단 1편** (¹⁸O 교환) | ⚠ **얇음 — 본 연구의 최대 취약점** |
| **[D] Reducibility claim** | S3 (TCD 해석), S12 (그 출처) | ⚠ 얇음 |
| **[D'] 반증·대안 설명** | S9 (H₂ heterolytic splitting), S10 (Al(V) 반증), S13 (spillover), S11 (금속 유도 spillover) | 확보 |

### 6.2 축별 충족 확인

| 축 | 담당 |
|---|---|
| Period | 1978 · 1979 · 1992 · 1996 ×2 · 2004 · 2006 · 2007 · 2008 · 2011 · 2012 · 2020 ×2 · 2021 · 2023 → 1970년대부터 2020년대까지 연속 |
| Group | 13개 독립 그룹 (Knözinger/Ratnasamy, Kramer, Chen–Fripiat, Morterra–Magnacca, Ingram-Jones/Slade, Martin–Duprez, IFP·Lyon(Digne), Copéret–Sautet ×2, PNNL ×2, Ammendola–Lisi, ETH(Prins), KAIST ×2, Liu) |
| Study type | 실험 11, 계산+실험 2, 순수 계산 1, review 1, 실험(열분석) 1 |
| Treatment | 소성 · 전구체 탈수화 · 가열방식(soak/flash) · H₂ 환원 · 수열(steam) · 고진공 열처리 · 부분 탈수화(700 °C) · 고온 상전이 · 합성경로 · TPR 승온 · H₂ 노출 · 산소교환 |
| Characterization | ²⁷Al NMR · ¹H NMR · ¹⁷O NMR(S2 경유) · IR/DRIFTS · DFT · H₂-TPR(TCD) · **¹⁸O 동위원소 교환** · H₂ 적정 · 열분석 · XRD/TEM · XPS/EXAFS |
| Property | Al 배위(IV/V/VI) · tricoordinate Al(III) · 양이온 공공 · 표면 OH · Lewis 산·염기쌍 · **격자 산소 이동성** · H₂ 해리 · 환원 신호 |
| Evidence type | 구조만 5 · 표면화학 3 · defect 반응성 3 · **산소 거동 직접 1** · 환원 주장 2 · 대안설명 2 |

### 6.3 이 seed set이 known-item testing에서 할 일

**[판단]** 16편은 서로 다른 어휘 영역에 흩어져 있으므로, query가 이들을 모두 검색해내지 못할 것이 거의 확실하다. 그것이 의도다. `literature_methodology.md` §4.2의 원인 코드로 미검출 seed를 진단하면 다음을 기대한다.

| 예상 미검출 seed | 예상 원인 코드 | 기대되는 교정 |
|---|---|---|
| S5, S13 (1978·1979) | `COVERAGE` 또는 `FIELD` (구 문헌의 abstract 미색인) | citation chasing 의존 확정, query로는 포기 |
| S11 (¹⁸O 교환) | `TERM` | `isotopic exchange`, `lattice oxygen`, `oxygen mobility` 어휘 추가 |
| S9, S10 (heterolytic splitting) | `TERM` | `heterolytic`, `Lewis acid-base pair`, `tricoordinate` 어휘 추가 |
| S13 (spillover) | `TERM` | `hydrogen spillover` 어휘 추가 |
| S15 (합성경로) | `TERM` | 형태·합성 어휘 추가 |
| S12 (Ammendola) | `TYPE`/`COVERAGE` | Surface Science 계열 색인 확인 |

즉 이 seed set의 설계 목적은 **"query가 잘 찾는 것을 확인"하는 것이 아니라 "query가 어디서 실패하는지 드러내는 것"**이다.

---

## 7. 이번 단계에서 확정하지 않은 것 / 다음 단계

1. **S12 (Ammendola 2011)의 내용 검증 미완** — closed access로 본 환경에서 전문을 받을 수 없었다. 서지는 Crossref로 검증했으나 **내용은 미확인**이다. 기관 접근으로 입수해 "alumina의 TPR 피크를 무엇으로 귀속했는지, H₂ 소모를 정량했는지"를 확인해야 한다. 이것이 확인되기 전까지 "γ-Al₂O₃가 환원된다"는 주장은 **`unverified`로 격리**된다.
2. **S3의 TCD 해석 재검토** — 267 °C 피크가 H₂ 소모인지(환원), H₂ 해리·흡착인지(S9), spillover인지(S13), 혹은 탈수·수산기 축합인지 구분하려면 MS 질량 추적 또는 H₂ 소모 정량이 필요하다. 이는 문헌에서 찾을 질문 목록에 올린다.
3. **G4(결함 분광) seed 공석** — γ-Al₂O₃ 촉매 문헌에 해당 전통이 없다는 §4.3의 관찰 때문에 의도적으로 비워 두었다. 전면 수집 단계에서 `EPR` + `γ-alumina` + `catalysis` 조합을 다시 시도해 공석이 실제인지 재확인한다.
4. 본 단계에서는 **γ-Al₂O₃ 문헌의 대량 수집을 수행하지 않았다.** 다음 단계는 이 16편으로 query v1을 시험하는 known-item diagnostic이다.

