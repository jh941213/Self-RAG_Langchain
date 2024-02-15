# Self-RAG_Langchain


# Self-RAG

## 프로젝트 개요

Self-RAG는 자기 성찰을 통해 RAG(Retrieval-Augmented Generation)의 성능을 향상시키는 새로운 접근 방식을 제시하는 최근 논문입니다. 이 프로젝트는 [Self-RAG 논문](https://arxiv.org/abs/2310.11511)에서 소개된 아이디어를 LangGraph를 사용하여 구현하는 방법을 보여줍니다.

회사 독스 Open data 파인튜닝 시킬 독스데이터를 CSV 파일로 변형해서 리트리버를 해주었습니다.

## 종속성

본 프로젝트를 시작하기 전에 `OPENAI_API_KEY` 환경 변수를 설정해야 합니다.

## Self-RAG 상세 설명

Self-RAG는 LLM(예: LLaMA2-7b 또는 13b)을 훈련시켜 RAG 과정을 몇 가지 방식으로 제어하는 토큰을 생성하는 흥미로운 접근 방식을 소개합니다. 이 프레임워크는 다음과 같은 과정을 포함합니다:

1. 검색기 `R`에서 검색할지 여부 결정
   - 토큰: `Retrieve`
   - 입력: `x (질문)` 또는 `x (질문)`, `y (생성물)`
   - 출력: `yes, no, continue`

2. 검색된 패시지 `D`가 질문 `x`와 관련이 있는지 여부 판단
   - 토큰: `ISREL`
   - 입력: (`x (질문)`, `d (chunk)`) for `d` in `D`
   - 출력: `relevant, irrelevant`

3. 각 `D` 청크에서 LLM 생성물이 해당 청크와 관련이 있는지 여부 (환각 등)
   - 토큰: `ISSUP`
   - 입력: `x (질문)`, `d (chunk)`,  `y (생성물)` for `d` in `D`
   - 출력: `fully supported, partially supported, no support`

4. 각 `D` 청크에서 LLM 생성물이 `x (질문)`에 대한 유용한 응답인지 여부
   - 토큰: `ISUSE`
   - 입력: `x (질문)`, `y (생성물)` for `d` in `D`
   - 출력: `{5, 4, 3, 2, 1}`

이 과정을 그래프로 표현할 수 있습니다:

(이미지는 실제 GitHub 저장소에 업로드된 후 적절한 링크로 교체해야 합니다)

## 구현하기

LangGraph를 사용하여 이러한 아이디어를 처음부터 구현하는 방법은 [LangGraph 문서](https://python.langchain.com/docs/langgraph)를 참조하세요.

---

이 README는 프로젝트의 기본적인 개요와 구현 세부 사항에 대한 지침을 제공합니다. 구체적인 구현 방법, 사용 예시, 필요한 종속성 설치 방법 등을 포함하여 프로젝트의 효율적인 사용을 위한 충분한 정보를 제공해야 합니다.
