<div align="center">

# ⚡ 1차 · 리뷰 감성과 소셜 NPS 파이프라인

**브랜드 리뷰를 수집하고 별점 또는 감성 점수로 추천·중립·비추천 비율을 계산하는 선행 분석 노트북입니다. 식품 브랜드 리뷰를 입력으로 사용한 실험 흐름을 담았습니다.**

**기술 분류:** 자연어 처리 › 리뷰 감성 점수화 › 키워드·선택 LLM과 소셜 NPS

[목적](#purpose) · [기능](#features) · [입출력](#flow) · [구성](#files) · [준비](#setup) · [사용법](#usage) · [결과](#results) · [제약](#limits) · [변경](#changes)

</div>

<a name="purpose"></a>

## 🎯 이 단계에서 하는 일

실제 별점이 있으면 먼저 이용하고, 없으면 키워드 또는 선택한 Gemini API로 1~5점을 추정합니다. 리뷰 기반 소셜 NPS와 0~10점 추천의향 설문 기반 NPS를 구분해 읽습니다.

<a name="features"></a>

## 🧩 주요 기능과 처리 방식

| 구성 | 실제 역할 |
| --- | --- |
| 리뷰 수집 | requests·BeautifulSoup과 페이지 규칙으로 리뷰·별점을 찾습니다. |
| 키워드 점수 | 키워드 가중치 합계와 간단한 부정어 규칙을 이용해 1~5점으로 나눕니다. |
| 선택 LLM | Gemini 배치 요청·재시도·배치 분할로 감성 점수를 구하는 별도 경로가 있습니다. |
| 소셜 NPS | 4~5점 추천·3점 중립·1~2점 비추천으로 분류해 비율 차를 계산합니다. |

<a name="flow"></a>

## 🔄 입력 → 처리 → 출력

| 입력 | 처리 | 출력·읽을 결과 |
| --- | --- | --- |
| 리뷰·실제 별점 | 수집·텍스트 정리 | 리뷰 표 |
| 별점 없는 리뷰 | 키워드 또는 LLM 점수화 | 1~5점과 감성 단서 |
| 리뷰 점수 | 추천·중립·비추천 집계 | 소셜 NPS와 그래프 |

<a name="files"></a>

## 📁 파일과 핵심 처리

| 파일 | 이용 방법 |
| --- | --- |
| [1차/brand_nps_auto_pipeline_v2.ipynb](../../1%EC%B0%A8/brand_nps_auto_pipeline_v2.ipynb) | 설정·함수·실행 셀 |

### 🔎 함수·셀로 찾아가기

아래 이름은 해당 파일의 실제 정의입니다. 위 처리 설명과 함께 설정·호출 순서·출력 경로를 따라 읽습니다.

| 파일 | 핵심 정의 |
| --- | --- |
| [1차/brand_nps_auto_pipeline_v2.ipynb](../../1%EC%B0%A8/brand_nps_auto_pipeline_v2.ipynb) | 셀 5: `setup_nanumgothic_style`<br>셀 9: `fetch_html` · `is_allowed_by_robots` · `build_page_url` · `extract_rating_from_row` · `extract_cafe24_review_rows` · `guess_review_elements` · `collect_reviews_auto`<br>셀 16: `_is_negated` · `score_review_keyword` · `classify_nps`<br>셀 17: `get_gemini_client` · `build_keyword_reference_block` · `_build_batch_prompt` · `score_reviews_llm_batch`<br>셀 27: `parse_keyword_field` |

<a name="setup"></a>

## ⚙️ 환경과 설정

| 항목 | 조건·기본값 |
| --- | --- |
| 기본 환경 | pandas·requests·BeautifulSoup·Matplotlib·Jupyter |
| 선택 모델 | google-genai와 본인의 GOOGLE_API_KEY |
| 점수 구간 | 합계≥5→5점,2~4→4점,-1~1→3점,-4~-2→2점,나머지 1점 |
| 분류 | 4~5 추천·3 중립·1~2 비추천 |

<a name="usage"></a>

## 🚀 준비와 사용 순서

1. 노트북에서 수집 대상 URL·페이지 구조와 입력 파일 위치를 확인합니다.
2. 별점 우선 경로와 텍스트 추정 경로 중 사용할 방식을 정합니다.
3. 키워드 사전·부정어 처리와 점수 구간을 확인하고 필요한 셀을 순서대로 읽습니다.
4. 추천·중립·비추천의 분모와 수집·분류 실패 건수를 확인한 뒤 집계 결과를 해석합니다.

<a name="results"></a>

## 📊 결과를 읽는 방법

키워드 함수의 점수 구간은 노트북 앞부분의 이전 설명표와 다른 부분이 있어 실제 함수 기준으로 읽어야 합니다. 반복 키워드 전체 횟수가 아니라 처음 찾은 위치를 중심으로 가중치를 적용합니다.

LLM 경로는 리뷰 본문을 외부 API로 보내며, 재시도·배치 분할 후에도 실패한 건은 3점으로 처리합니다. 이 대체값이 중립 반응에 섞이는 점과 반올림한 비율 차로 지표를 계산하는 방식을 함께 확인합니다.

<a name="limits"></a>

## 🛠️ 알려진 제약과 확인 지점

| 상황 | 확인할 내용 |
| --- | --- |
| 지표 정의 | 정식 추천의향 설문을 직접 받은 NPS가 아닙니다. |
| 대체값 | API 실패 3점을 실제 중립 평가와 구분합니다. |
| 수집 조건 | 페이지 구조·선택 표본·별점 유무가 결과에 영향을 줍니다. |
| 설치 셀 | 패키지 설치와 외부 API 셀을 실행 전에 구분합니다. |

<a name="changes"></a>

## 🔀 이전 단계와의 변화

브랜드 리뷰 수집·감성 점수·소셜 NPS를 연결한 1차입니다.2차는 이 입력을 그대로 확장한 국가 대표성 조사가 아니라 한·중·일 채널 콘텐츠의 분류·비교로 목적이 달라집니다.

[🔎 직전 단계 전체 비교·구성](step-1.patch)

<details>
<summary>📎 이 단계의 파일 기록과 전체 해시</summary>

아래 표는 해당 단계가 기록될 당시의 파일 정보입니다. 현재 첨부는 [프로젝트 자료 안내](../../README.md)에서 확인할 수 있습니다.

| 구분 | 파일 |
| :--- | :--- |
| 추가 | `brand_nps_auto_pipeline_v2.ipynb` |

</details>

---

[🏠 프로젝트](../../README.md) · [🗂️ 전체 차수](../REVISION_INDEX.md) · [📁 자료 폴더](../../1%EC%B0%A8) · [➡️ 2차](step-2.md)
