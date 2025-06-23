## Top-Down Decision Tree 

이번 파트는 결정 트리(Decision Tree)가 Top-Down 방식으로 학습되는 과정을 보여준다 

Top-Down는 말 그래도 위에서부터 학습한다는 의미이다 

![image](https://github.com/user-attachments/assets/4b3ad294-25da-4772-96e5-8c7f20d13163)

<br/>

질문의 선택 방법은 다음과 같다 

1. 카테고리 옵션을 최대한 많이 제거할 수 있는가 

2. 라벨에 대한 정보를 최대한 많이 드러나는가  (ex: 양말을 신은 사람으로 분류 -> 별로 도움이 안됨)
<br/>

## Top-Down 과정 

Top-Down에서 분류하는 알고리즘을 **ID3 알고리즘**이라고 한다 (아래 설명)

1. 모든 데이터가 같은 라벨이면 → 리프 노드 생성하고 종료

2. 그렇지 않으면 가장 좋은 특징(feature Xj)을 고름

3. 고른 특징으로 새로운 노드 생성

4. 그 특징의 가능한 값(v)마다 데이터를 나누고, 각 부분에 대해 재귀 호출

5. 트리의 노드를 반환

<br/>

즉, **모든 노드의 있는 모든 샘플이 동일해야만 종료됨 -> 종료 조건**

위 과정에서 핵심은 2번의 가장 좋은 특징을 고르는 것이다 

만약 가장 좋은 특징을 랜덤하게 고른다면 성능도 떨어지고 비효율적일 것이다 

이를 해결하기 위해 나온 개념이 **info gain** 이다

<br/>

## information gain &  ID3 알고리즘

**info gain** : 어떤 특징으로 데이터를 나눴을 때, **그 결과가 얼마나 "순수"해졌는지를 측정하는 값이다**

이때, 순수하다는 것은 라벨이 한쪽으로 몰렸다는 것이다 

즉, 분류를 했을 때 **분리도가 얼마나 높냐를 판단하는 개념이다**

<br/>

**ID3 알고리즘 : 결정 트리를 생성하는 알고리즘으로, 데이터를 반복적으로 나누며 분류 규칙을 학습함**

**Information Gain(정보이득)** 이 가장 큰 특징 (즉, 분리도가 가장 높은 특징)을 선택하여 분류함 

<br/>

## Entropy

그럼 info gain의 개념을 컴퓨터에게 어떻게 정의시켜줘야 할까?

답은 바로 entropy의 개념을 사용하는 것이다 

<br/>

## Entropy 예시 

![스크린샷 2025-04-14 131834](https://github.com/user-attachments/assets/002bd1c6-256a-4e36-928d-afe6faacaeec)

<br/>

## Info gain 예시 

![스크린샷 2025-04-14 131804](https://github.com/user-attachments/assets/5379c088-80e7-4e96-9abd-89499c0c341f)

![image](https://github.com/user-attachments/assets/4fe4cf57-4ffe-4cb5-9a49-69920a9a413d)

<br/>

## 풀이과정 

tennis 예시 테이블이 흐릿하게 보이는 관계로 아래에 따로 표를 제시함 

![IMG_3090](https://github.com/user-attachments/assets/c656ca2f-af06-458c-885c-e43195d757c0)

![IMG_3116](https://github.com/user-attachments/assets/c78f53c2-5545-425a-a7de-f92746049799)

<br/>

## 강의 예시 - 당뇨병 특징 예측 

아래 예시는 어떤 특징이 당뇨병 여부를 잘 설명하는지 알아보는 예이다 

현재 데이터를 기반으로 다음 분류 기준을 High BP(고혈압)으로 잡을 것인지, 아니면 EDUCATION(교육 수준 즉,학년)으로 분류할 것인지 

entropy값을 기준으로 탐색 

![스크린샷 2025-04-14 134106](https://github.com/user-attachments/assets/4e92c0cb-0ae1-4fcb-b767-f9b12537d705)

<br/>

## 풀이과정 

![IMG_3091](https://github.com/user-attachments/assets/c61501fd-374b-4171-927a-b88ffb6d7601)

<br/>

즉 과정은 아래와 같다 

1. 현재 entropy 구하기

2. 분리하는 대상 Yes의 entropy, no의 entropy

3. (분리하는 대상 entrop) x (분리하는 대상의 비율) 의 합 

4. 현재 entropy - 3번의 차이를 구함 = info gain

<br/>

## info gain 문제점 

**IG의 문제점은 자식 노드 수가 많은 특징을 선호함**

예를 들어, IG는 entropy를 가장 작게 만드는 방향을 선호하는데 

**n개의 샘플을 n개로 나눠버리면 entropy는 감소하나 의미가 없어짐**

이것을 해결한 것이 **Gain Ratio (정보이득 비율)** 이다 

<br/>

## Gain Ratio (정보이득 비율)

Gain ratio의 핵심 아이디어는 분리 기준에 의해 분리된 노드가 많다면, 당연히 더 적게 분리된 기준보다 entropy가 낮을 것임으로 개수를 감안해서 entropy를 계산해야 한다는 것이다. 아래는 Gain ratro의 정의이다 

![image](https://github.com/user-attachments/assets/b4fc8ac5-7c46-432a-ac72-47db4b0aa6b2)

위 이미지에서 splitinfo 공식은 복잡해 보이지만, 그냥 **확률 x 로그 확률이라는 의미이다**

<br/>

## Gain Ratio 예시 

![image](https://github.com/user-attachments/assets/bd1f27f9-6954-4f02-bd11-713707b38c02)

<br/>

따라서 splitinfo를 구하는 과정은 아래와 같다

1. (분리하는 대상의 비율) x log(분리하는 대상의 비율)

2. 1번의 합 구하기

위 과정을 시행한 뒤 info gain에서 나눠주면 된다 

<br/>

## 풀이과정 

![IMG_3092](https://github.com/user-attachments/assets/5ff06719-69b0-4a86-b251-06f66042272a)

<br/>

## Gini index

![image](https://github.com/user-attachments/assets/0e7851ab-c634-4af4-9639-d22366535ddf)

<br/>

## Gini 예시 및 풀이과정

![IMG_3093](https://github.com/user-attachments/assets/2c00f16f-734a-43af-831c-efc467f721e8)

Gini index도 info gain과 마찬가지로 

순수한 노드를 선호하므로 **자식이 많을수록 유리해 보이는 경향이 있음**

따라서 **과적합의 위험성이 있음**

<br/>

## 연속형 특성 처리 

실생활 문제에서 아래 예시와 같이 연속형 특성인 문제가 많이 존재함 

<br/>

## 감기 예시 

![image](https://github.com/user-attachments/assets/cf35e460-5b8d-49aa-9753-6eb23e1a5cdd)

이런 경우 오른쪽 상단 트리와 같이 **임계값을 기준으로 이진 분할로 바꿔야함**

<br/>

## Decision tree + 회귀 

Decision tree를 회귀에서 사용하는 방법은 아래와 같다 

![IMG_3094](https://github.com/user-attachments/assets/6f2a4d27-72d1-45f9-9dcf-75863f98e917)

<br/>

## 실제 Decision tree + 회귀 결과 함수 

![image](https://github.com/user-attachments/assets/c27cfc9c-24cd-42bd-882f-27bdf9504c80)

파란색 선의 max_depth가 2라는 것은 트리를 2번까지만 분리했다는 의미이다 

이렇게 트리의 깊이가 낮으면 데이터의 흐름은 따라가지만, 세부적인 변화는 놓친다

<br/>

반면 연두색 선은 최대 깊이가 5인데 자세히 보면 아래 작은 점들(noise) 까지 변화를 감지하는 모습을 보여준다 

이것은 **깊이가 너무 깊어지면 과적합의 위험성이 있다는 것을 의미한다**

<br/>

## Reduced-Error Pruning

**Prune : 가지를 치다**

트리가 너무 복잡하면 과적합 문제 발생. 이를 해결하기 위해 **불필요한 분기를 잘라내는(가지치기) 과정이 필요함**

해당 서브트리의 정확도가 학습 데이터에서는 좋지만, 평가 데이터에서는 안 좋을 때 

컴퓨터가 다수의 클래스로 (ex: 만약 당뇨 예측이라면 해당 노드의 당뇨환자와 비당뇨환자 중 더 많은 인원이 다수 클래스가 됨) 리프 노드를 만들어 전환함

여기서 리프 노드로 만든다는 의미는 그 부분에서 더 이상 나눌 필요가 없고 그냥 다수 클래스로 판단을 내어버린다는 뜻 

<br/>

만약 오류가 많은 노드에 비당뇨 환자가 더 많다면, 거기서 더 나누지 않고 그냥 비당뇨로 예측해버림 

![IMG_3095](https://github.com/user-attachments/assets/343507ec-5d6c-433c-af99-097f0dd8582b)

만약 서브 트리를 부분적으로 삭제하고 싶다면 CART 사용(강의에서 다루진 않지만 마지막 슬라이드에 참고로 나옴)

<br/>

pruning 과정을 거치면, **학습 데이터에서는 성능이 떨어지지만, 평가 데이터에서 성능이 올라간다**

<br/>

## Decision tree 특징 

## 1. 스케일링 및 정규화 불필요 

결정 트리는 Information Gain, Gain Ratio 같은 기준으로 분할을 결정함

이 기준들은 특성 값의 실제 크기보다 순서와 비율에 따라 결정되므로, 값이 크든 작든 상관없음.

예를 들어, 키(cm)를 m로 바꿔도 상관 관계는 똑같음 

<br/>

## 2. non-parameter 모델이다 

노드마다 어떤 특성을 기준으로 나눌지, 연속형 변수라면 임계값은 뭘로 할지 선택해야 함

하지만 **트리는 사전에 파라미터 개수를 고정하지 않음 → 학습된 트리의 복잡도는 데이터에 따라 달라짐**

최대 깊이 d를 고정하면 파라미터 수도 고정되지만, 보통은 그렇지 않음

즉, **트리는 학습을 통해 스스로 구조를 만들며 복잡도를 조절하는 모델**

**k-NN과 마찬가지로, 데이터를 바탕으로 모델이 구조를 형성**

<br/>

## 3. 손실함수로 최적화하지 않음 

물론 우리는 정확도를 높이고 싶어함

하지만 **ID3는 탐욕적 방법(greedy) 으로 분기마다 info gain을 최대화하는 특성을 고름** 

(여기서 greedy 알고리즘이란 눈 앞에 더 좋은 상황의 방향으로 가는 것을 말함 -> tree 눈 앞에 현재 조건을 바탕으로 판단)

**따라서, 전체 트리에 대한 손실 함수를 정의하지 않음**

즉, 결정 트리는 로지스틱 회귀나 신경망처럼 명시적 손실 함수 기반 학습이 아니라, **국소적으로 기준에 따라 구조를 만든다는 점이 핵심**

<br/>

## 참고 

![image](https://github.com/user-attachments/assets/95647f7f-ae88-4f30-a0b7-01a292933ba4)














































