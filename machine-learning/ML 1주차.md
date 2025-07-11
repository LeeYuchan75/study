## Machine Learning (ML) 1주차

**머신 러닝** : 데이터에서 **규칙을 자동으로 학습할 수 있는 프로그램을** 만드는 것이다

**learning** : 시스템이 **경험을 통해 성능을 향상시키는** 모든 과정을 의미한다 

<br/>

Tom Mitchell(1988) 이 말한 기계학습의 기본 개념 

1. improve their performance 𝑃

2. at some task 𝑇

3. with experience 𝐸.

기계 학습에서는 시스템이 주어진 **작업(task)** 을 잘 수행하기 위해 **경험(experience)** 을 통해 **성능(performance)** 을 향상시킨다 < 𝑃, 𝑇, 𝐸 >.

<br/>

## Traditional algorithms 와 Machine learning algorithms

Traditional algorithms은 명시적인 규칙이나 절차에 따라 문제를 해결함. **주어진 입력에 대해 미리 정해진 규칙에 따라 결과를 도출하는 방식이다**

Machine learning algorithms은 데이터에서 **패턴을 스스로 학습하여 문제를 해결하는 방식이다.** 즉, 모델을 학습한 뒤, 주어진 입력에 대해 예측을 수행. 또한 ML은 output으로 결과 + 룰을 도출함 

<br/>

학습된 모델은 다음과 같은 용도로 사용할 수 있다 

1. 데이터에서 패턴/구조/주제/추세/등을 감지

2. 미래 데이터에 대한 예측을 하고 결정을 내림

<br/>

## What is Machine Learning ?

Machine learning is a “data-driven (데이터 기반)” approach to tackling various problems.

No need to pre-define the rules by humans (infeasible/impossible cases)

The rules are not “static”; can adapt as the ML algorithms ingest more and more data

머신 러닝은 다양한 문제를 해결하기 위한 "데이터 기반" 접근 방식이고,

인간이 규칙을 미리 정의할 필요가 없다(불가능하거나 불가능한 경우)

또한, 규칙은 "정적"이지 않으며, ML 알고리즘이 점점 더 많은 데이터를 수집함에 따라 적응할 수 있다 

<br/>

## Hierarchy of Artificial Intelligence

![Image](https://github.com/user-attachments/assets/1c00b703-9c6d-4e6d-b328-222232a1be45)

<br/>

**인공지능(AI)** 은 인간의 행동을 모방하는 것을 목표로 하는 모든 과학과 기술을 통합한다

**머신 러닝(ML)** 시스템은 명시적으로 프로그래밍되지 않고도 경험을 통해 자동으로 학습하고 개선할 수 있는 기능을 갖추고 있다

**딥러닝(DL)** 은 신경망(딥 피처 + 신경망 분류기)이 사용되는 머신러닝의 특수한 경우임

쉽게 얘기하면, 인공지능(AI)은 사람의 일을 대신 할 수 있다면, 모두 ai라고 한다

예를 들어, 강아지와 고양이를 분류하는 Traditional algorithm(즉, 룰 베이스로 만든 프오그램)도 사람의 일을 모방하는 것이기 때문에 일종의 ai라고 할 수 있다

여기서 머신러닝은 그 ai 중에서 스스로 학습하는 능력을 갖춘 시스템이고, 딥러닝은 머신러닝 중에서 수 많은 뉴런을 이용하여 계층구조로 이루어진 시스템이다 

<br/>

## Supervised Learning (지도 학습)

Supervised Learning이란 **정답(Label)** 이 있는 데이터를 이용해 모델을 학습시키는 기계 학습 방법이다. 즉, **입력(Input)과 출력(Output, 정답)** 이 주어진 상태에서 모델이 입력을 보고 출력을 예측하도록 학습하는 방식

지도 학습의 핵심은 데이터를 변환하는 함수를 학습하는 것이다 

Given: training data as labeled instances {(𝑥1, 𝑦1) ,…,(𝑥𝑁,𝑦𝑁)}

Goal: Learn a rule (𝑓: 𝑥 → 𝑦) to predict outputs 𝑦 for new inputs x

<br/>

![Image](https://github.com/user-attachments/assets/25ba7dea-11f5-4e64-b717-dde43bde498d)

<br/>

## Unsupervised Learning (비지도 학습)

**Unsupervised Learning(비지도 학습)** 이란 **정답(Label) 없이** 데이터를 학습하는 기계 학습 방법

Given: training data in form of unlabeled instances {𝑥1,…,𝑥𝑁}

Goal: Learn the intrinsic latent structure that summarizes/explains data

* intrinsic : 내재적, 본질적 / latent : 잠재적, 숨어 있는 

<br/>

![image](https://github.com/user-attachments/assets/04c9fee2-c9b5-4fe4-bd23-3fe2f60f6f9a)

<br/>

## ML from function approximation perspective 

Supervised learning (“predict output given input”) can be usually thought of as learning a function 𝑓 that maps each input to the corresponding output

Unsupervised learning (“model/compress inputs”) can be usually thought of as learning a function 𝑓 that maps each input to a compact representation.

지도 학습("입력이 있을 때 출력 예측")은 일반적으로 각 입력을 해당 출력으로 매핑하는 함수 𝑓를 학습하는 것으로 생각할 수 있고

비지도 학습("모델/압축 입력")은 일반적으로 각 입력을 압축된 표현으로 매핑하는 함수 𝑓를 학습하는 것으로 생각할 수 있다

<br/>

![Image](https://github.com/user-attachments/assets/777262a9-378d-49f0-91d2-62fcf5df9710)

위 정리에서 비지도 학습의 예제 중 '이미지 → 데이터 압축' 는 예를 들어 고해상도 이미지를 입력으로 받는다면, 이미지의 중요한 특징만 추출해 저차원 벡터로 변환하는 함수 𝑓 학습하는 것처럼 필요한 부분을 얻기 위해 데이터를 압축한다. 

<br/>

## ML from probability estimation perspective 


<br>

## 예시 

✔ 예시 (스팸 메일 분류)

입력(𝑋): 이메일 본문

출력(𝑌): "스팸" or "정상 메일"

지도 학습 모델은 다음과 같은 조건부 확률을 추정함: 𝑃(𝑌=spam∣𝑋)=0.8, 𝑃(𝑌=not spam∣𝑋)=0.2

즉, 이메일을 보고 스팸일 확률이 80%, 정상일 확률이 20%라고 예측하는 것

📌 정리: **지도 학습은 "입력이 주어졌을 때 가능한 출력을 예측하는 확률 모델"** 이라고 볼 수 있다



✔ 예시 (군집화 Clustering)

입력(𝑋): 고객 데이터 (연령, 소비 패턴 등)

출력 없음 ❌ (정답이 없음)

비지도 학습 모델은 다음을 추정함: P(X)=?("이 데이터가 얼마나 흔한가?")

데이터가 많이 몰려 있는 곳이 있다면 **"이런 유형의 고객이 많다"** 고 판단하여 같은 그룹(클러스터)으로 묶음.

📌 정리: **비지도 학습은 "입력 데이터의 분포를 분석해 패턴을 찾는 확률 모델"** 이라고 볼 수 있음.

<br/>

![Image](https://github.com/user-attachments/assets/5e8945a1-c4fe-469d-ada3-48c55e854321)

<br/>

## 인공지능 (인공지능(김영성 교수님) 수업 내용)

지능 : 지혜를 가지고 있는 사람의 능력 

인공지능 : 인간 수행 능력과 유사하거나, 합리적인 사고 및 지능적 행동을 보이는 시스템을 설계하는 과학

Narrow AI (좁은 AI): 특정 작업에 특화 (예: 얼굴 인식)

General AI (범용 AI): 인간 수준의 전반적인 사고 가능 (가설적)

(내 생각: General AI가 중요한 만큼 Narrow AI도 중요하다고 생각. Gerneral AI가 활용 범위도 넓고 성능도 좋지만, 매우 사소한 부분에서는 Narrow AI를 사용하는게 더 효율적이라고 생각.
따라서 Gerneral AI가 발전되는 만큼 Narrow AI도 같이 발전되어야 한다고 생각함)

<br/>


아직 인공지능이 사람을 잘 묘사하는지는 의문이다 -> 활용 못 하는 것도 많음

많은 곳에서 ai가 투입이 되고 있다

자율 주행 운전 방법 : 수많은 데이터를 학습하는 방식으로 개발하고 있음. 또한 센프란시스코에서 자율 주행 자동차가 많아지고 있다. -> ai 기술의 발전을 알려줌 

<br/>

## 핵심 영역(Core Areas)

Learning(학습): 경험을 바탕으로 적응 (예: 머신러닝)

→ AI는 데이터를 통해 배우고, 경험을 기반으로 성능을 향상한다.

Reasoning(추론): 논리적인 결정을 내림 (예: 전문가 시스템)

→ AI는 논리적으로 사고하여 문제를 해결한다.

Perception(지각): 환경에서 데이터를 해석 (예: 컴퓨터 비전)

→ AI는 주변 데이터를 분석하여 의미를 파악한다.

<br/>

다양한 분야에서의 활용(Applications Across Fields):

AI는 거의 모든 지적 작업에 적용될 수 있음

→ AI는 다양한 분야에서 활용되며, 인간이 수행하는 지적 작업을 보조하거나 자동화한다.

예시:

언어 번역 (예: 구글 번역)

→ AI를 활용하면 자동으로 언어를 변환할 수 있다.

실시간 음성 인식

→ AI는 사람의 말을 즉시 인식하고 텍스트로 변환할 수 있다.

<br/>

## AI 접근 방식 4가지

AI는 두 가지 기준(인간 vs. 합리성, 사고 vs. 행동)에 따라 네 가지 접근 방식으로 나뉜다.

1. 인간처럼 생각하는 시스템 → 인간의 사고 과정 모방 (예: 인지 과학, 신경망)

2. 인간처럼 행동하는 시스템 → 인간 행동을 흉내 내는 AI (예: 챗봇, 로봇, 튜링 테스트)

3. 합리적으로 생각하는 시스템 → 논리적 사고 기반 AI (예: 전문가 시스템)

4. 합리적으로 행동하는 시스템 → 최적의 행동을 수행하는 AI (예: 강화학습, 자율주행)

<br/>

## 두 가지 주요 관점

1. 인간 중심 접근(Human-like Intelligence): 심리학적 관점에서 인간의 사고 및 행동을 연구하여 AI 개발, **경험적 연구(관찰과 가설)에 기반**

2. 합리주의적 접근(Rationalist Approach): 수학과 공학(통계, 제어 이론, 경제학 등) 활용, **논리적이고 최적화된 의사결정을 목표로 함**













































