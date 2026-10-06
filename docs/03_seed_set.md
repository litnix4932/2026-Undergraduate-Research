# Seed set

> **요약**
> - **seed**는 이미 알고 있는 핵심 논문이다. 검색식이 이 논문들을 찾아내는지로 query의 결함을 진단한다(known-item testing).
> - 현행 seed set은 **v2: KEEP 18 / OPTIONAL 9 / REMOVE 6**(총 33편)이다. query 시험에는 KEEP + OPTIONAL **27편**(core 21, boundary 6)을 쓴다.
> - v1(16편)은 초기 4편의 편향을 고치려고 만들었다. v2는 Ammendola 2011 원문 검증 이후 산소 거동·반증 문헌을 보강해 재분류했다.
> - seed set의 목적은 query가 잘 찾는 것을 확인하는 것이 아니라 **어디서 실패하는지 드러내는 것**이다.
>
> 라벨은 [README](../README.md#표기) 참조. framework 노드([P], [S], [O1]…)는 [02_evidence_framework.md §2](02_evidence_framework.md#2-연구-framework)에 정의되어 있다. 모든 논문은 Crossref로 서지를 검증했다.
>
> 데이터: [`seed_set_v2.csv`](../data/seed_set_v2.csv)(현행), [`seed_set_v1_final.csv`](../data/seed_set_v1_final.csv)(v1), [`seed_candidates.csv`](../data/seed_candidates.csv)(v1 후보 평가)

---

## 1. 초기 4편과 그 편향

출발점은 아래 4편이었다.

| 논문 | 핵심 내용 |
|---|---|
| **Kwak 2007** (J. Catal. 251, 189; `10.1016/j.jcat.2007.06.029`; PNNL) | 상용 γ-alumina(200 m²/g)에 BaO 담지 후 500 °C 소성. **[측정]** ²⁷Al MAS NMR(21.1 T)에서 ~23 ppm에 **Al(V)** 신호를 분리했다(0 ppm = 팔면체, ~59 ppm = 사면체). Al(V)의 T₁(스핀–격자 완화시간)은 8 ms 미만으로, 사면체·팔면체의 약 120 ms보다 훨씬 짧다 → 표면에 있음. 분율은 23 kHz 회전에서 1.56 mol%, 15 kHz에서 약 3.3%로 회전속도에 의존한다. BaO 2 wt% 담지 시 Al(V)가 1.56 → 0.92 mol%로 줄고(소모 0.64), 담지 Ba는 0.68 mol%다. 8·20 wt%에서는 신호가 거의 사라진다. **[저자해석]** Al(V)는 **표면에만** 있고, BaO가 1:1로 우선 고정(anchoring)된다. 일반성은 저자 스스로 유보했다. 인용된 Pecharroman 등에 따르면 950 °C 이상에서 Al(V)가 소멸한다 |
| **Prins 2020** (J. Catal. 392, 336; `10.1016/j.jcat.2020.10.010`; mini-review) | **[측정 종합]** 팔면체 Al 비율은 ²⁷Al NMR로 65%, ¹⁷O NMR로 62.5%다. 양이온 공공의 약 80%가 팔면체 자리에 있다. 탈수화 시 산소 손실은 boehmite 25%, bayerite 50%다. (110)면에는 나노 (111) facet이 생긴다. **[저자해석]** spinel 모델이 타당하다. **여기서 "vacancy"는 양이온 공공이다**([02 §6](02_evidence_framework.md#6-사슬-고리별-증거-감사)) |
| **Jeong 2020** (Nat. Catal. 3, 368; `10.1038/s41929-020-0427-z`; KAIST) | γ-alumina를 H₂로 **사전환원**(350 °C)한 rAl₂O₃ 위에 ceria와 Pt/Pd/Rh를 담지했다. **[측정]** 사전환원 후 Al(V) 피크가 나타나고, ceria 담지 후 사라진다. 잔존 Al(V)는 ceria 담지량과 선형이다. BET 비표면적은 66.8 → 64.1 → 46.8 m²/g다. Ce³⁺/Ce⁴⁺ 비가 증가한다. NMR은 9.4 T다. **연구 동기인 SI Fig. 1(267/661 °C TCD 피크)** 검증은 [02 §4](02_evidence_framework.md#4-사례-인용이-주장을-지지하지-않는다) |
| **Choi 2022** (Appl. Catal. B 325, 122325, 2023 게재; `10.1016/j.apcatb.2022.122325`; KAIST) | 수열합성 γ-Al₂O₃(750 °C 소성)를 10% H₂O/air, 500 또는 750 °C, 10 h로 **수열 전처리**한 뒤 ceria·Pt를 담지했다. **[측정]** 전처리 온도에 따라 표면 OH가 달라진다. 800 °C, 25 h, 10% H₂O aging 후 전처리 시료는 소결이 억제되었다(¹H MAS NMR 등). **[저자해석]** 표면 OH가 anchoring site 역할을 한다 |

**[판단] 이 4편의 coverage와 편향**
- **고리 coverage**: [P]→[S]는 잘 덮는다. 그러나 alumina **자체의 산소 거동**을 측정한 논문은 0편이다. 환원 주장의 근거는 SI 그림 1장뿐이었고, 그 근거 논문조차 seed에 없었다.
- **어휘 편향 (가장 심각)**: seed 어휘가 `penta-coordinated`, `surface hydroxyl`에 몰려 있다. 그래서 `oxygen vacancy`, `lattice oxygen`, `isotopic exchange`, `spillover`, `heterolytic` 같은 어휘를 쓰는 산소 거동 문헌을 구조적으로 놓친다.
- **그룹·응용 편향**: 4편 중 2편이 같은 교신저자(KAIST)다. 3편이 자동차 배가스 촉매 프레임이다.
- **방법 편향**: NMR에 편중되어 있다. IR, EPR, 동위원소, 열분석 문헌이 없다.
- **시대 편향**: 표면 용어의 정의 출처인 1978–1996년 문헌이 없다.
- **확증 편향**: 모든 seed가 "Al(V)/OH = 좋은 anchoring site"라는 한 방향 서술을 공유한다. 반대 증거와 대안 설명이 없다.

## 2. 후보 탐색

| 경로 | 결과 |
|---|---|
| BWC: 4편의 참고문헌 (OpenAlex) | 190 |
| FWC: 4편을 인용한 문헌 | 151 |
| **Jeong 2020 SI 참고문헌 직접 확인** | 2 (가장 가치 높음 — Ammendola 2011) |
| 자연어 검색 (OpenAlex `search`) | 150, 대부분 무관 |
| 필드 제한 Boolean 검색 | 330 |
| 합계 (중복 제거) | 727 |
| v2 추가: 기존 인용망과 **분리된** 독립 검색 8축 | 아래 표 |

**v2 독립 검색의 결과 자체가 발견이다 [판단].**
- 맨 alumina의 H₂-TPR을 주제로 한 문헌은 유효 결과가 5건뿐이었다.
- Al(V)↔산소공공 관계를 다룬 문헌도 결과 수가 매우 적었다.
- 반대로 "alumina + 산소공공"으로 검색하면 (i) 조사손상된 α상 세라믹과 (ii) 산소공공을 CeO₂·TiO₂에서 빌려온 담지촉매 문헌이 결과를 채운다.

| 검색 축 | 확보 |
|---|---|
| ¹⁸O 교환 | Martin1996 재검출. 나머지는 지구화학·운석 → 촉매 분야에서 희소 |
| 산소공공 생성에너지 | Carrasco2004, Hinuma2020 |
| 맨 지지체 TPR | 유효 5건 |
| dehydroxylation·물 탈착 | 직접 해당 문헌 희소 |
| OH 기반 WGS | Olympiou2007, Kalamaras2008, Serre1993 |
| spillover | Kramer1979 재검출, Shi2020 |
| Al(V)↔산소공공 | Wang2022, Ishizaki2003 |
| 환원 열역학 | Ostrovski2010 |

## 3. v2 분류

**기준은 하나다:** known-item testing에서 이 논문이 다른 논문으로 대체되지 않는 고유한 진단 역할을 갖는가.

### KEEP — 18편

| 논문 | 노드 | 고유 역할 / 핵심 측정 |
|---|---|---|
| Kwak 2007 | [P]→[S] | Al(V) 표면 국재의 1차 측정 |
| Prins 2020 | [S] | 양이온 공공 ≠ 산소공공 — 용어 혼동 차단 |
| Jeong 2020 | [P]→[S], [R2] 주장 (Tier C1) | 연구 동기 + 인용 불일치 사례 |
| Knözinger 1978 | [S] | 표면 OH 유형과 Lewis/Brønsted 산점 모델 — 검색 어휘의 정의 출처 |
| Morterra 1996 | [S] | **IR** 기반 표면화학. 전이 alumina의 CO 반응은 400 °C 이상에서 시작 |
| Digne 2004 | [P]→[S] (DFT) | 처리 온도 ↔ 표면 OH 피복률의 계산 기준 모델 |
| **Joubert 2006** | **[R1]** | H₂가 **약 25 °C**에서 Al(III)/Al(IV) 결함과 반응해 Al–H를 만든다. 결함 밀도는 25 °C에서 0.043, 150 °C에서 0.069 site/nm²(OH는 4/nm²). CH₄는 100–150 °C에서 Al(III)에만 반응(0.030 site/nm²) → **산소 제거 없는 H₂ 소모** |
| **Wischert 2012** | **[S]→[R1]** | 반응성 site는 (110)면의 3배위 **Al(III)**이며, 부분 dehydroxylation(최적 700 °C)으로 생긴다. (100)면 Al(V)로는 반응성을 설명할 수 없다 → Al(V) 전제의 **반증** |
| **Martin 1996** | **[O2]** (Tier B2) | ¹⁸O 교환 최대속도 온도: CeO₂ 410 ≫ CeO₂–Al₂O₃ 480 ≈ MgO 490 > ZrO₂ 530 ≫ **γ-Al₂O₃ 620** ≫ SiO₂ 850 °C. Rh 담지 시 200–300 °C 하강 |
| **Ammendola 2011** | **[O1]** | 인용 근거의 실제 내용 — OH의 WGS, Al 환원 아님 |
| Kramer 1979 | [R1]/[I] | spillover에 의한 alumina 상 원자수소 흡착 |
| **Amenomiya 1978** | **[O1]** | alumina 자체의 water-gas conversion (formate 중간체) |
| **Kalamaras 2008** | **[R1]/[I]** | **SSITKA**(정상상태에서 반응물을 동위원소로 갑자기 바꿔 표지 원자 흐름을 추적하는 기법)-DRIFTS-MS로 Pt/γ-Al₂O₃ WGS의 OH/H 이동을 추적 |
| **Hinuma 2020** | **[O3]** (Tier B3) | θ-Al₂O₃ (201̄) E_Ovac 5.46 eV |
| **Carrasco 2004** | **[O3]** (Tier B3) | MgO·CaO·α-Al₂O₃·ZnO의 공공 생성·이동장벽 비교 |
| **Shi 2020** | [P]→[O3] 주장 | H₂/O₂ **플라즈마**로 표면 산소공공을 증감시켰다고 주장. OH가 spillover를 촉진 |
| **Ostrovski 2010** | [O3] 기준선 | 벌크 alumina를 실제로 환원하는 조건(탄소열 환원 → Al₄C₃, Al·Al₂O 증기) |
| **Wang 2022** | 주장 패턴 | Al(V) + 산소공공 + spillover를 한데 묶은 주장 → 증거가 아니라 **검증 대상** |

굵은 11편이 산소 거동·반증 영역의 보강분이다. 이 영역에서 **산소 관련 측정을 가진 seed가 1편 → 6편**으로 늘었다.

### OPTIONAL — 9편

| 논문 | 유보 사유 |
|---|---|
| Choi 2022 | Jeong 2020과 같은 그룹이고 산소 거동 기여가 0이다. 단 `hydrothermal`, `aging`, `durability` 어휘가 고유하다 |
| Chen 1992 | Al 배위 ↔ Lewis 산성 연결의 선행 근거(Kwak보다 15년 앞섬)이나 Knözinger·Morterra와 부분 중복 |
| Ingram-Jones 1996 | 전구체(gibbsite/boehmite) × 가열방식(soak/flash) 축. [P]→[S]가 이미 과포화 |
| Liu 2021 | **합성**으로 Al(V) 풍부 구조를 만든 유일 사례. 합성 어휘가 고유 |
| Ishizaki 2003 | 조사손상이 아닌 EPR 경로이나 시료가 sol–gel 박막 |
| Föttinger 2008 | 표지 CO/CO₂ 분광으로 carbonate가 지지체 OH 경로로 생김을 확정. Ammendola·Kalamaras와 메시지 중복 |
| Serre 1993 | CO-TPR → WGS 귀속의 초기 관측. Ammendola에 요약 인용됨 |
| Haneda 2000 | OH → H₂ 직접 증거이나 Ga₂O₃–Al₂O₃ 혼합 산화물 |
| Shablonin 2021 (CSV 키 `Shablonin2020`) | 중성자 조사 α-Al₂O₃의 dimer F-center. **precision 탐침**(query가 엉뚱한 분야로 표류하는지 확인용)으로만 사용 |

### REMOVE — 6편

| 논문 | 사유 |
|---|---|
| Kwak 2008 (v1 seed S16) | [P]→[S] 과포화 + PNNL 그룹 중복 |
| Kwak 2009 (Science) | Kwak 2007과 개념·그룹 중복 |
| Arrouvel 2004 | Digne 2004와 그룹·방법·메시지 동일 |
| Dropsch 1997 | Ammendola·Föttinger가 더 직접적 |
| Olympiou 2007 | 같은 그룹의 Kalamaras 2008로 대체 |
| Iordan 2004 | Ammendola의 기전 논의에 흡수 |

v1 단계에서 후보로만 보고 제외한 문헌도 있다: Trueba 2005, Soled 1983, Samain 2014, Kovarik 2014, Cholewinski 2018, Dixit 2018. 모두 기존 seed와 역할이 중복된다. Pigeon 2021(IFPEN 최신 표면 모델)은 필요해지면 **보강 1순위**다. 사유는 `seed_candidates.csv` 참조.

## 4. Coverage (KEEP 기준)

| 노드 | 담당 | 상태 |
|---|---|---|
| [P] Processing | Kwak2007, Jeong2020, Shi2020, Digne2004 (+OPTIONAL: Choi, Ingram-Jones, Liu) | 과포화 |
| [S] Structure | Kwak2007, Morterra1996, Knozinger1978, Prins2020, Wischert2012 | 충분 |
| [O1] OH 화학 | Ammendola2011, Amenomiya1978 | 확보 |
| [O2] 격자 산소 이동 | Martin1996 | **실험 1편 — 얇음** |
| [O3] 산소 제거 | Hinuma2020, Carrasco2004 (계산), Ostrovski2010 (기준선), Shi2020·Wang2022 (주장) | 실험 직접 증거 없음 |
| [R1] 표면 반응성 | Joubert2006, Wischert2012, Kramer1979, Kalamaras2008 | 확보 |
| [R2] Reducibility | Jeong2020 (Tier C1) | Tier A 없음 |

**다양성** (KEEP 18편):
- 연도: 1978–2022 연속.
- 그룹: 17개 독립 그룹.
- 분야: 촉매, 표면과학, 계산재료, 금속공학, 플라즈마.
- 유형: 실험 12, 계산 3, 계산+실험 2, review 1.

## 5. 남은 공백

1. 맨 γ-Al₂O₃의 H₂-TPR을 주제로 한 1차 문헌. TPR 그림이 SI에 묻힌 경우도 찾아야 한다.
2. H₂ 소모와 H₂O 생성을 동시 정량한 문헌 (Tier A1).
3. 환원 후 O₂ 재산화 적정 문헌 (A2) — 미발견.
4. 같은 시료에서 Al(V) 분율과 산소 결손량을 동시 측정한 문헌 — 미발견. 존재하지 않을 수도 있다.
5. γ상 표면의 산소공공 생성에너지 계산.
6. 결함 분광(EPR 등) seed — 촉매 문헌에 전통이 없어 의도적으로 비워 두었다. 전면 수집 때 `EPR` + `γ-alumina` + `catalysis`로 재확인한다.
7. Tier A 증거 기준의 근거 문헌 4편(Ruiz Puigdollers 2017, Esch 2005, Madier 1999, Kumar 2016)은 γ-Al₂O₃ 논문이 아니다. 그래서 known-item 대상이 아니라 **비교 기준군(reference-standard)**으로 따로 분류한다.
