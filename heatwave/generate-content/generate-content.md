# HeatWave 데이터베이스 내 LLM을 사용하여 콘텐츠 생성 및 요약

## 세션 소개

HeatWave GenAI는 두 개의 데이터베이스 내 대규모 언어 모델(LLM)을 지원합니다: mistral-7b-instruct-v1 및 llama2-7b-v1, llama3-8b-instruct-v1. 이러한 모델을 사용하여 응답을 생성하거나 요약할 수 있습니다.

_Estimated Time:_ 10 minutes 소요

### 목표

이 Lab에서는 다음과 같은 작업들을 진행합니다.

- 데이터베이스 내 LLM을 사용하여 응답 생성.
- 데이터베이스 내 LLM을 사용하여 텍스트 요약.

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험

## 작업 1:  데이터베이스 내 LLM을 사용하여 응답(Generate) 생성

1. HeatWave에 LLM 로드합니다. **Enter** 수행합니다.:

    - llama3-8b-instruct-v1 모델을 로드하려면:

        ```bash
        <copy>call sys.ML_MODEL_LOAD('llama3-8b-instruct-v1', NULL);</copy>
        ```

        ![image](https://github.com/user-attachments/assets/aa1d6050-84b9-4314-9080-3a60e7d3d696)

2. 자연어로 된 쿼리를 @query 세션 변수에 설정하고 **Enter** 수행합니다.

    ```bash
    <copy>set @query="<자연어로 질의>";</copy>
    ```

    For example:
    
    ```bash
    <copy>set @query="What is the use of generative AI in 200 words";</copy>
    ```
3. 다음 명령을 입력하여 LLM에서 응답을 생성하세요. 

    ```bash
    <copy>select sys.ML_GENERATE(@query, JSON_OBJECT("task", "generation", "model_id", "llama3-8b-instruct-v1"));</copy>
    ```

    or

    ```bash
    <copy>select sys.ML_GENERATE(@query, JSON_OBJECT("task", "generation", "model_id", "llama3-8b-instruct-v1", "language", "ko"));</copy>
    ```
        
    ![image](https://github.com/user-attachments/assets/d745dabb-36f8-4ffa-b155-f263fe78a874)

4. HeatWave GenAI는 데이터베이스 내 LLM을 사용하여 응답을 생성합니다.

    ![image](https://github.com/user-attachments/assets/1112b344-0031-406a-9aef-fb74927d8e0a)

## 작업 2: 데이터베이스 내 LLM을 사용하여 텍스트 요약 (Summarize)

1. 요약하려는 텍스트를 정의하고 **Enter**를 클릭하세요.

    ```bash
    <copy>set @text="<TextToSummarize>";</copy>
    ```

    For example:
    ```bash
    <copy>set @text="Artificial Intelligence (AI) is an ever-expanding field that holds immense potential to transform our societal and professional landscapes. AI pertains to the creation of computer systems capable of simulating human intelligence to carry out tasks such as visual perception, speech recognition, decision-making, and language translation. A significant stride in AI development is the ascension of machine learning, a segment of AI that empowers computers to glean insights from data without explicit programming. By analyzing copious amounts of data and recognizing patterns, machine learning algorithms are becoming increasingly proficient at forecasting outcomes and making decisions. The integration of AI is already underway across diverse industries, ranging from healthcare and finance to transportation. In the healthcare sector, AI is playing a pivotal role in crafting personalized treatment plans for patients based on their unique medical history and genetic composition. In finance, AI is instrumental in detecting fraudulent activities and offering investment advice. Furthermore, in transportation, AI is driving advancements in self-driving vehicle technology and optimizing traffic management systems. Despite the manifold advantages associated with AI, there exist apprehensions regarding its potential societal impact. Some express concern about the possibility of AI leading to job displacement, as machines become more adept at performing tasks traditionally undertaken by humans. Additionally, there are worries about the potential malicious applications of AI technology.";</copy>
    ```

    ![image](https://github.com/user-attachments/assets/24ea5eaf-21d1-49c9-b38f-2d442e0d38bc)

2. 다음 명령을 입력하여 요약된 텍스트를 생성하고 **Enter**를 클릭합니다.

    ```bash
    <copy>select sys.ML_GENERATE(@text, JSON_OBJECT("task", "summarization", "model_id", "llama3-8b-instruct-v1"));</copy>
    ```

    or

    ```bash
    <copy>select sys.ML_GENERATE(@text, JSON_OBJECT("task", "summarization", "model_id", "llama3-8b-instruct-v1", "language", "ko"));</copy>
    ```   

    ![image](https://github.com/user-attachments/assets/05084c40-b9e7-4372-a537-5ff7c1f911fa)

 4. LLM은 귀하의 텍스트 요약을 생성합니다.:

    ![image](https://github.com/user-attachments/assets/0dcf8469-27b6-4f37-96a7-771dd9f34fe7)


이제 다음 Lab으로 진행할 수 있습니다.

## Learn More (관련 문서)

- [HeatWave User Guide](https://dev.mysql.com/doc/heatwave/en/)

- [HeatWave on OCI User Guide](https://docs.oracle.com/en-us/iaas/mysql-database/index.html)

- [MySQL Documentation](https://dev.mysql.com/)


## Acknowledgements

- **Author** - Aijaz Fatima, Product Manager
- **Contributors** - Mandy Pang, Senior Principal Product Manager, Aijaz Fatima, Product Manager
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, December 2024

