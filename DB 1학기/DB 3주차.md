## DataBase 실습 및 문법

```ruby
create database university;
use university;

create table classroom
	(building		varchar(15),
	 room_number		varchar(7),
	 capacity		numeric(4,0),	
	 primary key (building, room_number)
	);

create table department
	(dept_name		varchar(20), 
	 building		varchar(15), 
	 budget		        numeric(12,2) check (budget > 0),
	 primary key (dept_name)
	);

create table course
	(course_id		varchar(8), 
	 title			varchar(50), 
	 dept_name		varchar(20),
	 credits		numeric(2,0) check (credits > 0),
	 primary key (course_id),
	 foreign key (dept_name) references department (dept_name)
		on delete set null
	);

create table instructor
	(ID			varchar(5), 
	 name			varchar(20) not null, 
	 dept_name		varchar(20), 
	 salary			numeric(8,2) check (salary > 29000),
	 primary key (ID),
	 foreign key (dept_name) references department (dept_name)
		on delete set null
	);

create table section
	(course_id		varchar(8), 
         sec_id			varchar(8),
	 semester		varchar(6)
		check (semester in ('Fall', 'Winter', 'Spring', 'Summer')), 
	 year			numeric(4,0) check (year > 1701 and year < 2100), 
	 building		varchar(15),
	 room_number		varchar(7),
	 time_slot_id		varchar(4),
	 primary key (course_id, sec_id, semester, year),
	 foreign key (course_id) references course (course_id)
		on delete cascade,
	 foreign key (building, room_number) references classroom (building, room_number)
		on delete set null
	);

create table teaches
	(ID			varchar(5), 
	 course_id		varchar(8),
	 sec_id			varchar(8), 
	 semester		varchar(6),
	 year			numeric(4,0),
	 primary key (ID, course_id, sec_id, semester, year),
	 foreign key (course_id, sec_id, semester, year) references section (course_id, sec_id, semester, year)
		on delete cascade,
	 foreign key (ID) references instructor (ID)
		on delete cascade
	);

create table student
	(ID			varchar(5), 
	 name			varchar(20) not null, 
	 dept_name		varchar(20), 
	 tot_cred		numeric(3,0) check (tot_cred >= 0),
	 primary key (ID),
	 foreign key (dept_name) references department (dept_name)
		on delete set null
	);

create table takes
	(ID			varchar(5), 
	 course_id		varchar(8),
	 sec_id			varchar(8), 
	 semester		varchar(6),
	 year			numeric(4,0),
	 grade		        varchar(2),
	 primary key (ID, course_id, sec_id, semester, year),
	 foreign key (course_id, sec_id, semester, year) references section (course_id, sec_id, semester, year)
		on delete cascade,
	 foreign key (ID) references student (ID)
		on delete cascade
	);

create table advisor
	(s_ID			varchar(5),
	 i_ID			varchar(5),
	 primary key (s_ID),
	 foreign key (i_ID) references instructor (ID)
		on delete set null,
	 foreign key (s_ID) references student (ID)
		on delete cascade
	);

create table time_slot
	(time_slot_id		varchar(4),
	 day			varchar(1),
	 start_hr		numeric(2) check (start_hr >= 0 and start_hr < 24),
	 start_min		numeric(2) check (start_min >= 0 and start_min < 60),
	 end_hr			numeric(2) check (end_hr >= 0 and end_hr < 24),
	 end_min		numeric(2) check (end_min >= 0 and end_min < 60),
	 primary key (time_slot_id, day, start_hr, start_min)
	);

create table prereq
	(course_id		varchar(8), 
	 prereq_id		varchar(8),
	 primary key (course_id, prereq_id),
	 foreign key (course_id) references course (course_id)
		on delete cascade,
	 foreign key (prereq_id) references course (course_id)
	);

show databases; 
```

<br/>

## 설명 

1. create database university : university라는 이름의 새 데이터베이스를 생성한다.

2. use university : 현재 사용할 데이터베이스를 university로 설정한다.

3. create table <table_name> (...) : 새 테이블을 생성하며, 테이블 이름과 컬럼을 정의한다.

4. varchar(n) : 가변 길이 문자열 데이터 타입을 정의하며, 여기서 n은 최대 길이를 나타낸다. 예: varchar(15)는 최대 15자까지의 문자열을 저장할 수 있다.

5. numeric(p, s) : 고정 소수점 숫자 데이터 타입을 정의하며, p는 전체 자릿수(precision), s는 소수점 이하 자릿수(scale)를 나타낸다. (예: numeric(4,0)은 최대 4자리 정수를 저장할 수 있다.)

6. primary key (column_name, ...) : 지정된 컬럼을 기본 키로 설정하여 각 행이 고유함을 보장한다. 여러 컬럼을 기본 키로 사용할 수도 있다.

7. foreign key (column_name, ...) references <table_name> (column_name, ...) : 외래 키를 설정하여 다른 테이블과의 관계를 만든다. 지정된 컬럼이 다른 테이블의 기본 키나 고유 키를 참조하는 외래 키가 된다. 예: foreign key (dept_name) references department (dept_name)는 dept_name 컬럼이 department 테이블의 dept_name을 참조하는 외래 키로 설정됨을 의미한다.

8. on delete cascade : 부모 테이블의 데이터가 삭제될 때, 해당 데이터를 참조하는 자식 테이블의 데이터도 자동으로 삭제된다. 예: foreign key (course_id) references section (course_id) on delete cascade는 section 테이블에서 course_id가 삭제될 때, 이 외래 키를 참조하는 teaches 테이블의 관련 데이터도 삭제된다는 의미이다.

9. on delete set null : 부모 테이블의 데이터가 삭제될 때, 자식 테이블에서 해당 외래 키 컬럼의 값이 NULL로 설정된다. 예: foreign key (dept_name) references department (dept_name) on delete set null은 department 테이블의 dept_name이 삭제될 때, 이를 참조하는 instructor 또는 student 테이블의 dept_name 컬럼 값이 NULL로 설정된다는 의미이다.

10. check (condition) : 컬럼에 대해 특정 조건을 설정하며, 조건을 만족하지 않으면 해당 값을 삽입할 수 없다. 예: check (budget > 0)은 budget 컬럼에 0보다 큰 값만 저장할 수 있음을 의미한다.

11. show databases : 현재 MySQL 서버에서 존재하는 데이터베이스 목록을 표시한다.

12. unique : 고유한 값을 요구하는 제약 조건으로, 중복된 값이 삽입되지 않도록 한다. 예를 들어, primary key는 자동으로 고유 제약을 가진다.

<br/>

## Primary key 예시 

**1. 단일 컬럼을 기본 키로 설정**

```ruby
create table student (
    ID varchar(5),          -- 학생의 ID
    name varchar(20) not null,  -- 학생의 이름
    dept_name varchar(20),  -- 학생의 소속 학과
    tot_cred numeric(3,0) check (tot_cred >= 0),  -- 학생의 총 학점
    primary key (ID)       -- ID 컬럼을 기본 키로 설정
);
```

이 예시에서 student 테이블은 각 학생의 ID 컬럼을 기본 키로 설정합니다. 즉, ID는 고유해야 하고, 중복되는 값은 삽입될 수 없음

<br/>

**2. 복합 기본 키(여러 컬럼을 기본 키로 설정)**

```ruby
create table enrollment (
    student_id varchar(5),  -- 학생 ID
    course_id varchar(8),   -- 수강 과목 ID
    semester varchar(6),    -- 학기 (예: 'Fall', 'Spring' 등)
    year numeric(4,0),      -- 연도
    grade varchar(2),       -- 성적
    primary key (student_id, course_id, semester, year)  -- 학생, 과목, 학기, 연도를 복합 기본 키로 설정
);
```
enrollment 테이블에서 student_id, course_id, semester, year 네 개의 컬럼을 복합 기본 키로 설정함

즉, 모든 열이 같아야 중복으로 허용(3개의 attribute가 동일하더라도 1개의 attribute가 다르면 중복이 아님)

<br/>

## Basic Query Structure

**SELECT** : 반환할 열(속성)을 지정함 (예: SELECT name, age 는 name과 age 열만 반환)

**FROM** : 데이터를 조회할 테이블(관계)을 지정함 (예: FROM students, courses 는 students와 courses 테이블에서 데이터를 가져옴)

**WHERE** : 조건을 지정하여 반환할 행을 필터링 (예: WHERE age > 18 는 age가 18보다 큰 행만 반환)

<br/>

## literal and from

literal : SQL에서 고정된 값(문자열, 숫자 등)을 의미. (ex: 'A', 100, 또는 '2025-03-29')

```ruby
SELECT 'A'
FROM country;
```

SELECT 'A': 'A'는 리터럴임. 여기서 SQL은 특정 테이블이나 열에서 데이터를 가져오지 않고, 단순히 고정된 문자열 'A'를 반환하도록 요청함

FROM country: FROM 절에 명시된 테이블(country)이 존재하기 때문에, 이 테이블의 튜플(행) 수만큼 리터럴 값 'A'가 반복됨

**즉, where을 통한 조건이 없으면 from의 테이블의 행의 수 만큼 literal를 반복한다는 의미**

<br/>

## 중복 제거 : distinct 

기본적으로 SQL 쿼리에서는 중복된 값도 결과로 반환함. 만약 테이블에 같은 값이 여러 번 존재하면, 해당 값은 쿼리 결과에 중복으로 표현

```ruby
SELECT DISTINCT dept_name
FROM instructor;
```

중복된 값을 제거하려면 SELECT 뒤에 DISTINCT 키워드를 사용해야함

만약 코드가 아래와 같이 distinct를 쓰고 열이 2개 이상이면, 해당 열이 모두 동일해야 중복으로 인정한다 

```ruby
SELECT DISTINCT dept_name,salary
FROM instructor;
```

즉, dept_name과 salary가 둘 다 같은 튜플이 2개 이상일 때 중복이 발생한다

<br/>

중복값은 기본적으로 허용하지만, 명시적으로 표현하고 싶으면 all 키워드를 사용 

```ruby
SELECT ALL dept_name
FROM instructor;
```

<br/>

## The select Clause

## select* 

select* : 모든 속성 선택을 의미함 

```ruby
SELECT *
FROM country;
```
이 쿼리는 country 테이블의 모든 열을 선택하여 반환함 

또한 아래와 같이 사용할 수도 있음 

```ruby
select  instructor.*
from  instructor, teaches
where instructor.ID = teaches.ID;
```

<br/>

## as 

as : 열 이름을 새롭게 지정 

**as의 중요한 점은, as 사용 전의 이름은 더이상 사용하면 안된다는 것이다** 

```ruby
SELECT name AS Student_Name, age AS Student_Age  ▷ as 사용 후 'Student_Name' 만 사용 가능, 'name' 사용 불가, age도 동일한 이유로 사용 불가 
FROM students;
```

위 예시 코드를 보면 students 테이블에서 name이라는 값의 열 이름을 Student_Name로 하고, age라는 값의 열 이름을 Student_Age 라고 지정함

추가적으로 아래 예시와 같이 table을 다른 이름으로 나눠서 사용할 수 있음 

<br/>

```ruby
SELECT DISTINCT C1.name
FROM country AS C1, country AS C2
WHERE C1.population > C2.population AND C2.continent = 'Asia';
```
<br/>

만약 아래 코드와 같이 table이 하나만 올 때는 DBMS 입장에서 name이 당연히 instructor table에서 올 것이라고 생각해 모호하지 않아서 사용해도 됨

하지만 table이 여러개일 때, select문에 어떤 table에서 왔는지 표시도 없이 name만 사용하면 DBMS 입장에서는 모호하기 때문에 오류가 생긴다 

```ruby
select name 
from instructor as t
order by name;
```

<br/>


```ruby
SELECT 5 * 10 AS Multiplication
from test;
```

다른 예시로 5*10의 값, 또는 문자열 (ex: '487') 같은 데이터도 가능함 

<br/>

또한, SELECT 절에 산술 연산자(+, -, *, /)와 함수(예: FLOOR, ROUND 등)를 사용할 수 있다 

```ruby
SELECT name, FLOOR(Population / 1000) AS Pop10k
FROM country;
```

FLOOR(x) : 소수점 이하를 버리고 정수만 반환

<br/>

## 조건문 

예시 코드 1

```ruby
SELECT name  
FROM country  
WHERE (continent = 'Asia' AND Population >= 50000000) 
      OR (continent = 'Europe' AND Population < 1000000)
      AND NOT (name = 'Monaco');
```

<br/>

예시 코드 2

```ruby
SELECT ID, name, salary 
FROM instructor
WHERE salary >= 80000
  AND LENGTH(name) BETWEEN 4 AND 6;
```

LENGTH(x) : x의 길이 추출 

BETWEEN A AND B : 범위 표현 

<br/>

## string operation

## upper() and lower()

대소문자 변환하는 연산 

```ruby
SELECT * FROM instructor 
WHERE UPPER(name) = 'ALICE';
```

<br/>

## 예시 문제 

![image](https://github.com/user-attachments/assets/3376fd41-f97f-4408-aee0-4036f690c2bb)

**정답 코드**

```ruby
SELECT *
FROM instructor, teaches;
```

<br/>

## self join 심화 

![image](https://github.com/user-attachments/assets/44a4aa1e-f099-4952-b77f-895d01a82e04)

우선, from에서 table이 2개가 오면, 이것은 카르테시안 곱이다 

따라서 내부적으로 오른쪽 표와 같이 생성이 된다

왼쪽 하단 코드는 다음을 의미한다 

- T.person = 'Bob' → T 테이블에서 Bob을 찾고

- T.supervisor = S.person → T의 상사(Alice)가 S 테이블의 직원(Alice)과 같을 때 (표를 보고 판단)

- S.supervisor는 Alice의 상사인 David가 된다 (오른쪽에서 조건을 만족하는 행의 S.superviser를 가져옴)












































