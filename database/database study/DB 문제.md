## 두 개의 table 연결하기 

문제 : 2017 가을(fall), 또는 2017 봄(spring)에 열린 강의를 찾고, 해당 강의 이름을 추출해라

상황: 현재 연도와 계절은 section table에 저장되어 있지만, 강의 이름 속성이 존재하지 않음 

해결 방법 : course table에 course_id 속성과 section table의 course_id 속성을 조건문으로 결합한 뒤 course table로 넘어가서 강의명 추출 

```ruby
select c1.dept_name
from section as s1, course as c1
where s1.semester = 'fall' and s1.year ='2017' and s1.course_id = c1.course_id

union

select c1.dept_name
from section as s1, course as c1
where s1.semester = 'spring' and s1.year = '2018' and s1.course_id = c1.course_id;
```

<br/>

## 코드 설명 

위 코드에서 2017 가을(fall), 또는 2017 봄(spring)에 열린 강의를 찾기 위해 합집합(union) 사용 

이후, where 문을 이용해서 연도와 계절을 설정하고, 마지막 부분에 s1.course_id = c1.course_id를 추가 -> **해당 연도와 계절을 구한 table 의 course_id와 coures table course_id가 같으면 id를 가져온다는 의미** 

이렇게 되면, 최종적으로 얻는 table은 해당 연도 계절을 만족하는 course_id 테이블이 완성되고, **이것은 section table과 course table를 연결했다는 의미이다**

연결을 성공하면 마음대로 course table에서 원하는 정보를 select 할 수 있고, 결과적으로 course의 dept_name을 추출할 수 있게 됨 

