# 📚 1차

식품 브랜드 리뷰의 실제 별점 또는 추정 점수를 집계하는 선행 분석입니다.

## 🔎 확인할 자료

- [주요 근거 파일](../../1%EC%B0%A8/brand_nps_auto_pipeline_v2.ipynb) · `classify_nps`
- [전체 차수와 파일 집계](../VERSIONS.md)
- [프로젝트 소개](../../README.md)

## 🧭 읽을 때 주의할 점

별점이 없으면 키워드나 선택적 API로 추정합니다. 0~10점 추천의향 설문은 아닙니다.


## 🧩 구체적으로 살펴볼 내용

- 웹 리뷰를 수집하고 별점이 없으면 키워드 점수 또는 선택한 API로 평가하도록 구성합니다.
- classify_nps가 점수를 추천·중립·비추천으로 나눕니다. 설문 응답의 0~10점 추천의향 NPS와 자료 생성 방식이 다릅니다.

## 🔄 앞선 자료와의 관계

2차와 분석 대상·입력 단위가 달라 수치 증감을 같은 실험의 성능 향상으로 비교할 수 없습니다.

## 📍 파일 안에서 확인하기

- [1차/brand_nps_auto_pipeline_v2.ipynb](../../1%EC%B0%A8/brand_nps_auto_pipeline_v2.ipynb) · `def collect_reviews_auto` · 셀 9 소스 87행
- [1차/brand_nps_auto_pipeline_v2.ipynb](../../1%EC%B0%A8/brand_nps_auto_pipeline_v2.ipynb) · `def classify_nps` · 셀 16 소스 111행

셀 번호는 0부터, 소스 행 번호와 PDF 쪽 번호는 1부터 셉니다. 문서와 코드의 정적 대조이며, 새 학습·추론·장치 측정·공격 실행 결과는 아닙니다.
