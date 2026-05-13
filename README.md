# Multi-Agent Exercise Recommendation System (LangGraph)

### 1. 프로젝트명
LangGraph 기반 맞춤형 건강 진단 및 운동 추천 에이전트 시스템

### 2. 기간
2026년 5월 13일

### 3. 기술스택
- **Orchestration:** LangGraph, LangChain
- **LLM:** Ollama (Model: `exaone3.5:2.4b`)
- **State Management:** TypedDict, AgentState
- **Environment:** Python, Jupyter Notebook

### 4. 에이전트 워크플로우 (Workflow)
사용자의 고민(Query)을 입력받아 **추출 -> 후보 선정 -> 답변 생성**의 3단계 에이전트 과정을 거쳐 최적의 솔루션을 제공합니다.

1. **Extractor Agent**: 질문에서 "체력 저하", "체중 증가" 등 핵심 증상을 키워드로 추출
2. **Candidate Agent**: 추출된 증상을 해결하는 데 도움이 되는 5가지 운동 후보군 선정
3. **Answer Agent**: 선정된 운동의 특징, 추천 이유, 추가 조언을 포함한 개조식 가이드 생성

### 5. 데이터 구조 및 전처리
- **AgentState 정의**: 에이전트 간의 데이터 전달을 위해 `query`, `symptoms`, `exercise_candidates`, `result`를 상태 객체로 관리
- **Prompt Engineering**: 
  - 각 단계별 에이전트에게 명확한 페르소나 부여
  - `Ollama(exaone3.5:2.4b)` 모델이 안정적인 한국어 출력을 생성하도록 프롬프트 최적화

### 6. LangGraph 아키텍처


**[Graph Structure]**
```text
+-----------+  
| __start__ |  
+-----------+  
      * +-----------+  
| extractor |  
+-----------+  
      * +-----------+  
| candidate |  
+-----------+  
      * +-----------+  
|  answer   |  
+-----------+  
      * +-----------+  
|  __end__  |  
+-----------+
```

### 7. 실행 결과 및 인사이트

**사용자 입력:** > "체력이 안좋고 살이 계속 찌는데 어떤 운동을 할까?"

**에이전트 최종 응답:** - **증상 설명**: 체력 향상과 체중 관리를 통한 건강 개선을 목표로 하며, 에너지 수준 강화와 체지방 감소를 최우선으로 진단함.
- **추천 운동 목록**: 유산소 운동, 고강도 인터벌 트레이닝(HIIT), 스쿼트, 플랭크, 걷기 인터벌
- **핵심 인사이트**:
  1. **효율성**: HIIT와 걷기 인터벌을 결합하여 짧은 시간 내 칼로리 소모 극대화
  2. **근력 강화**: 스쿼트와 플랭크를 통해 전신 근육 균형 및 코어 안정성 확보
  3. **지속성**: 현재 체력 수준에 맞춘 강도 설정 및 영양 관리와 운동 기록의 병행 강조

### 8. 프로젝트 특징 (Key Features)
- **Local LLM 활용**: `Ollama(exaone3.5:2.4b)`를 사용하여 데이터 보안성을 높이고, 비용 발생 없이 로컬 환경에서 추론 가능
- **멀티 에이전트 오케스트레이션**: `LangGraph`의 `StateGraph`를 통해 증상 추출, 후보 선정, 답변 생성이라는 복잡한 단계를 노드 단위로 분리하여 관리
- **유연한 상태 관리**: `TypedDict` 기반의 `AgentState`를 사용하여 에이전트 간 데이터 전달의 안정성 확보
- **개조식 한국어 출력**: LLM의 답변 형식을 엄격하게 통제하여 사용자 가독성을 높인 결과물 생성

### 9. Reference
1. **프레임워크 및 라이브러리**
   - [LangGraph](https://python.langchain.com/docs/langgraph/): 그래프 기반 에이전트 흐름 제어
   - [LangChain Community](https://python.langchain.com/docs/get_started/introduction): LLM 체인 및 프롬프트 템플릿 관리
   - [Ollama](https://ollama.com/): 오픈소스 로컬 LLM 서버

2. **사용 모델**
   - **EXAONE 3.5 (2.4B)**: LG AI Research에서 개발한 한국어 성능이 뛰어난 경량화 지시 모델

3. **분석 방법론**
   - **Multi-Agent Design Pattern**: 작업별 전문 에이전트를 배치하여 결과의 정확도와 품질 향상
   - **Prompt Engineering**: 증상 추출 및 운동 추천을 위한 단계별 프롬프트 최적화 기법 적용
