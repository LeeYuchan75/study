## Relational Data Model

Relation Data model : 데이터를 행(Row)과 열(Column)로 구성된 테이블의 형태로 표현하는 데이터 모델

![image](https://github.com/user-attachments/assets/58bc7aab-b348-49a4-b804-598adf2c2da8)

왼쪽에 있는 표를 오른쪽과 같이 relation model로 데이터베이스 구축 
 
<br/>

전체적인 표 : tabel 

튜플 (행): 열(column)에 해당하는 값들이 모여 정보를 나타내는 집합

속성 (열): 각 열이 의미하는 것 (ex: 이름,ID)

하나의 축에는 하나의 attribute가 들어가야 하고, 데이터의 순서는 상관 없음 

속성이 가질 수 있는 값을 domains of attribute 라고 함 

**relational database** : 위와 같은 테이블 집합

![image](https://github.com/user-attachments/assets/9336f838-34f6-49e7-bb7f-edc1b85b3472)

<br/>

## Database Schema and instance

1. 데이터베이스 스키마 (Schema) : 데이터베이스의 구조나 설계도. 테이블, 칼럼, 관계, 제약 조건 등이 포함됨

2. 데이터베이스 인스턴스 (Instance) : 데이터베이스의 실제 데이터 상태. 특정 시점에 데이터베이스가 어떻게 구성되어 있는지를 나타냄

<br/>

## The purpose of schema design

스키마 설계의 목적 : 데이터베이스와 각 관계를 설계하여 서로 다른 관계의 튜플들을 연결

<br/>

## Key

![image](https://github.com/user-attachments/assets/922f00ff-3e33-4c70-aafc-dcd88b1cb189)

1. Super Key: 모든 행을 유일하게 식별할 수 있는 속성(집합)

2. Candidate Key: 슈퍼키 중에서 최소성을 만족하는 키

3. Primary Key: 후보키 중에서 하나를 선택한 키

<br/>

## 스키마 다이어그램 (Schema Diagram)

Schema Diagram : 데이터베이스의 스키마(구조)를 그림으로 표현한 것

<br/>

## Relational Query Language

Relational Query Language : 관계형 데이터베이스에서 테이블을 조작하고 결과를 테이블 형태로 반환하는 언어

<br/>

## Relational Algebra

Relational Algebra : 관계형 데이터베이스에서 데이터를 조작하고 질의하는 형식적(query language) 연산 집합

1. σ (select) : 조건을 만족하는 행(튜플)만 선택, SQL의 WHERE 절과 유사

2. π (Project) : 특정 속성(컬럼)만 선택, SQL의 SELECT (컬럼 선택)과 유사

3. × (Cartesian Product) : 두 테이블의 모든 조합을 반환 (각 행을 서로 조합), SQL에서 CROSS JOIN과 유사

4. ⋈𝜃 (Theta Join) : 𝜃(조건) 을 만족하는 경우에만 조인

5. ⋈ (Natural Join) : 공통 속성이 자동으로 매칭되는 조인

6. ∪ (Union) : 두 테이블의 모든 행을 합침 (중복 제거), SQL의 UNION과 유사

7. − (Set Difference) : 첫 번째 테이블에 있는 데이터 중, 두 번째 테이블에는 없는 데이터만 반환, SQL의 EXCEPT 연산과 유사 

8.  ∧ (and), ∨(or), ㄱ (not)

<br/>

## Select Operation

selection predicate : σ 오른쪽 하단에 있는 부분으로 **조건을 의미**

괄호에 있는 부분은 table을 의미

![image](https://github.com/user-attachments/assets/f84a541f-85b2-49ed-a2b9-a6e26b8d95f1)

<br/>

## Project Opertaion

π 오른쪽 아래에 있는 속성만을 반환함 

![image](https://github.com/user-attachments/assets/7beb3ed7-1a39-4b47-80fe-69661a84a689)

<br/>

## Cartesian Product

문제점 : Cartesian Product는 모든 조합을 반환하므로 개발자가 원하고자 하는 데이터만 얻기 어려움 

-> Theta Join 또는 Natural Join으로 문제 해결 

<br/>

## Join Operation

![image](https://github.com/user-attachments/assets/33bebd0c-d328-4b5d-b512-5dfaec8cc636)

**Natural Join 과정**

![스크린샷 2025-04-03 123157](https://github.com/user-attachments/assets/81bd9d24-0c01-4092-9de8-1e786ffe3b69)

![스크린샷 2025-04-03 123208](https://github.com/user-attachments/assets/7952068b-f8bb-4c22-b5dc-3e27fb7ad311)

![스크린샷 2025-04-03 123214](https://github.com/user-attachments/assets/999fed00-d0b0-4eef-bfb1-c0d91461a6bf)

**Natural Join은 관계의 교집합(∩)과 같다**

<br/>

## union operation 



<br/>

## union operation 예시

![image](https://github.com/user-attachments/assets/22cdedca-0e9c-4c22-b93b-42e675900017)

![스크린샷 2025-04-03 162754](https://github.com/user-attachments/assets/b0fe632a-56b0-460a-a834-13e2aabd8697)

![스크린샷 2025-04-03 162911](https://github.com/user-attachments/assets/07907cc7-8572-4dac-9463-c18da142f186)

<br/>

## Set-Intersection Operation

**1. 두 table의 arity(열 개수)가 돟일해야한다**

**2. 속성들의 domain이 일치해야 한다**

union 속성과 동일 

<br/>

## 예시 

![스크린샷 2025-04-03 163837](https://github.com/user-attachments/assets/d3dbfa09-6c3b-495a-8525-aaf100fa8510)



















































































































