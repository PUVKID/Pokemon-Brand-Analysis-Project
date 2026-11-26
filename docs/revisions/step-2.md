<!-- language-choice:start -->
🔵 **한국어** · [English overview](../../en/README.md)
<!-- language-choice:end -->

<a id="-2차--한중일-포켓몬-콘텐츠-비교"></a>

# 2차·한·중·일 포켓몬 콘텐츠 비교

<!-- reading-levels17:start -->
읽기 수준 · [LEVEL 1](#user-content-reading-level-1) · [LEVEL 2](#user-content-reading-level-2) · [LEVEL 3](#user-content-reading-level-3) · [LEVEL 4](#user-content-reading-level-4) · [LEVEL 5](#user-content-reading-level-5)

<details open>
<summary>LEVEL 1 · Beginner — 목적과 동작부터</summary>

<a id="reading-level-1"></a>

## LEVEL 1 - Beginner

<a id="semantic-collection-level-1"></a>

| 항목 | 이 차수의 내용 |
| --- | --- |
| 목적 | 한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다. |
| 변경 | 1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다. |
| 조건 | 글을 모은 뒤 키워드나 선택한 언어 모델로 점수를 붙이고, 결과를 표로 정리합니다. 2차에서는 댓글·게시물·홈페이지 자료를 모아 분류·시트·통계로 연결합니다.<br>같은 행이 여러 의미의 완료 건수를 뜻하는 것은 아닙니다. |
| 동작 | 1.<br>입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다. |
| 결과 | 검수 표본 파일의 행 수는 사람이 검수를 모두 마친 건수와 같은 뜻이 아닙니다. |

### LEVEL 1·2차수집과 자동 분류의 준비

1차는 식품 리뷰,2차는 한·중·일 포켓몬 채널 자료입니다. 이미 보관된 표를 읽는 일과 새로 자료를 모으는 일은 다릅니다. 먼저 Excel6개와 폴더를 맞추고 사용할 채널·기간·선택 기능을 고른 뒤 순서대로 실행하세요.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-1-row-1"></a> 준비와 실행 순서 | 2차는 한국·중국·일본 홈페이지/SNS/댓글을 비교합니다.<br>원본 Excel6개와 DATA_DIR, 채널 링크·기간을 확인하고 수집 →분류 →표 작성 →분석 순서로 진행합니다.<br>미지원 자료는 manual/CSV로 넣습니다. |
| <a id="layout18-table-1-row-2"></a> 도구 역할 | requests는 문서 요청,BeautifulSoup은 페이지에서 내용 추출,pandas는 표 처리,openpyxl은 Excel,Matplotlib은 그래프를 맡습니다.<br>선택 yt-dlp·감성 모델·Playwright는 실행 경로에 따라 필요하며 사람 검 수의 정답을 대신하지 않습니다. |
| <a id="layout18-table-1-row-3"></a> 기간·표본 상한 | 기본 국가 순서는 한국·중국·일본, 시작2026-01-01, 종료 None은 실행 당시 날짜입니다.<br>채널당 영상 최대 100, 영상 당 댓글 최대 30,relevance 정렬이 수집 표본을 제한합니다. |
| <a id="layout18-table-1-row-4"></a> 분류 값 | 캠페인 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다.<br>선택 감성 모델이 로드 실패하면 사전 방식으로 바꾸고 유효한 수동 CSV 분류 값이 있으면 우선합니다. |
| <a id="layout18-table-1-row-5"></a> 인증·실행 사본 차이 | 기본 2차는 YOUTUBE_API_KEY가 없으면 YouTube 수집을 건너뜁니다.<br>이전 Docker 이름 사본은 GOOGLE_API_KEY가 없으면 KeyError로 중단합니다.<br>Docker 이름이 컨테이너 환경 포함을 뜻하지 않습니다.pip/apt 설치·폰트 셀도 실행 전에 확인합니다. |


<a id="semantic-statistics-level-1"></a>

### LEVEL 1 · 비율·검정·관계 분석을 구분하기

같은 표에서도 **비율,나라 간 차이,두 값의 관계는 다른 질문**입니다. 공유 수 0은 미 제공 때문에 적힌 값일 수 있으니 실제 반응 0으로 해석하지 마세요. 구간은 비율의 불확실성을 나타내며 한 숫자로 모든 나라의 소비자를 설명하지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-2-row-1"></a> 참여율 | (좋아요 +댓글 +공유)/조회 수 ×100입니다.<br>조회 수 0·결 측은 제외합니다.<br>YouTube는 공유 수를 제공하지 않아 0으로 기록하므로 실제 공유가 0이었다는 관측과 다릅니다. |
| <a id="layout18-table-2-row-2"></a> 행동 의도와 범주 비교 | 95% Wilson 구간은 국가별 비율의 불확실성을 봅니다.<br>카이제곱은 범주 구성 차이,Cramér’s V는 그 관련 크기를 봅니다.<br>작은 기대 빈도 경고가 있으면 검정 해석을 함께 점검해야 합니다. |
| <a id="layout18-table-2-row-3"></a> 분포와 국가 쌍 비교 | Kruskal–Wallis·ε² 는 국가 간 분포 비교와 효과 크기,Mann–Whitney U는 국가 쌍 비교,Bonferroni는 여러 비교를 한 데 따른 보정입니다. |
| <a id="layout18-table-2-row-4"></a> 상관과 산출물 | Spearman은 게시물 참여율과 댓글 평균 감성의 관계를 살핍니다.<br>표 3개·PNG 그래프 10개가 현황·지표·검정 결과를 보여 줍니다.<br>관계가 있다는 사실이 캠페인의 인과 효과를 증명하지는 않습니다. |


<a id="semantic-human-level-1"></a>

### LEVEL 1 · 사람 검수와 저장 결과의 의미

표본을 뽑아 놓은 것과 사람이 판정한 것은 다릅니다. 원문과 자동 분류를 읽고 human 열을 채운 뒤에야 사람의 판단과 비교할 수 있습니다. 그래프만 보기 전에 어느 자료를 몇 건 검수했는지 확인하세요.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-3-row-1"></a> 보관 자료와 표본 | 댓글 data5585 행/검수 표본 100 행, 게시 물400/28, 홈페이지73/35입니다.<br>표본 파일 행 수는 사람이 검수 완료한 건수가 아닙니다. |
| <a id="layout18-table-3-row-2"></a> 표본 상한과 human _* | 국가별 댓글 최대 50개, 게시물·홈페이지 각각 최대 14개를 뽑습니다.<br>후자 두 자료는 각각 3개국 최대 42개이며 확보 량에 따라 줄어듭니다.<br>사람이 human _*열을 채운 뒤 검수 지표를 계산합니다. |
| <a id="layout18-table-3-row-3"></a> Cohen’s κ와 일치율 | κ는 우연 일치를 고려한 분류 일치 지표입니다.일부만 채운 파일에서는 κ의 유효쌍과 일치율 분모가 달라질 수 있으므로 실제 채운 표본과 분모를 확인합니다. |
| <a id="layout18-table-3-row-4"></a> 폴더별 자료 역할 | data/는 수집 CSV·검수표본, 수집 결과/는 국가별 Excel 사본, 결과/분석 결과 _통합.xlsx는 통합 분석, 결과/figures/는 10 그래프,manual/은 수동 입력입니다.<br>자동 분류와 사람 정답을 구분해 읽습니다. |


<a id="semantic-limitations-level-1"></a>

### LEVEL 1 · 재실행·수집 실패와 해석의 한계

같은 노트북을 다시 실행해도 날짜·채널 접근·파일이 달라질 수 있습니다. **사람이 고친 검수파일을 먼저 보관**하세요. 자료가 비면 경로나 접근 조건을 확인하고, 없는 의견을 0점이나 국가 전체의 반응으로 만들지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-4-row-1"></a> 대표성과 기간 | 공식 채널·인기 순 댓글 중심의 비확률 표본입니다.<br>국가 전체 소비자를 대표하지 않습니다.<br>홈페이지에는 SNS와 같은 기간 필터가 적용되지 않습니다. |
| <a id="layout18-table-4-row-2"></a> 접근 과 정규화 | robots.txt 조회 실패는 허용으로 처리됩니다.<br>URL 정규화는 대소 문자를 바꾸므로 대소 문자를 구분하는 게시물 ID의 링크가 맞는지 확인해야 합니다. |
| <a id="layout18-table-4-row-3"></a> 재작성되는 파일 | 원본 Excel 사본을 사용하지만 같은 이름 출력 Excel·CSV·검수표본은 재실행 시 다시 씁니다.<br>사람이 채운 검수 파일은 먼저 별도 보존합니다. |
| <a id="layout18-table-4-row-4"></a> 증상별 확인 점 | Excel 오류는 DATA_DIR·파일/시트,YouTube 실패는 키·서비스 설정·쿼터, 빈 웹 수집은 페이지 구조·JS·접근 조건을 확인합니다.<br>미지원 채널은 manual CSV, 감성 차이는 모델/사전/사람 표본, 한글 오류는 폰트 설정을 봅니다. |

[동일 수준 프로젝트 안내](../%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A81.md)


</details>

<details>
<summary>LEVEL 2 · Explorer — 구성과 연결 원리</summary>

<a id="reading-level-2"></a>

## LEVEL 2 - Explorer

<a id="semantic-collection-level-2"></a>

| 항목 | 이 차수의 내용 |
| --- | --- |
| 목적 | 한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다. |
| 변경 | 1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다. |
| 조건 | 1차는 수집 →1~5점 추정 →추천 범주 →비율 차이입니다. 2차는 채널별 수집 →정규화 →콘텐츠 분류 →검수 표본·비교표입니다.<br>원문과 분류 값, 집계 단위를 연결해 읽습니다. |
| 동작 | 1.<br>입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다. |
| 결과 | 검수 표본 파일의 행 수는 사람이 검수를 모두 마친 건수와 같은 뜻이 아닙니다. |

### LEVEL 2·2차수집과 자동 분류의 준비

수집 도구가 원문을 가져오고 분류가 이를 범주로 바꾸며 표·그래프가 국가별 차이를 보여 줍니다. 댓글 상한과 relevance는 어떤 의견이 들어오는지를 바꿉니다. 자동 모델과 사전 대체·수동 우선 규칙도 결과의 일부입니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-10-row-1"></a> 준비와 실행 순서 | 2차는 한국·중국·일본 홈페이지/SNS/댓글을 비교합니다.<br>원본 Excel6개와 DATA_DIR, 채널 링크·기간을 확인하고 수집 →분류 →표 작성 →분석 순서로 진행합니다.<br>미지원 자료는 manual/CSV로 넣습니다. |
| <a id="layout18-table-10-row-2"></a> 도구 역할 | requests는 문서 요청,BeautifulSoup은 페이지에서 내용 추출,pandas는 표 처리,openpyxl은 Excel,Matplotlib은 그래프를 맡습니다.<br>선택 yt-dlp·감성 모델·Playwright는 실행 경로에 따라 필요하며 사람 검 수의 정답을 대신하지 않습니다. |
| <a id="layout18-table-10-row-3"></a> 기간·표본 상한 | 기본 국가 순서는 한국·중국·일본, 시작2026-01-01, 종료 None은 실행 당시 날짜입니다.<br>채널당 영상 최대 100, 영상 당 댓글 최대 30,relevance 정렬이 수집 표본을 제한합니다. |
| <a id="layout18-table-10-row-4"></a> 분류 값 | 캠페인 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다.<br>선택 감성 모델이 로드 실패하면 사전 방식으로 바꾸고 유효한 수동 CSV 분류 값이 있으면 우선합니다. |
| <a id="layout18-table-10-row-5"></a> 인증·실행 사본 차이 | 기본 2차는 YOUTUBE_API_KEY가 없으면 YouTube 수집을 건너뜁니다.<br>이전 Docker 이름 사본은 GOOGLE_API_KEY가 없으면 KeyError로 중단합니다.<br>Docker 이름이 컨테이너 환경 포함을 뜻하지 않습니다.pip/apt 설치·폰트 셀도 실행 전에 확인합니다. |


<a id="semantic-statistics-level-2"></a>

### LEVEL 2 · 비율·검정·관계 분석을 구분하기

참여율을 만든 뒤 범주·분포·상관이라는 질문에 맞게 분석 도구가 나뉩니다. Wilson은 비율 추정,Cramér’s V/ε² 는 효과 크기,Bonferroni 는 비교를 여러 번 한 문제를 다룹니다. 이 도구들은 서로 대체하는 점수가 아닙니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-11-row-1"></a> 참여율 | (좋아요 +댓글 +공유)/조회 수 ×100입니다.<br>조회 수 0·결 측은 제외합니다.<br>YouTube는 공유 수를 제공하지 않아 0으로 기록하므로 실제 공유가 0이었다는 관측과 다릅니다. |
| <a id="layout18-table-11-row-2"></a> 행동 의도와 범주 비교 | 95% Wilson 구간은 국가별 비율의 불확실성을 봅니다.<br>카이제곱은 범주 구성 차이,Cramér’s V는 그 관련 크기를 봅니다.<br>작은 기대 빈도 경고가 있으면 검정 해석을 함께 점검해야 합니다. |
| <a id="layout18-table-11-row-3"></a> 분포와 국가 쌍 비교 | Kruskal–Wallis·ε² 는 국가 간 분포 비교와 효과 크기,Mann–Whitney U는 국가 쌍 비교,Bonferroni는 여러 비교를 한 데 따른 보정입니다. |
| <a id="layout18-table-11-row-4"></a> 상관과 산출물 | Spearman은 게시물 참여율과 댓글 평균 감성의 관계를 살핍니다.<br>표 3개·PNG 그래프 10개가 현황·지표·검정 결과를 보여 줍니다.<br>관계가 있다는 사실이 캠페인의 인과 효과를 증명하지는 않습니다. |


<a id="semantic-human-level-2"></a>

### LEVEL 2 · 사람 검수와 저장 결과의 의미

수집 자료 →자동 범주 →검수표본 →사람 라벨 →κ/일치율의 순서입니다. 5585개 댓글이 있다고 모두 사람이 확인한 것은 아닙니다. 검수 지표는 입력 규모보다 실제 서로 비교 가능한 라벨쌍에 의해 결정됩니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-12-row-1"></a> 보관 자료와 표본 | 댓글 data5585 행/검수 표본 100 행, 게시 물400/28, 홈페이지73/35입니다.<br>표본 파일 행 수는 사람이 검수 완료한 건수가 아닙니다. |
| <a id="layout18-table-12-row-2"></a> 표본 상한과 human _* | 국가별 댓글 최대 50개, 게시물·홈페이지 각각 최대 14개를 뽑습니다.<br>후자 두 자료는 각각 3개국 최대 42개이며 확보 량에 따라 줄어듭니다.<br>사람이 human _*열을 채운 뒤 검수 지표를 계산합니다. |
| <a id="layout18-table-12-row-3"></a> Cohen’s κ와 일치율 | κ는 우연 일치를 고려한 분류 일치 지표입니다.일부만 채운 파일에서는 κ의 유효쌍과 일치율 분모가 달라질 수 있으므로 실제 채운 표본과 분모를 확인합니다. |
| <a id="layout18-table-12-row-4"></a> 폴더별 자료 역할 | data/는 수집 CSV·검수표본, 수집 결과/는 국가별 Excel 사본, 결과/분석 결과 _통합.xlsx는 통합 분석, 결과/figures/는 10 그래프,manual/은 수동 입력입니다.<br>자동 분류와 사람 정답을 구분해 읽습니다. |


<a id="semantic-limitations-level-2"></a>

### LEVEL 2 · 재실행·수집 실패와 해석의 한계

기간 필터·인기 정렬·접근 실패·URL 변환은 모두 모이는 자료에 영향을 줍니다. 한 단계의 누락이 뒤의 국가 비교로 이어질 수 있습니다. 표와 그래프는 확보된 표본의 분석이며 전체 여론이나 인과 효과를 설명하지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-13-row-1"></a> 대표성과 기간 | 공식 채널·인기 순 댓글 중심의 비확률 표본입니다.<br>국가 전체 소비자를 대표하지 않습니다.<br>홈페이지에는 SNS와 같은 기간 필터가 적용되지 않습니다. |
| <a id="layout18-table-13-row-2"></a> 접근 과 정규화 | robots.txt 조회 실패는 허용으로 처리됩니다.<br>URL 정규화는 대소 문자를 바꾸므로 대소 문자를 구분하는 게시물 ID의 링크가 맞는지 확인해야 합니다. |
| <a id="layout18-table-13-row-3"></a> 재작성되는 파일 | 원본 Excel 사본을 사용하지만 같은 이름 출력 Excel·CSV·검수표본은 재실행 시 다시 씁니다.<br>사람이 채운 검수 파일은 먼저 별도 보존합니다. |
| <a id="layout18-table-13-row-4"></a> 증상별 확인 점 | Excel 오류는 DATA_DIR·파일/시트,YouTube 실패는 키·서비스 설정·쿼터, 빈 웹 수집은 페이지 구조·JS·접근 조건을 확인합니다.<br>미지원 채널은 manual CSV, 감성 차이는 모델/사전/사람 표본, 한글 오류는 폰트 설정을 봅니다. |

[동일 수준 프로젝트 안내](../%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A82.md)


</details>

<details>
<summary>LEVEL 3 · Practitioner — 준비·실행·결과 확인</summary>

<a id="reading-level-3"></a>

## LEVEL 3 - Practitioner

<a id="semantic-collection-level-3"></a>

| 항목 | 이 차수의 내용 |
| --- | --- |
| 목적 | 한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다. |
| 변경 | 1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다. |
| 조건 | 키워드 함수 기준은 점수 5 이상 →5점, 2~4 →4점, -1~1 →3점, -4~-2 →2점, 나머지 →1점입니다.<br>노트북 앞 부분의 예전 설명 표와 차이가 있습니다.<br>실제 함수의 기준을 확인하세요. |
| 동작 | 1.<br>입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다. |
| 결과 | 검수 표본 파일의 행 수는 사람이 검수를 모두 마친 건수와 같은 뜻이 아닙니다. |

### LEVEL 3·2차수집과 자동 분류의 준비

DATA_DIR·Excel 구조·기간·영상/댓글 상한을 먼저 기록하세요. 선택 패키지와 API 키가 필요한 셀을 구분하고 미지원 채널은 manual CSV 흐름으로 준비합니다. 기본 파일과 이전 Docker 사본은 키 누락 동작이 다르므로 같은 실행 명령으로 취급하지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-19-row-1"></a> 준비와 실행 순서 | 2차는 한국·중국·일본 홈페이지/SNS/댓글을 비교합니다.<br>원본 Excel6개와 DATA_DIR, 채널 링크·기간을 확인하고 수집 →분류 →표 작성 →분석 순서로 진행합니다.<br>미지원 자료는 manual/CSV로 넣습니다. |
| <a id="layout18-table-19-row-2"></a> 도구 역할 | requests는 문서 요청,BeautifulSoup은 페이지에서 내용 추출,pandas는 표 처리,openpyxl은 Excel,Matplotlib은 그래프를 맡습니다.<br>선택 yt-dlp·감성 모델·Playwright는 실행 경로에 따라 필요하며 사람 검 수의 정답을 대신하지 않습니다. |
| <a id="layout18-table-19-row-3"></a> 기간·표본 상한 | 기본 국가 순서는 한국·중국·일본, 시작2026-01-01, 종료 None은 실행 당시 날짜입니다.<br>채널당 영상 최대 100, 영상 당 댓글 최대 30,relevance 정렬이 수집 표본을 제한합니다. |
| <a id="layout18-table-19-row-4"></a> 분류 값 | 캠페인 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다.<br>선택 감성 모델이 로드 실패하면 사전 방식으로 바꾸고 유효한 수동 CSV 분류 값이 있으면 우선합니다. |
| <a id="layout18-table-19-row-5"></a> 인증·실행 사본 차이 | 기본 2차는 YOUTUBE_API_KEY가 없으면 YouTube 수집을 건너뜁니다.<br>이전 Docker 이름 사본은 GOOGLE_API_KEY가 없으면 KeyError로 중단합니다.<br>Docker 이름이 컨테이너 환경 포함을 뜻하지 않습니다.pip/apt 설치·폰트 셀도 실행 전에 확인합니다. |


<a id="semantic-statistics-level-3"></a>

### LEVEL 3 · 비율·검정·관계 분석을 구분하기

조회 수 0/결 측 제외와 공유 미 제공 0 처리를 확인한 뒤 각 표의 유효 건수를 확인하세요. 카이제곱 경고·국가 쌍 보 정·Wilson 구간을 결과와 함께 읽습니다. 이미 생성된 Excel·PNG를 확인하는 것과 새 수집·분석 실행은 구분합니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-20-row-1"></a> 참여율 | (좋아요 +댓글 +공유)/조회 수 ×100입니다.<br>조회 수 0·결 측은 제외합니다.<br>YouTube는 공유 수를 제공하지 않아 0으로 기록하므로 실제 공유가 0이었다는 관측과 다릅니다. |
| <a id="layout18-table-20-row-2"></a> 행동 의도와 범주 비교 | 95% Wilson 구간은 국가별 비율의 불확실성을 봅니다.<br>카이제곱은 범주 구성 차이,Cramér’s V는 그 관련 크기를 봅니다.<br>작은 기대 빈도 경고가 있으면 검정 해석을 함께 점검해야 합니다. |
| <a id="layout18-table-20-row-3"></a> 분포와 국가 쌍 비교 | Kruskal–Wallis·ε² 는 국가 간 분포 비교와 효과 크기,Mann–Whitney U는 국가 쌍 비교,Bonferroni는 여러 비교를 한 데 따른 보정입니다. |
| <a id="layout18-table-20-row-4"></a> 상관과 산출물 | Spearman은 게시물 참여율과 댓글 평균 감성의 관계를 살핍니다.<br>표 3개·PNG 그래프 10개가 현황·지표·검정 결과를 보여 줍니다.<br>관계가 있다는 사실이 캠페인의 인과 효과를 증명하지는 않습니다. |


<a id="semantic-human-level-3"></a>

### LEVEL 3 · 사람 검수와 저장 결과의 의미

data의 원자료와 검수 파일을 구분하고 human 열의 채움 상태를 확인하세요. 국가별 표본 상한과 확보 량을 기록한 뒤 κ 유효쌍·일치율 분모를 대조합니다. 재실행 전에 사람이 채운 파일을 별도로 보관해야 합니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-21-row-1"></a> 보관 자료와 표본 | 댓글 data5585 행/검수 표본 100 행, 게시 물400/28, 홈페이지73/35입니다.<br>표본 파일 행 수는 사람이 검수 완료한 건수가 아닙니다. |
| <a id="layout18-table-21-row-2"></a> 표본 상한과 human _* | 국가별 댓글 최대 50개, 게시물·홈페이지 각각 최대 14개를 뽑습니다.<br>후자 두 자료는 각각 3개국 최대 42개이며 확보 량에 따라 줄어듭니다.<br>사람이 human _*열을 채운 뒤 검수 지표를 계산합니다. |
| <a id="layout18-table-21-row-3"></a> Cohen’s κ와 일치율 | κ는 우연 일치를 고려한 분류 일치 지표입니다.일부만 채운 파일에서는 κ의 유효쌍과 일치율 분모가 달라질 수 있으므로 실제 채운 표본과 분모를 확인합니다. |
| <a id="layout18-table-21-row-4"></a> 폴더별 자료 역할 | data/는 수집 CSV·검수표본, 수집 결과/는 국가별 Excel 사본, 결과/분석 결과 _통합.xlsx는 통합 분석, 결과/figures/는 10 그래프,manual/은 수동 입력입니다.<br>자동 분류와 사람 정답을 구분해 읽습니다. |


<a id="semantic-limitations-level-3"></a>

### LEVEL 3 · 재실행·수집 실패와 해석의 한계

재실행 전에 출력 보존·기간·키/쿼터·URL 사례를 확인하세요. 자료 부족은 미지원 채널의 수동 입력 경로와 구분해서 기록합니다. 감성 분류가 다르면 모델로드와 사전 대체를 확인하고 한글 그래프는 폰트 셀을 점검합니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-22-row-1"></a> 대표성과 기간 | 공식 채널·인기 순 댓글 중심의 비확률 표본입니다.<br>국가 전체 소비자를 대표하지 않습니다.<br>홈페이지에는 SNS와 같은 기간 필터가 적용되지 않습니다. |
| <a id="layout18-table-22-row-2"></a> 접근 과 정규화 | robots.txt 조회 실패는 허용으로 처리됩니다.<br>URL 정규화는 대소 문자를 바꾸므로 대소 문자를 구분하는 게시물 ID의 링크가 맞는지 확인해야 합니다. |
| <a id="layout18-table-22-row-3"></a> 재작성되는 파일 | 원본 Excel 사본을 사용하지만 같은 이름 출력 Excel·CSV·검수표본은 재실행 시 다시 씁니다.<br>사람이 채운 검수 파일은 먼저 별도 보존합니다. |
| <a id="layout18-table-22-row-4"></a> 증상별 확인 점 | Excel 오류는 DATA_DIR·파일/시트,YouTube 실패는 키·서비스 설정·쿼터, 빈 웹 수집은 페이지 구조·JS·접근 조건을 확인합니다.<br>미지원 채널은 manual CSV, 감성 차이는 모델/사전/사람 표본, 한글 오류는 폰트 설정을 봅니다. |

[동일 수준 프로젝트 안내](../%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A83.md)


</details>

<details>
<summary>LEVEL 4 · Advanced — 구현·설계·실패 처리</summary>

<a id="reading-level-4"></a>

## LEVEL 4 - Advanced

<a id="semantic-collection-level-4"></a>

| 항목 | 이 차수의 내용 |
| --- | --- |
| 목적 | 한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다. |
| 변경 | 1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다. |
| 조건 | LLM 경로는 리뷰 본문을 외부 API로 보냅니다.<br>재시도·배치 분할 뒤에도 실패한 한 건은 3점으로 처리해 집계에 포함됩니다.<br>정규화에서 URL 대소 문자를 바꾸는 정책과 robots.txt 조회 실패를 허용으로 처리하는 코드도 검토 지점입니다. |
| 동작 | 1.<br>입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다. |
| 결과 | 검수 표본 파일의 행 수는 사람이 검수를 모두 마친 건수와 같은 뜻이 아닙니다. |

### LEVEL 4·2차수집과 자동 분류의 준비

수집·분류·분석의 의존성을 분리해야 합니다. 페이지 구조/JS 렌더링과 API 쿼터가 수집 범위를, 감성 모델 로드 실패와 수동 값 우선 이 분류 경로를 바꿉니다. END_DATE =None은 재실행 시점에 따라 입력 표본이 달라지는 설정입니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-28-row-1"></a> 준비와 실행 순서 | 2차는 한국·중국·일본 홈페이지/SNS/댓글을 비교합니다.<br>원본 Excel6개와 DATA_DIR, 채널 링크·기간을 확인하고 수집 →분류 →표 작성 →분석 순서로 진행합니다.<br>미지원 자료는 manual/CSV로 넣습니다. |
| <a id="layout18-table-28-row-2"></a> 도구 역할 | requests는 문서 요청,BeautifulSoup은 페이지에서 내용 추출,pandas는 표 처리,openpyxl은 Excel,Matplotlib은 그래프를 맡습니다.<br>선택 yt-dlp·감성 모델·Playwright는 실행 경로에 따라 필요하며 사람 검 수의 정답을 대신하지 않습니다. |
| <a id="layout18-table-28-row-3"></a> 기간·표본 상한 | 기본 국가 순서는 한국·중국·일본, 시작2026-01-01, 종료 None은 실행 당시 날짜입니다.<br>채널당 영상 최대 100, 영상 당 댓글 최대 30,relevance 정렬이 수집 표본을 제한합니다. |
| <a id="layout18-table-28-row-4"></a> 분류 값 | 캠페인 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다.<br>선택 감성 모델이 로드 실패하면 사전 방식으로 바꾸고 유효한 수동 CSV 분류 값이 있으면 우선합니다. |
| <a id="layout18-table-28-row-5"></a> 인증·실행 사본 차이 | 기본 2차는 YOUTUBE_API_KEY가 없으면 YouTube 수집을 건너뜁니다.<br>이전 Docker 이름 사본은 GOOGLE_API_KEY가 없으면 KeyError로 중단합니다.<br>Docker 이름이 컨테이너 환경 포함을 뜻하지 않습니다.pip/apt 설치·폰트 셀도 실행 전에 확인합니다. |


<a id="semantic-statistics-level-4"></a>

### LEVEL 4 · 비율·검정·관계 분석을 구분하기

분모 결 측 처리와 플랫폼별 누락 값의 0 기록은 참여율 비교에 영향을 줍니다. 범주/순위 분포/상관은 다른 분석 단위이므로 동일한 효과로 합치지 않습니다. 여러 국가 쌍 검 정의 보정과 작은 기대 빈도 경고를 유지해야 합니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-29-row-1"></a> 참여율 | (좋아요 +댓글 +공유)/조회 수 ×100입니다.<br>조회 수 0·결 측은 제외합니다.<br>YouTube는 공유 수를 제공하지 않아 0으로 기록하므로 실제 공유가 0이었다는 관측과 다릅니다. |
| <a id="layout18-table-29-row-2"></a> 행동 의도와 범주 비교 | 95% Wilson 구간은 국가별 비율의 불확실성을 봅니다.<br>카이제곱은 범주 구성 차이,Cramér’s V는 그 관련 크기를 봅니다.<br>작은 기대 빈도 경고가 있으면 검정 해석을 함께 점검해야 합니다. |
| <a id="layout18-table-29-row-3"></a> 분포와 국가 쌍 비교 | Kruskal–Wallis·ε² 는 국가 간 분포 비교와 효과 크기,Mann–Whitney U는 국가 쌍 비교,Bonferroni는 여러 비교를 한 데 따른 보정입니다. |
| <a id="layout18-table-29-row-4"></a> 상관과 산출물 | Spearman은 게시물 참여율과 댓글 평균 감성의 관계를 살핍니다.<br>표 3개·PNG 그래프 10개가 현황·지표·검정 결과를 보여 줍니다.<br>관계가 있다는 사실이 캠페인의 인과 효과를 증명하지는 않습니다. |


<a id="semantic-human-level-4"></a>

### LEVEL 4 · 사람 검수와 저장 결과의 의미

라벨 출처와 결측 처리 경계가 핵심입니다.자동 분류 출력과 수동정답을 섞으면 검수 의미가 달라집니다.부분 검수일 때 서로 다른 유효쌍/분모를 사용하는 지표는 같은 표본의 점수라고 단순 비교할 수 없습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-30-row-1"></a> 보관 자료와 표본 | 댓글 data5585 행/검수 표본 100 행, 게시 물400/28, 홈페이지73/35입니다.<br>표본 파일 행 수는 사람이 검수 완료한 건수가 아닙니다. |
| <a id="layout18-table-30-row-2"></a> 표본 상한과 human _* | 국가별 댓글 최대 50개, 게시물·홈페이지 각각 최대 14개를 뽑습니다.<br>후자 두 자료는 각각 3개국 최대 42개이며 확보 량에 따라 줄어듭니다.<br>사람이 human _*열을 채운 뒤 검수 지표를 계산합니다. |
| <a id="layout18-table-30-row-3"></a> Cohen’s κ와 일치율 | κ는 우연 일치를 고려한 분류 일치 지표입니다.일부만 채운 파일에서는 κ의 유효쌍과 일치율 분모가 달라질 수 있으므로 실제 채운 표본과 분모를 확인합니다. |
| <a id="layout18-table-30-row-4"></a> 폴더별 자료 역할 | data/는 수집 CSV·검수표본, 수집 결과/는 국가별 Excel 사본, 결과/분석 결과 _통합.xlsx는 통합 분석, 결과/figures/는 10 그래프,manual/은 수동 입력입니다.<br>자동 분류와 사람 정답을 구분해 읽습니다. |


<a id="semantic-limitations-level-4"></a>

### LEVEL 4 · 재실행·수집 실패와 해석의 한계

수집 단계의 조건 차이를 분석 단계에서 자동 보정한 것으로 취급할 수 없습니다. 홈페이지와 SNS의 기간 차이, 실패 허용 robots 정책, 식별자 소문자화는 별도 검토 대상입니다. 고정 출력 명은 사람 검수 이력을 손실시킬 수 있습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-31-row-1"></a> 대표성과 기간 | 공식 채널·인기 순 댓글 중심의 비확률 표본입니다.<br>국가 전체 소비자를 대표하지 않습니다.<br>홈페이지에는 SNS와 같은 기간 필터가 적용되지 않습니다. |
| <a id="layout18-table-31-row-2"></a> 접근 과 정규화 | robots.txt 조회 실패는 허용으로 처리됩니다.<br>URL 정규화는 대소 문자를 바꾸므로 대소 문자를 구분하는 게시물 ID의 링크가 맞는지 확인해야 합니다. |
| <a id="layout18-table-31-row-3"></a> 재작성되는 파일 | 원본 Excel 사본을 사용하지만 같은 이름 출력 Excel·CSV·검수표본은 재실행 시 다시 씁니다.<br>사람이 채운 검수 파일은 먼저 별도 보존합니다. |
| <a id="layout18-table-31-row-4"></a> 증상별 확인 점 | Excel 오류는 DATA_DIR·파일/시트,YouTube 실패는 키·서비스 설정·쿼터, 빈 웹 수집은 페이지 구조·JS·접근 조건을 확인합니다.<br>미지원 채널은 manual CSV, 감성 차이는 모델/사전/사람 표본, 한글 오류는 폰트 설정을 봅니다. |

[동일 수준 프로젝트 안내](../%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A84.md)


</details>

<details>
<summary>LEVEL 5 · Expert — 근거·프로토콜·한계 검토</summary>

<a id="reading-level-5"></a>

## LEVEL 5 - Expert

<a id="semantic-collection-level-5"></a>

### LEVEL 5·2차수집과 자동 분류의 준비

국가 순서·기간·채널/댓글 상한·정렬·인증 분기·분류 우선순위를 재현 명세로 유지합니다.수동·모델·사전 라벨은 출처가 다르며 자동 수집 성공을 모집단 대표성이나 사람 정답 검증으로 해석할 수 없습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-37-row-1"></a> 준비와 실행 순서 | 2차는 한국·중국·일본 홈페이지/SNS/댓글을 비교합니다.<br>원본 Excel6개와 DATA_DIR, 채널 링크·기간을 확인하고 수집 →분류 →표 작성 →분석 순서로 진행합니다.<br>미지원 자료는 manual/CSV로 넣습니다. |
| <a id="layout18-table-37-row-2"></a> 도구 역할 | requests는 문서 요청,BeautifulSoup은 페이지에서 내용 추출,pandas는 표 처리,openpyxl은 Excel,Matplotlib은 그래프를 맡습니다.<br>선택 yt-dlp·감성 모델·Playwright는 실행 경로에 따라 필요하며 사람 검 수의 정답을 대신하지 않습니다. |
| <a id="layout18-table-37-row-3"></a> 기간·표본 상한 | 기본 국가 순서는 한국·중국·일본, 시작2026-01-01, 종료 None은 실행 당시 날짜입니다.<br>채널당 영상 최대 100, 영상 당 댓글 최대 30,relevance 정렬이 수집 표본을 제한합니다. |
| <a id="layout18-table-37-row-4"></a> 분류 값 | 캠페인 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다.<br>선택 감성 모델이 로드 실패하면 사전 방식으로 바꾸고 유효한 수동 CSV 분류 값이 있으면 우선합니다. |
| <a id="layout18-table-37-row-5"></a> 인증·실행 사본 차이 | 기본 2차는 YOUTUBE_API_KEY가 없으면 YouTube 수집을 건너뜁니다.<br>이전 Docker 이름 사본은 GOOGLE_API_KEY가 없으면 KeyError로 중단합니다.<br>Docker 이름이 컨테이너 환경 포함을 뜻하지 않습니다.pip/apt 설치·폰트 셀도 실행 전에 확인합니다. |


<a id="semantic-statistics-level-5"></a>

### LEVEL 5 · 비율·검정·관계 분석을 구분하기

분모·제외규칙·미제공값 코드·비율 구간·효과크기·다중 비교 보정과 원자료의 비확률 표 집을 함께 검토합니다. Spearman 관계나 유의성만으로 국가 전체 여론·캠페인 인과 효과를 주장할 수 없으며 원문에 없는 검정 공 식/성과를 만들지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-38-row-1"></a> 참여율 | (좋아요 +댓글 +공유)/조회 수 ×100입니다.<br>조회 수 0·결 측은 제외합니다.<br>YouTube는 공유 수를 제공하지 않아 0으로 기록하므로 실제 공유가 0이었다는 관측과 다릅니다. |
| <a id="layout18-table-38-row-2"></a> 행동 의도와 범주 비교 | 95% Wilson 구간은 국가별 비율의 불확실성을 봅니다.<br>카이제곱은 범주 구성 차이,Cramér’s V는 그 관련 크기를 봅니다.<br>작은 기대 빈도 경고가 있으면 검정 해석을 함께 점검해야 합니다. |
| <a id="layout18-table-38-row-3"></a> 분포와 국가 쌍 비교 | Kruskal–Wallis·ε² 는 국가 간 분포 비교와 효과 크기,Mann–Whitney U는 국가 쌍 비교,Bonferroni는 여러 비교를 한 데 따른 보정입니다. |
| <a id="layout18-table-38-row-4"></a> 상관과 산출물 | Spearman은 게시물 참여율과 댓글 평균 감성의 관계를 살핍니다.<br>표 3개·PNG 그래프 10개가 현황·지표·검정 결과를 보여 줍니다.<br>관계가 있다는 사실이 캠페인의 인과 효과를 증명하지는 않습니다. |


<a id="semantic-human-level-5"></a>

### LEVEL 5 · 사람 검수와 저장 결과의 의미

5585/400/73의 보관 행수와100/28/35의 표본 행수, 국가별 추출 상한, 실제 human값 유효 쌍을 분리합니다. κ와 일치율의 분모 정의를 확인하며 자동 분류를 사람이 검증한 정답으로 치환하지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-39-row-1"></a> 보관 자료와 표본 | 댓글 data5585 행/검수 표본 100 행, 게시 물400/28, 홈페이지73/35입니다.<br>표본 파일 행 수는 사람이 검수 완료한 건수가 아닙니다. |
| <a id="layout18-table-39-row-2"></a> 표본 상한과 human _* | 국가별 댓글 최대 50개, 게시물·홈페이지 각각 최대 14개를 뽑습니다.<br>후자 두 자료는 각각 3개국 최대 42개이며 확보 량에 따라 줄어듭니다.<br>사람이 human _*열을 채운 뒤 검수 지표를 계산합니다. |
| <a id="layout18-table-39-row-3"></a> Cohen’s κ와 일치율 | κ는 우연 일치를 고려한 분류 일치 지표입니다.일부만 채운 파일에서는 κ의 유효쌍과 일치율 분모가 달라질 수 있으므로 실제 채운 표본과 분모를 확인합니다. |
| <a id="layout18-table-39-row-4"></a> 폴더별 자료 역할 | data/는 수집 CSV·검수표본, 수집 결과/는 국가별 Excel 사본, 결과/분석 결과 _통합.xlsx는 통합 분석, 결과/figures/는 10 그래프,manual/은 수동 입력입니다.<br>자동 분류와 사람 정답을 구분해 읽습니다. |


<a id="semantic-limitations-level-5"></a>

### LEVEL 5 · 재실행·수집 실패와 해석의 한계

비확률 표 집·플랫폼별 기간/미제공값·접근 정책·식별자 변환·재작성·분류 대체를 재현 한계로 보존합니다. 기본 사본과 이전 사본의 인증 차이를 기록하고 저장 행수나 통계 유의성을 국민 전체 대표성으로 확대하지 않습니다.

| 조건·자료 | 의미와 확인 방법 |
| --- | --- |
| <a id="layout18-table-40-row-1"></a> 대표성과 기간 | 공식 채널·인기 순 댓글 중심의 비확률 표본입니다.<br>국가 전체 소비자를 대표하지 않습니다.<br>홈페이지에는 SNS와 같은 기간 필터가 적용되지 않습니다. |
| <a id="layout18-table-40-row-2"></a> 접근 과 정규화 | robots.txt 조회 실패는 허용으로 처리됩니다.<br>URL 정규화는 대소 문자를 바꾸므로 대소 문자를 구분하는 게시물 ID의 링크가 맞는지 확인해야 합니다. |
| <a id="layout18-table-40-row-3"></a> 재작성되는 파일 | 원본 Excel 사본을 사용하지만 같은 이름 출력 Excel·CSV·검수표본은 재실행 시 다시 씁니다.<br>사람이 채운 검수 파일은 먼저 별도 보존합니다. |
| <a id="layout18-table-40-row-4"></a> 증상별 확인 점 | Excel 오류는 DATA_DIR·파일/시트,YouTube 실패는 키·서비스 설정·쿼터, 빈 웹 수집은 페이지 구조·JS·접근 조건을 확인합니다.<br>미지원 채널은 manual CSV, 감성 차이는 모델/사전/사람 표본, 한글 오류는 폰트 설정을 봅니다. |

[동일 수준 프로젝트 안내](../%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A85.md)

<!-- reading-levels17:end -->

한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다.

분야: 자연어 처리 › 다국어 콘텐츠 분류 › pandas·Excel·통계·사람 검수

[목적](#purpose) · [기능](#features) · [입출력](#flow) · [구성](#files) · [준비](#setup) · [사용법](#usage) · [결과](#results) · [제약](#limits) · [변경](#changes)

<a name="purpose"></a>

<a id="-이-단계에서-하는-일"></a>

## 연구 목적

노트북은 입력 Excel을 읽고 결과 사본을 작성합니다. 수집과 분류 뒤에는 국가별 표·그래프·통계 검정 과 사람 검수 표본을 따로 구성해 자동 분류의 결과를 확인합니다.

<a name="features"></a>

<a id="-주요-기능과-처리-방식"></a>

## 방법과 구현

| 구성 | 실제 역할 |
| --- | --- |
| <a id="layout18-table-41-row-1"></a> 입력과 수집 | 원본 Excel6개, YouTube·홈페이지와 수동 CSV를 연결합니다. |
| <a id="layout18-table-41-row-2"></a> 분류 | 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다. |
| <a id="layout18-table-41-row-3"></a> 시트와 분석 | CSV·Excel 사본, 국가별 그래프와 카이제곱·Kruskal–Wallis·상관 분석을 구성합니다. |
| <a id="layout18-table-41-row-4"></a> 사람 검수 | human 열을 채울 표본을 만들고 Cohen κ·일치율을 계산하는 함수를 제공합니다. |


<a name="flow"></a>

<a id="-입력--처리--출력"></a>

## 입력·처리·출력

| 입력 | 처리 | 출력 |
| --- | --- | --- |
| 채널 Excel·수동 CSV | 수집·URL·날짜 정리 | 홈페이지·게시물·댓글 표 |
| 텍스트와 메타데이터 | 규칙 또는 다국어 감성 모델·수동값 우선 분류 | 분류 CSV·Excel 사본 |
| 분류 결과·검수값 | 비교표·그래프·통계·일치도 | 국가별 차이와 분류 한계 확인 |

<a name="files"></a>

<a id="-파일과-핵심-처리"></a>

## 파일별 역할

| 파일 | 이용 방법 |
| --- | --- |
| [2차/포켓몬 30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) | 설정·함수·실행 셀 |
| [2차/포켓몬 30주년_올인원_이전도커버전.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90_%EC%9D%B4%EC%A0%84%EB%8F%84%EC%BB%A4%EB%B2%84%EC%A0%84.ipynb) | 설정·함수·실행 셀 |
| [2차/공개집계/분류별_건수.csv](../../2%EC%B0%A8/%EA%B3%B5%EA%B0%9C%EC%A7%91%EA%B3%84/%EB%B6%84%EB%A5%98%EB%B3%84_%EA%B1%B4%EC%88%98.csv) | 원정밀도 표 |

<a id="-함수셀로-찾아가기"></a>

### 관련 함수와 셀

관련 함수와 셀을 파일별로 정리했습니다. 실행 전 설정과 호출 순서, 출력 경로를 확인하세요.

| 파일 | 핵심 정의 |
| --- | --- |
| <a id="layout18-table-44-row-1"></a> [2차/포켓몬 30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) | 셀 4: `_kw` · `_count` · `classify_purpose` · `classify_proposals` · `classify_msg_type` · `classify_intent` · `classify_topics` · `_load_sent_model`<br>셀 6: `nfc` · `find_file` · `norm_platform` · `read_channels` · `read_homepage_urls`<br>셀 9: `yt_get` · `yt_uploads_playlist` · `yt_collect_videos` · `yt_collect_comments` · `collect_youtube`<br>셀 11: `collect_bilibili`<br>셀 13: `robots_ok` · `fetch_html` · `_date_in` · `parse_blocks` · `collect_homepage`<br>셀 15: `manual_name` · `make_manual_templates` · `norm_url` · `load_manual`<br>셀 17: `parse_count` |
| <a id="layout18-table-44-row-2"></a> [2차/포켓몬 30주년_올인원_이전도커버전.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90_%EC%9D%B4%EC%A0%84%EB%8F%84%EC%BB%A4%EB%B2%84%EC%A0%84.ipynb) | 셀 4: `_kw` · `_count` · `classify_purpose` · `classify_proposals` · `classify_msg_type` · `classify_intent` · `classify_topics` · `_load_sent_model`<br>셀 6: `nfc` · `find_file` · `norm_platform` · `read_channels` · `read_homepage_urls`<br>셀 9: `yt_get` · `yt_uploads_playlist` · `yt_collect_videos` · `yt_collect_comments` · `collect_youtube`<br>셀 11: `collect_bilibili`<br>셀 13: `robots_ok` · `fetch_html` · `_date_in` · `parse_blocks` · `collect_homepage`<br>셀 15: `manual_name` · `make_manual_templates` · `norm_url` · `load_manual`<br>셀 17: `parse_count` |


<a name="setup"></a>

<a id="️-환경과-설정"></a>

## 실행 환경과 설정

| 항목 | 조건·기본값 |
| --- | --- |
| 기간 | START_DATE=2026-01-01·END_DATE=None |
| 수집 상한 | 채널당 영상 100·영상당 댓글 30·relevance 정렬 |
| 기본 파일 인증 | YOUTUBE_API_KEY가 없으면 YouTube 수집 건너뜀 |
| Docker 이름 사본 | GOOGLE_API_KEY가 없으면 초기화에서 중단 |
| 산출 위치 | data/·수집결과/·결과/·manual/ |

<a name="usage"></a>

<a id="-준비와-사용-순서"></a>

## 실행 순서

1. 입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다.
2. 수집 기간·공식 채널 링크와 API를 사용할 범위를 정하고 미지원 자료는 수동 CSV에 준비합니다.
3. 수집→분류→시트 사본 작성→분석 구간을 나누어 읽고 필요한 단계만 실행합니다.
4. human 열을 사람이 채운 표본을 별도로 보관한 뒤 κ·일치율의 유효쌍 수를 확인합니다.
5. 기존 결과를 다시 볼 때는 data CSV와 결과 Excel·그래프를 먼저 열어 새 수집과 구분합니다.

<a name="results"></a>

<a id="-결과를-읽는-방법"></a>

## 결과와 해석

보관된 data와 검수 표본 파일의 행 수입니다.

| 자료 | 보관된 data | 검수 표본 파일 |
| --- | --- | --- |
| 댓글 | 5585 행 | 100 행 |
| 게시물 | 400 행 | 28 행 |
| 홈페이지 | 73 행 | 35 행 |

검수 표본 파일의 행 수는 사람이 검수를 모두 마친 건수와 같은 뜻이 아닙니다.

참여율은(좋아요 +댓글 +공유)/조회 수 ×100이고 YouTube 공유 수는 제공되지 않는 값을 0으로 기록합니다. Wilson 구간·카이제곱/Cramér V·Kruskal–Wallis/ε²·Mann–Whitney/Bonferroni·Spearman 결과는 표본과 유효 건수를 함께 읽습니다.

<a name="limits"></a>

<a id="️-알려진-제약과-확인-지점"></a>

## 제약과 확인 사항

| 상황 | 확인할 내용 |
| --- | --- |
| <a id="layout18-table-47-row-1"></a> 대표성 | 공식 채널·인기순 댓글 중심의 비확률 표본이며 국가 전체 소비자 의견으로 일반화하지 않습니다. |
| <a id="layout18-table-47-row-2"></a> 수집·정규화 | 홈페이지 기간 필터·robots 조회 실패 허용·URL 소문자화가 자료 연결과 표본에 영향을 줍니다. |
| <a id="layout18-table-47-row-3"></a> 분류 대체 | 감성 모델 로드 실패 시 사전 방식으로 전환하고 수동 분류값이 있으면 우선합니다. |
| <a id="layout18-table-47-row-4"></a> 재실행 | 같은 이름의 CSV·Excel·검수 표본을 다시 쓰므로 사람이 채운 파일은 별도 보관합니다. |


<a name="changes"></a>

<a id="-이전-단계와의-변화"></a>

## 직전 단계와 비교

1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다.

2차 기본 파일과 이전 Docker 사본은 인증 환경 변수와 시작 일 중복 선언의 차이를 구분합니다.

[직전 단계 전체 비교·구성](step-2.patch)

<details>
<summary>이 단계의 파일 기록과 전체 해시</summary>

아래 내용는 해당 단계가 기록될 당시의 파일 정보입니다. 현재 첨부는 [프로젝트 자료 안내](../../README.md)에서 확인할 수 있습니다.

| 구분 | 파일 |
| --- | --- |
| <a id="layout18-table-48-row-1"></a> 추가 | `data/comments.csv` |
| <a id="layout18-table-48-row-2"></a> 추가 | `data/hp_all.csv` |
| <a id="layout18-table-48-row-3"></a> 추가 | `data/review_sample_comments.csv` |
| <a id="layout18-table-48-row-4"></a> 추가 | `data/review_sample_hp.csv` |
| <a id="layout18-table-48-row-5"></a> 추가 | `data/review_sample_posts.csv` |
| <a id="layout18-table-48-row-6"></a> 추가 | `data/sns_posts.csv` |
| <a id="layout18-table-48-row-7"></a> 추가 | `manual/일본_Instagram_comments.csv` |
| <a id="layout18-table-48-row-8"></a> 추가 | `manual/일본_Instagram_posts.csv` |
| <a id="layout18-table-48-row-9"></a> 추가 | `manual/일본_X_comments.csv` |
| <a id="layout18-table-48-row-10"></a> 추가 | `manual/일본_X_posts.csv` |
| <a id="layout18-table-48-row-11"></a> 추가 | `manual/일본_YouTube_comments.csv` |
| <a id="layout18-table-48-row-12"></a> 추가 | `manual/일본_YouTube_posts.csv` |
| <a id="layout18-table-48-row-13"></a> 추가 | `manual/중국_Bilibili_comments.csv` |
| <a id="layout18-table-48-row-14"></a> 추가 | `manual/중국_Bilibili_posts.csv` |
| <a id="layout18-table-48-row-15"></a> 추가 | `manual/중국_Weibo_comments.csv` |
| <a id="layout18-table-48-row-16"></a> 추가 | `manual/중국_Weibo_posts.csv` |
| <a id="layout18-table-48-row-17"></a> 추가 | `manual/한국_Instagram_comments.csv` |
| <a id="layout18-table-48-row-18"></a> 추가 | `manual/한국_Instagram_posts.csv` |
| <a id="layout18-table-48-row-19"></a> 추가 | `manual/한국_X_comments.csv` |
| <a id="layout18-table-48-row-20"></a> 추가 | `manual/한국_X_posts.csv` |
| <a id="layout18-table-48-row-21"></a> 추가 | `manual/한국_YouTube_comments.csv` |
| <a id="layout18-table-48-row-22"></a> 추가 | `manual/한국_YouTube_posts.csv` |
| <a id="layout18-table-48-row-23"></a> 추가 | `결과/figures/fig01_homepage_format_purpose.png` |
| <a id="layout18-table-48-row-24"></a> 추가 | `결과/figures/fig02_homepage_proposal_types.png` |
| <a id="layout18-table-48-row-25"></a> 추가 | `결과/figures/fig03_message_type.png` |
| <a id="layout18-table-48-row-26"></a> 추가 | `결과/figures/fig04_engagement_distribution.png` |
| <a id="layout18-table-48-row-27"></a> 추가 | `결과/figures/fig05_engagement_by_strategy.png` |
| <a id="layout18-table-48-row-28"></a> 추가 | `결과/figures/fig06_platform_heatmap.png` |
| <a id="layout18-table-48-row-29"></a> 추가 | `결과/figures/fig07_monthly_trend.png` |
| <a id="layout18-table-48-row-30"></a> 추가 | `결과/figures/fig08_sentiment.png` |
| <a id="layout18-table-48-row-31"></a> 추가 | `결과/figures/fig09_intent.png` |
| <a id="layout18-table-48-row-32"></a> 추가 | `결과/figures/fig10_topics.png` |
| <a id="layout18-table-48-row-33"></a> 추가 | `결과/분석결과_통합.xlsx` |
| <a id="layout18-table-48-row-34"></a> 추가 | `공개집계/README.md` |
| <a id="layout18-table-48-row-35"></a> 추가 | `공개집계/분류별_건수.csv` |
| <a id="layout18-table-48-row-36"></a> 추가 | `수집결과/일본 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-37"></a> 추가 | `수집결과/일본 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-38"></a> 추가 | `수집결과/중국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-39"></a> 추가 | `수집결과/중국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-40"></a> 추가 | `수집결과/한국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-41"></a> 추가 | `수집결과/한국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-42"></a> 추가 | `일본 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-43"></a> 추가 | `일본 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-44"></a> 추가 | `중국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-45"></a> 추가 | `중국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-46"></a> 추가 | `포켓몬30주년_올인원.ipynb` |
| <a id="layout18-table-48-row-47"></a> 추가 | `포켓몬30주년_올인원_이전도커버전.ipynb` |
| <a id="layout18-table-48-row-48"></a> 추가 | `한국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-49"></a> 추가 | `한국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| <a id="layout18-table-48-row-50"></a> 이전에만 존재 | `brand_nps_auto_pipeline_v2.ipynb` |


</details>

---

[프로젝트](../../README.md) · [전체 차수](../REVISION_INDEX.md) · [자료 폴더](../../2%EC%B0%A8) · [1차](step-1.md)


<a id="layout18-table-14-row-1"></a><a id="layout18-table-14-row-2"></a><a id="layout18-table-14-row-3"></a><a id="layout18-table-14-row-4"></a><a id="layout18-table-18-row-1"></a><a id="layout18-table-18-row-2"></a><a id="layout18-table-18-row-3"></a><a id="layout18-table-18-row-4"></a><a id="layout18-table-23-row-1"></a><a id="layout18-table-23-row-2"></a><a id="layout18-table-23-row-3"></a><a id="layout18-table-23-row-4"></a><a id="layout18-table-27-row-1"></a><a id="layout18-table-27-row-2"></a><a id="layout18-table-27-row-3"></a><a id="layout18-table-27-row-4"></a><a id="layout18-table-32-row-1"></a><a id="layout18-table-32-row-2"></a><a id="layout18-table-32-row-3"></a><a id="layout18-table-32-row-4"></a><a id="layout18-table-36-row-1"></a><a id="layout18-table-36-row-2"></a><a id="layout18-table-36-row-3"></a><a id="layout18-table-36-row-4"></a><a id="layout18-table-5-row-1"></a><a id="layout18-table-5-row-2"></a><a id="layout18-table-5-row-3"></a><a id="layout18-table-5-row-4"></a><a id="layout18-table-9-row-1"></a><a id="layout18-table-9-row-2"></a><a id="layout18-table-9-row-3"></a><a id="layout18-table-9-row-4"></a>

</details>

