<a id="-2차--한중일-포켓몬-콘텐츠-비교"></a>

# 2차 · 한·중·일 포켓몬 콘텐츠 비교

한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동의도·토픽을 비교하는 분석 단계입니다.

분야: 자연어 처리 › 다국어 콘텐츠 분류 › pandas·Excel·통계·사람 검수

[목적](#purpose) · [기능](#features) · [입출력](#flow) · [구성](#files) · [준비](#setup) · [사용법](#usage) · [결과](#results) · [제약](#limits) · [변경](#changes)

<a name="purpose"></a>

<a id="-이-단계에서-하는-일"></a>

## 연구 목적

노트북은 입력 Excel을 읽고 결과 사본을 작성합니다. 수집과 분류 뒤에는 국가별 표·그래프·통계 검정과 사람 검수 표본을 따로 구성해 자동 분류의 결과를 확인합니다.

<a name="features"></a>

<a id="-주요-기능과-처리-방식"></a>

## 방법과 구현

| 구성 | 실제 역할 |
| --- | --- |
| 입력과 수집 | 원본 Excel6개, YouTube·홈페이지와 수동 CSV를 연결합니다. |
| 분류 | 목적 3종·제안 4종·내부자형/초대형·감성-1/0/1·행동의도 O/X·토픽을 정리합니다. |
| 시트와 분석 | CSV·Excel 사본, 국가별 그래프와 카이제곱·Kruskal–Wallis·상관 분석을 구성합니다. |
| 사람 검수 | human 열을 채울 표본을 만들고 Cohen κ·일치율을 계산하는 함수를 제공합니다. |

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
| [2차/포켓몬 30주년_올인원.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90.ipynb) | 셀 4: `_kw` · `_count` · `classify_purpose` · `classify_proposals` · `classify_msg_type` · `classify_intent` · `classify_topics` · `_load_sent_model`<br>셀 6: `nfc` · `find_file` · `norm_platform` · `read_channels` · `read_homepage_urls`<br>셀 9: `yt_get` · `yt_uploads_playlist` · `yt_collect_videos` · `yt_collect_comments` · `collect_youtube`<br>셀 11: `collect_bilibili`<br>셀 13: `robots_ok` · `fetch_html` · `_date_in` · `parse_blocks` · `collect_homepage`<br>셀 15: `manual_name` · `make_manual_templates` · `norm_url` · `load_manual`<br>셀 17: `parse_count` |
| [2차/포켓몬 30주년_올인원_이전도커버전.ipynb](../../2%EC%B0%A8/%ED%8F%AC%EC%BC%93%EB%AA%AC30%EC%A3%BC%EB%85%84_%EC%98%AC%EC%9D%B8%EC%9B%90_%EC%9D%B4%EC%A0%84%EB%8F%84%EC%BB%A4%EB%B2%84%EC%A0%84.ipynb) | 셀 4: `_kw` · `_count` · `classify_purpose` · `classify_proposals` · `classify_msg_type` · `classify_intent` · `classify_topics` · `_load_sent_model`<br>셀 6: `nfc` · `find_file` · `norm_platform` · `read_channels` · `read_homepage_urls`<br>셀 9: `yt_get` · `yt_uploads_playlist` · `yt_collect_videos` · `yt_collect_comments` · `collect_youtube`<br>셀 11: `collect_bilibili`<br>셀 13: `robots_ok` · `fetch_html` · `_date_in` · `parse_blocks` · `collect_homepage`<br>셀 15: `manual_name` · `make_manual_templates` · `norm_url` · `load_manual`<br>셀 17: `parse_count` |

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

보관된 data에는 댓글 5585행·게시물 400행·홈페이지 73행이 있습니다. 검수 표본 파일은 댓글 100행·게시물 28행·홈페이지 35행이며, 사람 검수를 모두 마친 건수와 같은 뜻은 아닙니다.

참여율은(좋아요+댓글+공유)/조회수×100이고 YouTube 공유수는 제공되지 않는 값을 0으로 기록합니다. Wilson 구간·카이제곱/Cramér V·Kruskal–Wallis/ε²·Mann–Whitney/Bonferroni·Spearman 결과는 표본과 유효 건수를 함께 읽습니다.

<a name="limits"></a>

<a id="️-알려진-제약과-확인-지점"></a>

## 제약과 확인 사항

| 상황 | 확인할 내용 |
| --- | --- |
| 대표성 | 공식 채널·인기순 댓글 중심의 비확률 표본이며 국가 전체 소비자 의견으로 일반화하지 않습니다. |
| 수집·정규화 | 홈페이지 기간 필터·robots 조회 실패 허용·URL 소문자화가 자료 연결과 표본에 영향을 줍니다. |
| 분류 대체 | 감성 모델 로드 실패 시 사전 방식으로 전환하고 수동 분류값이 있으면 우선합니다. |
| 재실행 | 같은 이름의 CSV·Excel·검수 표본을 다시 쓰므로 사람이 채운 파일은 별도 보관합니다. |

<a name="changes"></a>

<a id="-이전-단계와의-변화"></a>

## 직전 단계와 비교

1차 리뷰·소셜 NPS에서 한·중·일 콘텐츠의 수집·분류·시트·통계 비교로 분석 목적을 확장했습니다.2차 기본 파일과 이전 Docker 사본은 인증 환경변수와 시작일 중복 선언의 차이를 구분합니다.

[직전 단계 전체 비교·구성](step-2.patch)

<details>
<summary>이 단계의 파일 기록과 전체 해시</summary>

아래 표는 해당 단계가 기록될 당시의 파일 정보입니다. 현재 첨부는 [프로젝트 자료 안내](../../README.md)에서 확인할 수 있습니다.

| 구분 | 파일 |
| :--- | :--- |
| 추가 | `data/comments.csv` |
| 추가 | `data/hp_all.csv` |
| 추가 | `data/review_sample_comments.csv` |
| 추가 | `data/review_sample_hp.csv` |
| 추가 | `data/review_sample_posts.csv` |
| 추가 | `data/sns_posts.csv` |
| 추가 | `manual/일본_Instagram_comments.csv` |
| 추가 | `manual/일본_Instagram_posts.csv` |
| 추가 | `manual/일본_X_comments.csv` |
| 추가 | `manual/일본_X_posts.csv` |
| 추가 | `manual/일본_YouTube_comments.csv` |
| 추가 | `manual/일본_YouTube_posts.csv` |
| 추가 | `manual/중국_Bilibili_comments.csv` |
| 추가 | `manual/중국_Bilibili_posts.csv` |
| 추가 | `manual/중국_Weibo_comments.csv` |
| 추가 | `manual/중국_Weibo_posts.csv` |
| 추가 | `manual/한국_Instagram_comments.csv` |
| 추가 | `manual/한국_Instagram_posts.csv` |
| 추가 | `manual/한국_X_comments.csv` |
| 추가 | `manual/한국_X_posts.csv` |
| 추가 | `manual/한국_YouTube_comments.csv` |
| 추가 | `manual/한국_YouTube_posts.csv` |
| 추가 | `결과/figures/fig01_homepage_format_purpose.png` |
| 추가 | `결과/figures/fig02_homepage_proposal_types.png` |
| 추가 | `결과/figures/fig03_message_type.png` |
| 추가 | `결과/figures/fig04_engagement_distribution.png` |
| 추가 | `결과/figures/fig05_engagement_by_strategy.png` |
| 추가 | `결과/figures/fig06_platform_heatmap.png` |
| 추가 | `결과/figures/fig07_monthly_trend.png` |
| 추가 | `결과/figures/fig08_sentiment.png` |
| 추가 | `결과/figures/fig09_intent.png` |
| 추가 | `결과/figures/fig10_topics.png` |
| 추가 | `결과/분석결과_통합.xlsx` |
| 추가 | `공개집계/README.md` |
| 추가 | `공개집계/분류별_건수.csv` |
| 추가 | `수집결과/일본 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `수집결과/일본 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 추가 | `수집결과/중국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `수집결과/중국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 추가 | `수집결과/한국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `수집결과/한국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 추가 | `일본 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `일본 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 추가 | `중국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `중국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 추가 | `포켓몬30주년_올인원.ipynb` |
| 추가 | `포켓몬30주년_올인원_이전도커버전.ipynb` |
| 추가 | `한국 30주년 공식 홈페이지 콘텐츠 분석용 시트.xlsx` |
| 추가 | `한국 공식 SNS 게시물 및 정량 반응 분석용 시트.xlsx` |
| 이전에만 존재 | `brand_nps_auto_pipeline_v2.ipynb` |

</details>

---

[프로젝트](../../README.md) · [전체 차수](../REVISION_INDEX.md) · [자료 폴더](../../2%EC%B0%A8) · [1차](step-1.md)
