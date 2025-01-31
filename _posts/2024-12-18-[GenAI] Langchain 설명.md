---
layout: post
---

### 1. Langchain 구성도

![image](https://github.com/user-attachments/assets/45763e4d-9670-42e4-81c0-514ed0b355ff)

- Models
  - Langchaine 모델은 다양한 LLM(OpenAI, Hugging Face, Cohere, GPT4ALL..)과 상호 연동을 위한 표준 인터페이스 제공

- Prompts
  - 사용자 질의를 효과적으로 하기 위해 템플릿 포함 다양한 툴을 포함하고 있는 LLM에 질의하는 인터페이스 제공

- Indexes
  - 다양한 외부 데이터(vector db, 문서등)와 연동을 위한 인터페이스 제공
 
- Chains
  - 여러 모델이나 프롬프트를 결합하는 호출 시퀀스를 생성하는 체인 인터페이스 제공

- Agents
  - 사용자 태스크를 완성하기 위해 필요한 사용자 입력, 결정등을 위한 컴포넌트 기반에 agent 인터페이스 제공
 
- Memory
  - 사용자 질의(agent, chain등 통해서)의 결과에 대한 상태 유지를 통해 일관된 문맥(context)를 제공
 
### 2. Langchain 중요한 3가지 
- Chat models   
  LangChain 설명서를 참조하세요. OpenAI(상업적 API)를 사용하고 싶지 않다면 상업적 대안으로 Anthropic을 제안하고, 오픈 소스 대안으로 Ollama를 제안합니다.

- Embeddings   
  LangChain 설명서를 참조하세요. OpenAI(상업적 API)를 사용하고 싶지 않다면 상업적 대안으로 Cohere를 제안하고, 오픈 소스 대안으로 Ollama를 제안합니다.

- Vector stores   
  LangChain 설명서를 참조하세요. PGVector(인기 있는 SQL 데이터베이스 Postgres의 오픈 소스 확장)를 사용하고 싶지 않다면 Weaviate(전용 벡터 스토어) 또는 OpenSearch(인기 있는 검색 데이터베이스의 일부인 벡터 검색 기능)를 사용하는 것이 좋습니다.



### 3. 사용예제 (prompt)
```
from langchain.chat_models import ChatOpenAI
from langchain.agents import load_tools, initialize_agent, AgentType
llm = ChatOpenAI(model_name="gpt-3.5-turbo", temperature=0)
tools = load_tools(["wikipedia", "llm-math"], llm=llm)
agent = initialize_agent(
    tools, llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True
)
question = """ """
agent.run(question)
```
