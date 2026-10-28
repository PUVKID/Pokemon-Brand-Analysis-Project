# 📚 2차

한·중·일 포켓몬 채널의 목적·메시지·감성·행동의도·토픽을 비교합니다.

## 🔎 확인할 자료

- [주요 근거 파일](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) · `YOUTUBE_API_KEY`
- [전체 차수와 파일 집계](../VERSIONS.md)
- [프로젝트 소개](../../README.md)

## 🧭 실험 조건

기본 노트북의 YouTube 키는 선택 사항이며, 이전 Docker 사본의 인증 조건은 다릅니다. 2차 노트북은 수집과 분류 과정을 구성합니다.


## 🧩 주요 내용

- 채널 Excel, YouTube·홈페이지 수집, 수동 CSV를 연결하며 수동 입력 템플릿과 보완 경로를 제공합니다.
- 목적·메시지 유형·행동의도·토픽 및 감성 분류를 수행합니다. 댓글의 표본 구성이 전체 이용자 의견을 대표한다는 보장은 없습니다.
- Excel 시트 작성과 국가별 그래프·통계 비교, 수동 검토 표본 및 Cohen kappa 계산 경로를 포함합니다.

## 🔄 자료 구성

1차의 리뷰 점수 집계에서 다국가 콘텐츠 속성 비교로 목적이 바뀝니다. 기본 2차와 이전 Docker 사본은 인증 조건이 다릅니다.

## 📍 관련 자료

- [2차/포켓몬30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) · `def load_manual` · 셀 15 소스 26행
- [2차/포켓몬30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) · `def classify_purpose` · 셀 4 소스 63행
- [2차/포켓몬30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) · `def kappa_report` · 셀 46 소스 25행

셀 번호는 0부터, 소스 행 번호와 PDF 쪽 번호는 1부터 셉니다. 
