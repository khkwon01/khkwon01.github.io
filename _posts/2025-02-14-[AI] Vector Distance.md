---
layout: post
---

## Vector Distance

Vector 공간에 거리 측정하는 것은 사용자 질문(쿼리)에 가장 가까운 거리에 있는 결과를 식별하는 기술입니다.

(데이터베이스에서 사용하는 where 조건에 keyword로 데이터 조회하는 것과는 매우 다른 방식입니다.)

Vectors를 가지고 작업할때 두 vector간에 얼마나 유사한지 또는 다른지 에 대한 거리를 계산하는 방식은 여러가지가 있습니다.

일반적으로 사용자 질의에 대해 Vector 검색시 **벡터를 생성하는 벡터 임베딩 모델을 학습하는 데 사용된 거리 측정법에 맞는 거리 측정법**을 사용하는 것이 가장 좋습니다.


- Euclidean and Euclidean Squared Distances

  유클리드 거리는 비교되는 각 벡터의 좌표 사이의 거리를 반영합니다. 기본적으로 두 벡터 사이의 직선 거리입니다.

  이는 벡터 좌표에 적용된 피타고라스 정리를 사용하여 계산됩니다(SQRT(SUM((xi-yi)2))).

  ![image](https://github.com/user-attachments/assets/9285862e-0266-49cd-8025-f9fde3225cec)


- Cosine Similarity

  가장 널리 사용되는 유사도 측정 기준 중 하나는, 특히 자연어 처리(NLP)에서 코사인 유사도입니다. 이는 두 벡터 사이 각도의 코사인을 측정합니다.

  ![image](https://github.com/user-attachments/assets/946c6258-ee08-4ca0-b046-36a18f59581f)


- Dot Product Similarity

  두 벡터의 점곱 유사성은 각 벡터의 크기에 각 벡터의 코사인을 곱하는 것으로 볼 수 있습니다.

  이 정의에 대한 해당 기하학적 해석은 두 벡터 중 하나의 크기에 두 번째 벡터를 첫 번째 벡터에 투영한 크기를 곱하는 것과 같거나 그 반대입니다.

  ![image](https://github.com/user-attachments/assets/cb53d2d1-fff2-4f6c-b0ac-1626dddcf326)
