# γ-Al₂O₃ Literature Study

γ-Al₂O₃(gamma alumina)의 **synthesis / post-treatment condition이 surface 및 defect structure를 어떻게 바꾸며, 어떤 조건에서 reactive하거나 reducible한 γ-Al₂O₃가 형성되는가**를 문헌연구로 규명하고, 최종적으로 **pretreatment strategy를 도출**한다.



---

## 현재 상태

| 단계 | 내용 | 상태 |
|---|---|---|
| 1–5 | 방법론 확립, seed set 구축 및 재검토, query 설계 시험 | 완료 |
| 6 | Tier 1 코퍼스 수집 및 screening | **다음 단계** |

## 문서 (읽는 순서)

| 파일 | 내용 |
|---|---|
| [`docs/01_methodology.md`](docs/01_methodology.md) | 선행 문헌 연구 방법론. 리뷰 유형, source 역할, query 원칙, 중단 기준, screening, LLM 사용 범위와 검증 관문(Gate 1–3) |
| [`docs/02_evidence_framework.md`](docs/02_evidence_framework.md) | reducibility의 정의, 연구 framework(5축·2분기), 증거 등급 Tier A/B/C |
| [`docs/03_seed_set.md`](docs/03_seed_set.md) | seed set v2 (KEEP 18 / OPTIONAL 9 / REMOVE 6)와 선정 근거 |
| [`docs/04_query.md`](docs/04_query.md) | 검색식 전문, 변이별 recall 측정, 미검출 진단, 2-tier 설계, Scopus/WoS 변환형 |

## 데이터

| 파일 | 행 | 내용 |
|---|---|---|
| `data/methodology_references.csv` | 71 | 방법론 근거 문헌 (Crossref 70 + arXiv 1 검증). 본문 인용 키 `[Key]`와 대응 |
| `data/reducibility_references.csv` | 18 | reducibility 개념 문헌. `content_read` 열에 초록 열람(9) / 서지만 검증(9) 표시 |
| `data/reducibility_evidence_criteria.csv` | 12 | Tier A/B/C 기준. 각 기준이 입증하는 것과 입증하지 못하는 것 |
| `data/seed_set_v2.csv` | 33 | 현행 seed set |
| `data/seed_set_v1_final.csv` / `seed_candidates.csv` | 16 / 21 | v1 seed set과 후보 평가 (이력) |
| `data/known_item_diagnostic.csv` | 27 | seed × query 라운드별 검출 여부, 원인 코드, 조치 |

`process/`에는 각 단계의 실행 계획(JSON)이 과정 기록으로 남아 있음

---

## 핵심 발견 (방법론적)

1. **인용이 주장을 지지하지 않는다.** Jeong 2020은 267°C의 H₂-TPR peak를 보고 “Al₂O₃ 표면의 Al이 환원된 것”이라고 해석하면서 Ammendola 2011을 인용했다. 그런데 Ammendola 원문은 H₂가 아니라 CO를 사용한 실험이었고, 594–602°C의 신호를 Al 환원이 아니라 surface OH와 CO의 반응으로 물이 생성된 것이라고 설명한다.
→ 즉, 논문에 citation이 있다고 해서 그 citation이 실제로 그 주장을 뒷받침하는 것은 아니다. 그래서 앞으로는 인용된 원문까지 확인하는 Gate 3가 필요하다. → [02 §4](docs/02_evidence_framework.md#4-사례-인용이-주장을-지지하지-않는다)
2. **Al(V)가 많으면 oxygen vacancy가 잘 생긴다”는 핵심 연결고리가 아직 없다** 처음 생각한 가설은 대략
**Al(V) 증가 → oxygen vacancy 형성 용이 → reducible γ-Al₂O₃** 이었으나, 문헌을 찾아보니 Al(V)와 oxygen vacancy를 직접 연결해서 측정한 연구를 찾지 못했다.
→ 따라서 현재로서는 이 연결을 알려진 사실로 전제하면 안 되고, 오히려 연구에서 검증해야 할 hypothesis로 봐야 한다.
→ [02 §6](docs/02_evidence_framework.md#6-사슬-고리별-증거-감사)
4. **Al2O3 환원 증명의 어려움** CeO₂라면 Ce⁴⁺ → Ce³⁺, TiO₂라면 Ti⁴⁺ → Ti³⁺처럼 metal oxidation state 변화를 XPS/EPR 등으로 확인할 수 있다. 하지만 Al₂O₃의 Al은 기본적으로 Al³⁺이고 안정한 Al²⁺ 같은 상태를 이용하기 어렵다.
→ 따라서 H₂-TPR peak 하나만 보고 “Al₂O₃가 환원됐다”고 하기 어렵고, oxygen vacancy 같은 defect가 실제 생성됐다는 spectroscopic evidence가 필요하다. 현재 조사 범위에서는 γ-Al₂O₃에 대해 그런 강한 직접 증거(Tier A)를 아직 찾지 못하였다.
5. **OpenAlex만 검색해서는 논문을 충분히 찾기 어렵다** 특히 Elsevier 논문의 경우 OpenAlex에 abstract가 들어 있는 비율이 조사 결과 **2.6%**밖에 되지 않았다. 그러면 abstract keyword search를 한다고 해도 실제로는 대부분 title만 검색하는 것과 비슷해진다.
→ 그래서 OpenAlex 하나만 쓰지 말고 Web of Science(WoS), Scopus 같은 database를 추가하였다. → [04 §0](docs/04_query.md#0-설계-전제를-뒤집은-관측--openalex-초록-보유율)
7. **검색어 하나로 모든 관련 논문을 잘 찾는 것은 불가능했다.** 검색식을 좁게 만들면 관련성이 높은 논문만 나오지만 중요한 논문을 놓친다(high precision, low recall). 반대로 관련 논문 21개를 전부 잡도록 검색식을 넓히면 93,857건이나 나와 screening이 불가능해진다(high recall, low precision).
→ 그래서 2단계 검색을 사용하여, 먼저 비교적 정확한 query로 핵심 논문을 찾고, 그 논문들의 references와 citing papers를 따라가는 citation chasing으로 놓친 논문을 확보한다.
8. **oxygen vacancy를 직접 측정한 좋은 방법론은 Al₂O₃ catalyst 문헌보다 다른 분야에 많았다.** γ-Al₂O₃ catalyst 논문만 보면 직접적인 oxygen 이동·제거 증거가 부족하다. 반면 nuclear materials, optical materials, metallurgy, high-temperature oxidation 분야에서는 F-center spectroscopy, ¹⁸O isotope labeling + SIMS 같은 방법으로 oxygen defect나 oxygen transport를 더 직접적으로 연구한다.
→ 이 분야들의 측정 방법을 γ-Al₂O₃ 연구에 가져올 수 있는지 살펴볼 가치가 있으나, 다만 기존 연구 대상은 주로 α-Al₂O₃나 oxide film이므로 γ-Al₂O₃에 그대로 적용된다고 가정하면 안된다.

## 다음 단계

1. Tier 1(5,758건)을 확보한 뒤 제목 screening. 현상별로 분할할 수 있다(reducibility 3,482 / OH 매개 1,675 / defect 반응성 1,195 / 계면 539).
2. Scopus·WoS 보강을 1회 실행하고, OpenAlex 단독 대비 신규 적격 논문 수를 측정.
3. 고온산화·산화피막 문헌 탐색. α상 피막 → γ상 분말 전이 가능성은 별도로 평가.

**미해결**: Tier A 문헌의 존재 여부(A2·A3은 어휘 오염으로 판정 미완), 서지만 검증한 개념 문헌 9편의 원문 확인, 연구 표적 선택(reducibility / defect 반응성 / OH 매개 / 계면).

---

## 표기

| 라벨 | 의미 |
|---|---|
| **[측정]** | 논문이 실제로 측정·계산한 값 |
| **[저자해석]** | 저자가 측정에서 끌어낸 해석 |
| **[문헌정의]** | 문헌이 명시적으로 내린 정의 |
| **[판단]** | 이 사람의 판단 — 논문의 주장이 아님 |
| ①확립 / ②수정 / ③신규 | 방법론 결정의 출처. 기존 문헌에서 확립됨 / 확립된 것을 이 분야에 맞게 수정함 / 이 프로젝트의 신규 제안(직접 근거 없음) |
| † | 서지만 검증한 문헌. 내용 주장 없이 표준 참조로만 인용 |

### 자주 나오는 용어

| 용어 | 뜻 |
|---|---|
| seed | 이미 알고 있는 핵심 논문. 검색식이 이를 찾는지로 query를 진단한다 |
| recall / precision | 관련 문헌 중 검색에 걸린 비율 / 검색 결과 중 관련 문헌 비율 |
| citation chasing (BWC / FWC) | 참고문헌을 거슬러 가기(backward) / 인용한 문헌을 따라가기(forward) |
| Al(V) | 5배위 알루미늄. 표면에만 있는 저배위 Al site |
| oxygen vacancy | 격자에서 O²⁻가 빠진 자리. cation vacancy(Al 자리의 빈자리, γ-Al₂O₃에 원래 존재)와 다름 |
| E_Ovac | 산소공공 하나를 만드는 데 드는 에너지. reducibility의 대표 척도 |
| Tier A/B/C | reducibility 증거로 인정 / 보조 / 불인정 |

---

## 데이터 출처와 검증

- 문헌 탐색과 인용 네트워크에는 OpenAlex API를 썼다.
- 서지 검증에는 Crossref API(preprint는 arXiv API)를 썼다.
- 이 저장소의 모든 DOI는 위 API가 반환한 값이다. 
- 출판사 PDF 원문은 저작권 때문에 포함하지 않았다.
- 파이프라인 스크립트는 포함하지 않았다. 질의 문자열은 `docs/04`에 그대로 있어 재현할 수 있다.

*분석 보조: Claude Science. 확정된 사실, 저자의 해석, AI의 추론은 각 문서에서 구분 표기했다.*
