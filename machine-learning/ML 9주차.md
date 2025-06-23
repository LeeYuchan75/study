## 불확실성의 원천

우리가 사는 세상은 매우 불확실한 곳이다

**1. Uncertain inputs (불확실한 입력 값)**

- Missing data : 데이터가 누락됨

- Noisy data : 잡음이 섞인 데이터

<br/>

**2. Uncertain knowledge (불확실한 지식)**

- 여러 원인이 여러 결과를 초래함

- 조건이나 결과를 완전히 나열하지 못함

- 해당 분야에서 인과관계에 대한 지식이 불완전함

- 확률적(무작위적인) 효과들

<br/>

**3. Uncertain outputs (불확실한 결과)**

- 귀납과 유추는 본질적으로 불확실함

- 불완전한 연역 추론은 불확실할 수 있음

30년간의 인공지능 연구는 세상이 본질적으로 불확실하다는 사실을 피해 다녔다.

과거의 AI 연구는 실제로 세상이 예측 불가능하고 불확실하다는 점을 정면으로 다루지 않고, 그 문제를 피해가거나 외면한 것이다 

연구자들은 이러한 불확실성을 해결해야겠다고 생각했고, 이에 **베이즈 추론**을 제시했다

<br/>

## Bayesian inference (베이즈 추론)

**Bayesian Inference (베이즈 추론)** : 확률 이론과 독립성에 대한 정보를 사용한다

**확률적 추론**은 오직 **확률적인 결과**만을 제공한다

<br/>

## Discrete Random Variables (이산 확률 변수)

A를 확률 변수라고 하면 다음을 만족한다 

- A는 특정 값을 가질 수 있는 사건을 나타낸다 (ex: "시험에 합격했다" vs "불합격했다"처럼, 확률 변수는 여러 가능한 결과 중 하나를 가짐)

- 각 값에는 관련된 확률이 있다 (ex: A가 0(불합격), 1(합격)이라면, P(A=1)=0.7, P(A=0)=0.3 같은 확률이 할당함) 

<br/>

## 이진 확률 변수의 예시

**이진(binary)** : 결과가 두 가지(예/아니오, 0/1 등)만 가능한 확률 변수

**P(A)** : **A가 참인** 가능한 세계들의 비율

<br/>

**예시 1**

A는 "나는 두통이 있다" -> A=1이면 두통 있음, A=0이면 없음. 참/거짓으로 판단 가능한 사건

<br/>

**예시 2**

A는 "샐리가 2020년에 미국 대통령이 된다" ->  이 역시 참/거짓만 가능한 사건. 실제로 일어날 가능성이 매우 낮거나 0이지만, 확률적으로 기술 가능

<br/>

## 확률 변수 A의 시각화

![IMG_3281](https://github.com/user-attachments/assets/2a493336-80d7-445b-a140-048cd2e68783)

- **전체 공간 U**는 모든 가능한 세계(사건 공간)이다 따라서 **P(U) = 1**

- P(A)는 **빨간 타원의 면적**

- 따라서 **P(A) + P(¬A) = 1** 와 **P(¬A) = 1 − P(A) 만족**

<br/>

## Axioms of Probability (확률의 공리)

확률 이론의 기초는 러시아 수학자 콜모고로프가 정립한 세 가지 기본 법칙(공리)에 기반한다 

**공리** : **증명 없이 자명하게 참으로 받아들이는** 기본 명제

**확률의 세 가지 공리**

1. 모든 확률은 0 이상 1 이하이다

2. 항상 참인 명제는 확률이 1이고, 절대로 참이 될 수 없는 명제는 확률이 0이다 (P(true) = 1, P(false) = 0)

3. P(A∨B) = P(A) + P(B) − P(A∧B)

## P(¬A) = 1 + P(A) 증명

![image](https://github.com/user-attachments/assets/4f5f781c-3128-4322-a0fa-c6693fa48005)

<br/>

## Multi-valued Random Variables (다중값 확률 변수)

만약 A가 2개 이상의 값을 가질 수 있다고 하자 (ex: 시험 점수 A가 {A, B, C, D, F} 중 하나일 수 있음)

이때, A는 k개의 가능한 값을 가지는 **확률 변수**라고 한다

이 경우 다음과 같은 성질을 가진다   

![image](https://github.com/user-attachments/assets/a3d609e0-4931-4598-a30c-e1873becc02d)


- P(A = vi​ ∧A = vj) = 0 (if i != j) : A가 **동시에 vi와 vj가 되는 확률은 0**이다 (ex: 주사위는 동시에 2와 5가 될 수 없음)  

- P(A = v1 ∨ A = v2 ∨ ... ∨ A = vk) = 1: A는 **반드시 그 중 하나의 값**을 가짐 -> **전체 확률의 합은 1**

<br/>

## marginalization (주변화)

만약 우리가 B 사건의 확률을 구하고 싶다고 가정하자 

이때, 사건 B가 일어날 확률을 확률 변수 A의 가능한 값들에 대해 나누어서 계산하는 것이 **marginalization**이다 

![image](https://github.com/user-attachments/assets/27d76f17-d090-4e8f-a352-31c9f09d6063)

**예시**

- A: 오늘 날씨 → {맑음, 흐림, 비}

- B: 야외 행사가 열린다

그럼 P(B)는 다음처럼 계산할 수 있다 

p(B) = P(B ∧ 맑음) + P(B ∧ 흐림) + P(B ∧ 비)

<br/>

**marginalization은 다음과 같은 상황에서 유용하다**

1. 어떤 사건의 전체 확률이 궁금할 때 (ex: 야외 행사가 열릴 확률은 얼마인가?" -> 그런데 이건 날씨(A)에 따라 다름 -> marginalization으로 개별적으로 총 확률 계산)

2. 모델 설계에서 ‘숨겨진 변수’를 제거할 때 (ex: 유전자 상태(A)는 모르지만 질병 발생(B)의 확률은 알고 싶다면? 아래와 같이 식 작성 가능 

![image](https://github.com/user-attachments/assets/5f48e954-d49d-40bf-a126-5d5b3e823be0)

관측 불가능한 A를 수학적으로 없애줘서 원하는 값을 구할 수 있음 

<br/>

## Prior(사전 확률) & Joint(결합 확률)

**Prior Probability (사전 확률)** : 다른 정보를 고려하지 않고, 단일 사건에 대한 믿음의 정도

**Joint Probability (결합 확률)** : 여러 사건이 동시에 일어날 확률

**예시 : Alarm Domain**

세 가지 변수로 알람(Alarm), 도둑(Burglary), 지진(Earthquake)이 존재한다고 가정하자

만약 여기서 알람과 도둑의 관계를 보고싶다면 아래와 같이 표로 표현할 수 있고, marginalization으로 표현할 수도 있다 

![IMG_3283](https://github.com/user-attachments/assets/3808cfcc-372e-4016-9141-2dd892da047f)

<br/>

## Joint Distribution（결합 확률 분포）

d개의 변수에 대한 결합 분포를 만드는 방법은 다음과 같다 

1. 변수들의 모든 가능한 값을 나열한 **진리표(truth table)** 를 만든다 (만약 Boolean 변수 d개면, 테이블에는 2의 d제곱개의 행이 생긴다)

2. 각 조합에 대해, 그 조합이 일어날 확률을 지정

3. 확률의 공리를 따른다면, 그 모든 숫자의 합은 1이 되어야 한다

![image](https://github.com/user-attachments/assets/dacee06c-adee-454a-8223-04c734321b52)

<br/>

## 결합 확률 분포(Joint Probability)로부터 사전 확률(Prior Probability)을 계산 방법 

**핵심 개념**

- **결합 확률 분포(Joint Probability)** = **모든 변수 조합**의 확률

- **사전 확률(Prior Probability)** = **특정 변수 하나**의 단독 확률

이걸 구하려면 다른 변수들을 모두 “더해버리면” 됨. 즉 **Marginalization (주변화)** 이용

<br/>

## 예시

![IMG_3284](https://github.com/user-attachments/assets/7d9fd4bb-05a0-40b0-add4-a1427b8c6c39)

<br/>

## Conditional Probability (조건부 확률)

![IMG_3285](https://github.com/user-attachments/assets/b77a85dd-3adc-49ba-91ab-d2378e013ac2)

**조건부 확률** : 어떤 조건이 주어진 상황에서 다른 사건이 일어날 확률

**P(A∣B)** : B가 참인 세계들 중에서, A도 참인 세계들의 비율

![image](https://github.com/user-attachments/assets/8f16fad6-e9c9-4ed6-97bf-46874fe8ec4f)

**예시**

- B = “비가 온다”

- A = “우산을 썼다”

P(A∣B) = 비가 오는 날만 골라봤을 때, 그중에서 우산 쓴 날이 얼마나 되는지 보는 것

<br/>

## 조건부 확률 예시 

![image](https://github.com/user-attachments/assets/11180a54-3167-4885-9177-fc1487333932)

<br/>

## Priors(사전 확률)을 따로 계산하지 않고도 조건부 확률을 계산하는 방법

![IMG_3286](https://github.com/user-attachments/assets/0cec536f-5884-43f7-8b11-d97d7b92442b)

<br/>

## 조건부 확률 역 성립 x 예제 

![IMG_3287](https://github.com/user-attachments/assets/014c114a-10a8-4b16-a427-3f1dcd1f1043)

- 빨간 영역 Headache: 두통이 있는 경우

- 파란 영역 Flu: 독감인 경우

- 겹친 부분: 두통과 독감이 동시에 있는 경우

<br/>

위 상황을 설명하자면 두통이 있는 경우는 1/10 로 상대적으로 드물고 독감인 경우는 두통이 있는 경우보다 더 드물다 

하지만 독감이 있을 때, 두통이 있을 확률은 50 : 50의 확률로 빈번하게 일어난다 

**그럼 반대로 두통이 있을 때, 독감이 있을 확률도 50 : 50 일까?**

**답은 아니다**

<br/>

![스크린샷 2025-05-23 183422](https://github.com/user-attachments/assets/e602f6f9-a04f-46da-93d3-b061cab0dfde)

**하지만 베이즈 정리를 이용하면 역 추론이 가능하다**

<br/>

## Bayes' Rule (베이즈 정리)

![image](https://github.com/user-attachments/assets/3f8d7d0b-212f-4a07-81c3-e576e7816e20)

**Bayes' Rule (베이즈 정리)** : B가 일어난 상태에서 A가 일어날 확률은, A의 사전 확률에 B가 A일 때 일어날 조건부 확률을 곱한 뒤, B 전체 확률로 나누면 된다

**Bayes' Rule (베이즈 정리)** 는 확률적 머신러닝에서 가장 중요한 공식이다 

<br/>

이전 두통-독감 예시에서 역 추론을 구할 수 없었지만, 베이즈 정리를 통해 구할 수 있는 이유는 

베이즈 정리의 공식을 보면 아래 성질을 이용하여 **원인과 결과의 위치를 바꿔서 추론하기 때문이다**. 이것이 베이즈 정리가 중요한 이유이다

![image](https://github.com/user-attachments/assets/c87569e0-132e-4632-9701-8eb61ccd11f6)


<br/>

## 베이즈 정리 & 조건부확률 차이점 (중요)

조건부확률과 베이즈 정리의 차이점을 정리하자면 

조건부확률은 B가 일어났다는 사실을 알고 있을 때, A가 일어날 확률을 계산한 것처럼 **원인이 발생했을 때 결과가 나온 확률을 구한 것**이고

베이즈 정리는 결과가 나왔을 때, **해당 결과가 도출된 원인의 확률을 구한 것**이다

- **조건부확률 = 원인 -> 결과**

- **베이즈 정리 = 결과 -> 원인**


<br/>

## p.47 부터 공부 




