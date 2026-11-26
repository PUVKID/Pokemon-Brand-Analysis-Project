<!-- language-choice:start -->
🔵 **한국어** · [English overview](../en/README.md)
<!-- language-choice:end -->

<a id="-2차"></a>

# 2차

<!-- reading-levels17:start -->
<details>
<summary>읽기 수준 선택</summary>

| 레벨 | 읽는 목적 |
| --- | --- |
| [LEVEL 1 - Beginner](../docs/%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A81.md) | 목적과 입력·출력을 쉬운 말로 이해하기 |
| [LEVEL 2 - Explorer](../docs/%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A82.md) | 주요 기능과 전체 처리 흐름 살펴보기 |
| [LEVEL 3 - Practitioner](../docs/%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A83.md) | 설정·실행 순서와 결과 확인하기 |
| [LEVEL 4 - Advanced](../docs/%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A84.md) | 구현 선택과 조건·한계 비교하기 |
| [LEVEL 5 - Expert](../docs/%EC%9D%BD%EA%B8%B0%EC%95%88%EB%82%B4/%EB%A0%88%EB%B2%A85.md) | 세부 근거와 재현 조건 검토하기 |

</details>
<!-- reading-levels17:end -->

한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다.

| 주요 구성 | 내용 |
| --- | --- |
| <a id="layout18-table-1-row-1"></a> 입력과 수집 | 원본 Excel6개, YouTube·홈페이지와 수동 CSV를 연결합니다. |
| <a id="layout18-table-1-row-2"></a> 분류 | 목적 3 종·제안 4 종·내부자형/초대형·감성-1/0/1·행동 의도 O/X·토픽을 정리합니다. |
| <a id="layout18-table-1-row-3"></a> 시트와 분석 | CSV·Excel 사본, 국가별 그래프와 카이제곱·Kruskal–Wallis·상관 분석을 구성합니다. |
| <a id="layout18-table-1-row-4"></a> 사람 검수 | human 열을 채울 표본을 만들고 Cohen κ·일치율을 계산하는 함수를 제공합니다. |


<a id="-이용-순서"></a>

## 이용 순서

1. 입력 Excel6개와 DATA_DIR·시트 구조를 확인합니다.
2. 수집 기간·공식 채널 링크와 API를 사용할 범위를 정하고 미지원 자료는 수동 CSV에 준비합니다.
3. 수집→분류→시트 사본 작성→분석 구간을 나누어 읽고 필요한 단계만 실행합니다.
4. human 열을 사람이 채운 표본을 별도로 보관한 뒤 κ·일치율의 유효쌍 수를 확인합니다.
5. 기존 결과를 다시 볼 때는 data CSV와 결과 Excel·그래프를 먼저 열어 새 수집과 구분합니다.

| 차수·단계 | 주요 내용 | 자료 | 직전 비교 |
| --- | --- | --- | --- |
| <a id="layout18-table-2-row-1"></a> [2차](../docs/revisions/step-2.md) | 한국·중국·일본의 홈페이지·SNS·댓글을 수집하거나 수동 CSV로 보완하고 목적·메시지·감성·행동 의도·토픽을 비교하는 분석 단계입니다. | [폴더](.) | [전체 비교](../docs/revisions/step-2.patch) |


[프로젝트](../README.md) · [전체 차수](../docs/REVISION_INDEX.md)
