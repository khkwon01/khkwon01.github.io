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

### 2. 사용예제 (prompt)
