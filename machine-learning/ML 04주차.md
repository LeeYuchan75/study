## Classification

아래 이미지와 같이 두 개의 class를 구분 짓는 선을 **decision boundary** 라고 함 

![image](https://github.com/user-attachments/assets/808baaaf-b194-44a5-a272-1d3465ae2c07)

## Non-linear model 

실제 클래스를 구분하는 과정에서 선형적으로 분리가 안 되는 경우가 많다

이런 경우 비선형적으로 분리하는데, 이 원리가 바로 **basis expansion(기저 확장)** 이다 

기저란 공간을 구성하는 기본 벡터 집합 즉, **모든 데이터를 표현할 수 있는 표현 단위** 이다 

따라서 입력 벡터의 차원을 확장하여 아래와 같이 표현함 

![image](https://github.com/user-attachments/assets/0dcbd241-0ade-422f-88d8-96788f20ae7c)

위 이미지는 데이터가 직선(선형)으로 나눠지지 않기 때문에 비선형 결정 경계를 사용한 것이다 

비선형 모델의 원리는 **기저 확장(basis Expansion)** 이다

예를 들어 원래 특성 x = [1, x₁, x₂] 만으로는 한계가 있기 때문에 왼쪽 벡터와 같이 나타내어 표현 가능 

직관적으로 해석하면 ex : x1 = 면적, x2 = 방 개수 라면 x1 * x2는 집의 규모

<br/>

![스크린샷 2025-04-05 124415](https://github.com/user-attachments/assets/26a6e607-aa53-4c59-a00f-653f160a101d)

이 함수는 예측이 틀린 경우만 1로 계산해서, 전체에서 **틀린 비율(=오류율)** 을 계산하는 수식이다 

위 함수는 좋은 성능 지표지만, **불연속**하고, 수학적으로 **기울기**를 계산할 수 없어서 Gradient Descent 같은 방법으로 학습이 안 됨

-> **최적화(학습)** 에는 적합하지 않다

## Sigmoid function

위 식을 더 부드럽게 만들기 위해 

1. 큰 양수 → 클래스 1일 확률 ↑ (≈ 1)

2. 큰 음수 → 클래스 0일 확률 ↑ (≈ 0)

3. 0 근처 → 애매한 위치 → 확률 ≈ 0.5

와 같이 근사적으로 표현하여 부드럽게 표현할 수 있다 

이때 βTx 값의 범위는 (−∞,∞)이기 때문에 0~1 사이의 의미 있는 확률로 바꾸기 위해 **시그모이드 함수를 이용한다**

![image](https://github.com/user-attachments/assets/841524fd-3426-40cd-9e17-17dcb8b30a87)

위 첫번째 공식에서 p(y=1∣x;β) 의미는 '입력 x와 파라미터 β가 주어졌을 때, 정답이 1일 확률' 로 해석한다 

**Sigmoid function의 decision boundary는 0.5이다**

<br/>

## Soft Non-linear Decision Boundaries

아래는 비선형 모델과 시그모이드 함수를 사용했을 때 결과이다 

![스크린샷 2025-04-05 130659](https://github.com/user-attachments/assets/db35b658-0327-47a6-b879-677bb0272dc5)

<br/>

## Likelihood of Logistic Regression 

선형 회귀 : 수치를 예측하는 모델

로지스틱 회귀 : 확률을 예측해 분류하는 모델

Likelihood란 모델이 실제 라벨들을 맞출 확률을 의미

이 확률이 높을수록 → 그 모델은 그 데이터를 잘 설명하고 있음

이 확률이 낮을수록 → 모델이 데이터를 잘 설명하지 못함

![image](https://github.com/user-attachments/assets/ff9bdfc3-8b05-4e22-8cc5-57889cf24636)

왼쪽 이미지는 파란 점과 노란 삼각형이 깔끔하게 나뉘어 있음

모델의 결정 경계(직선)가 정확히 라벨들을 구분하고 모델이 데이터를 잘 설명함

⇒ High likelihood 

<br/>

오른쪽 이미지는 점들이 결정 경계를 중심으로 뒤섞여 있음 많은 예측이 틀릴 확률이 높음

⇒ Low likelihood 

<br/>

## MLE(Maximum Likelihood Estimation)

![image](https://github.com/user-attachments/assets/e53f26fc-dbbb-40b7-8a5d-ae5055fb17f5)

첫번째 식은 예측한 확률이 정답에 가까울수록 likelihood가 높아진다는 의미이다 

만약 모델이 어떤 𝑥1 에 대해 클래스 1일 확률을 0.9로 예측했다면

𝑦1 = 1 이면 → likelihood = 0.9

𝑦1 =0 이면 → likelihood = 0.1 -> 잘못 예측한 경우 반대 확률을 사용하여 더 좋은 모델로 학습하도록 함 

<br/>

두번째 식의 의미는 첫번째 식을 일반화 한 것인데, 각각의 확률을 모두 곱한다는 의미이다 

모든 값을 더한 뒤 평균을 구하지 않고 곱하는 이유는 **각각의 샘플이 독립적이기 때문이다**

우리는 전체 샘플을 동시에 맞을 확률을 구하고 싶기 때문임 (위 식은 오차가 아니라 정답률 기준) 

**따라서 이 값을 최대화를 시키는 방향으로 접근해야 함. 이것을 MLE라고 한다**

<br/>

하지만 샘플의 값은 0~1 사이의 값이기 때문에 계속하여 곱하면 값이 너무 작아진다는 문제점이 있다 

**이것을 해결한 것이 바로 로그의 활용이다**

<br/>

## MLE 정리 

![image](https://github.com/user-attachments/assets/04b97d6b-d51e-486b-bb4f-515bde522361)

위와 같이 마이너스로 표현한 이유는 대부분의 최적화 알고리즘은 최소화 방식으로 설계되어 있기 때문에 다음과 같이 변형하여 사용

또한 arg min은 최소로 반드는 β값이다 (ex: 이차함수의 해의 값과 같이 결과 값이 아니라 x값을 구하는 것과 유사)

-> 이렇게 해서 실제 β값과 β의 예측률의 차이를 이용 

<br/>

또한 마지막 공식을 보면 일반화가 되어 있는데 

yi = 1 일 때, 첫 번째 로그를, yi = 0 일 때, 두 번째 로그를 사용한다는 의미이다

이때, hβ는 오른쪽 상단 공식과 같이 시그모이드를 활용한 값이기 때문에 연속 함수로 표현되고 

로그의 덧셈 과점에서 연속 함수 x 연속 함수를 시행하기 때문에 위 식은 미분이 가능하다 

<br/>

![image](https://github.com/user-attachments/assets/fce46012-15ed-400f-b86c-6daa853f5991)

오른쪽 함수에서 값이 커질수록 변화가 미미하지만, 값이 작아지면 변화가 크게 일어난다

**이것은 모델의 예측이 틀릴 수록 패널티를 더 크게 준다는 의미이다**

**𝑝𝛽 (𝑌 =1 | 𝑥𝑖)는 입력 𝑥𝑖에 대해, 모델 파라미터 𝛽를 사용했을 때, 클래스 1일 확률을 의미함**

위에서는 모델이 입력 𝑥𝑖에 대해 클래스 1일 확률이 100%라고 확신한다는 뜻

<br/>

![image](https://github.com/user-attachments/assets/88574e7d-7189-42ad-93ac-973cc517c3c4)

위 미분 과정의 마지막 부분을 보면 선형 회귀와 기울기를 계산하는 방법이 유사하다 (gradient = error x input feature)

**따라서, 로지스틱 회귀와 선형 회귀의 기울기 계산은 매우 유사하다**

<br/>

## MAP(Maximum A Posteriori)

![image](https://github.com/user-attachments/assets/69527c4b-7dbd-4ed3-9c5c-3a0b386094d4)

Posteriori는 라틴어로 '경험 이후에'라는 뜻 미리 값을 예상하여 그것을 확률에 기반한다는 의미이다 

**결론부터 말하면, MAP는 MLE에 정규화를 해준 것이다**

![image](https://github.com/user-attachments/assets/acae7f03-4d16-4029-a83d-0490749b50f0)

위 공식의 전개하여 마지막 부분을 보면 정규화가 됐다는 것을 확인할 수 있다 (알고만 넘어가기)

**p(β)=N(0,σ^2I)는 𝛽가 평균이 ０이고 분산이 σ^2인 정규 분포를 따른다는 의미로 𝛽가 0에 가까운 값으로 지정할 수 있음**

또한, L1 은 Laplace(라플라스) 사전 확률과 유사하고 L2는 Gaussian(가우시안) 함수와 같다 (week 4. p.34,36)

<br/>

Laplace : 대부분의 𝛽가 정확히 0이어야 한다는 강한 믿음. 끝이 뾰족한 형태로  모델이 𝛽= 0 을 매우 강하게 선호

Gaussian : 대부분의 𝛽가 0에 가까울수록 자연스러움. 큰 값을 완전히 배제하지는 않음 → 부드러운 제약, 모든 값을 허용하되 작을수록 좋다고 여김

위 성질 때문에 Laplace는 불필요한 feature가 많을 때 사용하고, Gaussian은 모든 feature이 조금씩 중요할 때 사용한다

<br/>

## Smaller 𝛽 -> Hedging your bet

![스크린샷 2025-04-05 184421](https://github.com/user-attachments/assets/df93c680-0c8b-4548-b77d-a06caceb06a4)

왼쪽 Sigmoid 함수보다 오른쪽 Sigmoid 함수의 𝛽값이 더 작음(음수가 있어서 절댓값이 클수록 작다고 표현)

위 이미지처럼 𝛽가 더 작아질수록 (음의 무한으로 갈수록) 시그모이드가 매우 가파르게 변하여, 0 또는 1 근처로 확신이 강해짐 

**𝛽의 절댓값이 작으면 모델은 더 부드럽고 안정적인 예측**

**𝛽의 절댓값이 크면 모델은 더 극단적인 확신을 가지게 됨 -> 과적합**

<br/>

## 정규화의 역할 

정규화는 𝛽가 커지는 걸 막음. 즉, 너무 확신하는 모델을 억제함

그래서 훈련 데이터에만 과하게 적합되는 Overfitting 을 방지할 수 있다 

<br/>

## 정규화 장점

작은 𝛽 → 부드러운 결정 → 베팅을 분산함

특히 데이터가 작거나 noisy(잡음이 많을 때) 더 효과적이다 

만약 정규화 없이 훈련을 한다면, β가 매우 커질 수 있고, 모델은 훈련 데이터에 매우 확신 있는(극단적인) 결정을 하게 된다 (𝛽의 절댓값이 클 때의 현상과 동일)

이렇게 되면 발산의 위험성이 생기고 과적합 위험성이 커지게 된다 -> 정규화를 사용하면 모델이 너무 극단적인 결정을 내리지 않게 하여 발산을 막아줌

<br/>

## Multi-class Classification : Softmax

![image](https://github.com/user-attachments/assets/a2e8c64f-129f-4767-a531-d160f372a2b8)

다중 클래스 분류는 3개 이상의 클래스를 분류할 때 사용한다

여기서 핵심은 Softmax 함수를 사용하여 전체 확률의 합이 1이 되게 만들어주는 것이 핵심이다 

예: [3, 1, 0] → [0.84, 0.11, 0.05] (큰 값일수록 높은 확률)

위 예에서 [3, 1, 0]의 softmax 결과가 [3/4, 1/4, 0]가 **아닌 이유는** softmax는 단순히 비율을 계산하는 게 아니라, **지수 함수를 사용해서** 각 값을 확률로 변환하기 때문이다

이렇게 하여 가장 확률이 높은 클래스를 답으로 출력한다 

<br/>

## Classification Metrics

**모든 상황에서 정확도가 좋은 지표는 아니다**

예시1 : 불균형 데이터 문제

전체 데이터 중 99%가 음성(negative, y=0)일 때

모델이 항상 fβ(x) = 0만 예측해도 정확도 99%가 나옴 (모든 결과를 예측 없이 항상 0이라는 결과만 내놓은 모델)

<br/>

예시2 : 세상을 잘 모르는 어린 아이의 범죄가, 범죄를 많이 한 사람보다 더 나음 

범죄, 의료, 금융 등에서는 정확도만 보는 건 위험함

<br/>

## Confusion Matrix

![image](https://github.com/user-attachments/assets/8576fb8a-476f-4f2b-bfa4-b713f6de9904)

TP (True Positive)	실제 양성, 예측도 양성	

TN (True Negative)	실제 음성, 예측도 음성	

FP (False Positive)	실제는 음성, 예측은 양성	

FN (False Negative)	실제는 양성, 예측은 음성

암기 방법: TP, TN = 정답 + 정답을 뭐로 예측했는지 ,  FP, FN = 오답 + 오답을 뭐로 예측했는지(실제 정답은 반대 P -> N이 정답)

앞에는 정답 여부, 뒤에는 예측한 것 

![image](https://github.com/user-attachments/assets/1ff3c8ef-05a5-41c2-a860-4951f462a069)

<br/>

## 에시 

![image](https://github.com/user-attachments/assets/db6ed0d1-3a60-4ef1-93ce-30b4ac57e5d0)

**위에서 Accuracy = 0.8이지만 양성일 때 양성을 맞춘 수가 상대적으로 너무 적음**

이 모델은 불균형 데이터에서는 오히려 위험할 수 있기 때문에 적합한 모델이 아님 

<br/>

## Precision and Recall

![IMG_3073](https://github.com/user-attachments/assets/39bc1356-b721-4d20-adbc-0661eb541410)

**1. Recall (True positive rate)**

TPR(True positive rate) 라고도 부름 

실제 양성 중에서 얼마나 많이 맞췄는가 -> 놓치지 않는 능력 (False Negative를 줄이는 게 핵심)

사용되는 경우 : 의료 진단 (질병을 놓치면 안 됨), 스팸 필터링에서 스팸을 빠짐없이 잡아내야 할 때 등

직관적 해석 :'이 사람은 아닌 것 같아요' 라고 추측

<br/>

**2. Precision (positive predictive value)**

양성이라고 예측한 것 중 실제로 맞은 비율은 얼마인가 → 잘못된 긍정을 줄이는 능력 (False Positive를 줄이는 게 핵심)

사용되는 경우 : 형사 사건 (“한 명의 무고한 사람도 처벌받지 않아야 함”), 질병 예측에서 ‘양성’ 알람이 신뢰 가능해야 할 때

직관적 해석 : '이 사람이 맞는 거 같아요' 라고 추측 

![image](https://github.com/user-attachments/assets/422d7095-0900-4b8d-b3bb-f4e56b582091)

<br/>

## F1 score

**F1 score는 Precision와 Recall의 조화 평균이다**

식 자체는 2 x Precision x Recall / (Precision x Recall) 이고 이것을 계산하기 쉽게 아래와 같이 사용함 

![IMG_3075](https://github.com/user-attachments/assets/a3c41302-f83d-4b3c-8557-8c14e04d3040)

<br/>

## Optimizing Classification Metric

모델은 NLL를 최소화하면서 학습하지만,

**실제로 우리가 중요하게 여기는 평가지표(accuracy, F1 score 등)가 좋아지는 건 아님**

<br/>

**해결책 1. 훈련 전 양성(또는 음성) 샘플에 가중치를 더 줘서 학습**

예: positive가 적다면 → positive 샘플의 손실(loss)을 더 크게 반영하도록

이렇게 하면 학습 자체가 불균형 문제를 인식하고 대응하게 됨

<br/>

**해결책 2. 훈련 후 임계값을 조정해서 평가 지표를 높임**

예: 기본적으로 시그모이드 값이 0.5 이상이면 양성으로 예측하지만, 이를 0.7 이상이어야 양성으로 간주하도록 바꿀 수 있음

이렇게 하면 precision이나 recall 같은 지표를 조절 가능함































































