key: 20190224
title: "[MySQL: BASIC] 맨앞/맨끝 특정 문자가 있는/없는 값만 추출하기"
excerpt: "맨앞/맨끝 특정 문자가 있는/없는 값만 추출하기"
categories: programming
comments: true
tag : [sql, mysql]

---

## SQL 쿼리 예시

```mysql
-- 맨 끝에 특정 문자 오는 값만 추출
SELECT DISTINCT CITY FROM STATION 
WHERE RIGHT(CITY,1) IN ('a','i','e','o','u');

SELECT DISTINCT CITY FROM STATION 
WHERE CITY REGEXP '[aeiou]$'

-- 양쪽 끝에 특정 문자 오는 값만 추출
SELECT DISTINCT CITY FROM STATION
WHERE LEFT(CITY, 1) IN ('a', 'e', 'i', 'o', 'u') 
       AND RIGHT(CITY, 1) IN ('a', 'e', 'i', 'o', 'u');

SELECT DISTINCT CITY FROM STATION 
WHERE CITY RLIKE '^[aeiou].*[aeiou]$'

-- 특정 문자로 시작하지 않는 값만 추출
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP '^[^aeiou]';

-- 특정 문자로 끝나지 않는 값만 추출
SELECT DISTINCT CITY FROM STATION
WHERE CITY NOT REGEXP '[aeiou]$'
```



## Regular Expression

```sql
-- [] (Square bracket): 문자들의 모음
WHERE CITY REGEXP '[aeiou]'

-- $ (Dollar sign): 맨끝을 나타낸다. x$라고 하면 x로 끝나는 것을 표현한다. 
WHERE CITY REGEXP '[aeiou]$'
WHERE CITY NOT REGEXP '[aeiou]$'

-- ^ (Caret): $와는 반대로 맨앞을 나타낸다. ^x라고 하면 x로 시작하는 것을 표현한다.
WHERE CITY RLIKE '^[aeiou]'

-- [^] (Negative character set) : [] 안의 값을 제외한 것을 의미
WHERE CITY REGEXP '^[^aeiou]'

-- . (Dot): \n을 제외한 모든 문자
WHERE CITY RLIKE '^[aeiou].*[aeiou]$'

-- * (Multiply sign): 반복문자
WHERE CITY RLIKE '^[aeiou].*[aeiou]$'
```



