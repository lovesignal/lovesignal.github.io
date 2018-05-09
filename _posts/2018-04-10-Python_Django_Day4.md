---
layout: post
title: Python & Django Day4
tags: [django, python]
---

  Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## 데이터 구조(Dictionary, set), tuple(list comprehension)

### Tuple

immutable + 순서가 있는 자료형

(1, 2, 3, 4)

```python
tuple1 =(1, 2, 3, 4)
```

<br>

#### 튜플을 리스트로 바꾸기 :

1) 1 ~ 100까지 숫자를 포함하는 Tuple을 만드세요.

2) 그 Tuple을 list로 바꾸세요.

```python
tuple_1_to_100 = tuple(range(1, 101))
list_1_to_100 = list(tuple_1_to_100)
```

<br><br>

### Dictionary

key, value형태의 자료형 / 순서가 보장되지 않음

{‘key1’: ‘value1’, ‘key2’: ‘value2’}

```python
 d = {}
 d['name'] = 'sol'
# {'name': 'sol'}
```

<br>

#### Dictionary 만들기

1) 내 정보를(이름, 나이, 연락처) dictionary로 만들어보세요.


2) 이메일 정보를 추가하세요.

3) 각 정보를 대괄호와, .get메소드를 이용하여서 출력해보세요.

```python
info = {'name' : 'Jane', 'age':30, 'phone':'010-123-1234'}
info['email'] = 'email@abc.com'
info['email']
info.get('name')
```

* get을 쓰면 값이 없는 경우도 에러가 나지 않고, none을 출력하게 된다.

<br>


#### Tuple을 Dictionary로 바꾸기

```python
myInfo = [('name', 'Jane'), ('age', 30), ('phone', '010-123-1234')]

# 방법1
myInfoDic = {}

for el in myInfo:
    myInfoDic[el[0]] = el[1]

# 방법2
dict(myInfo)
```



<br><br>

### CSV (comma-separated values)

#### csv를 dictionary 형태로 바꾸기 ********

```python
csv_values = """
이름, 연락처, 나이, 이메일
철수, 010-1234-1234, 23, ch@ab.com
영희, 010-2485-4728, 39, yh@ac.com
"""

csv_values = csv_values.strip('\n')  
# strip(): 양 끝에 괄호 안의 값이 있으면 모두 삭제해주는 메서드

# string = "-----e---e---e-e--e---"
# print(string.strip('-'))
# e---e---e-e--e


csv_list = csv_values.split('\n')    # enter를 기준으로 값 나누어서 리스트 만듦
print(csv_list)

# ['이름, 연락처, 나이, 이메일', '철수, 010-1234-1234, 23, ch@ab.com', '영희, 010-2485-4728, 39, yh@ac.com']

info = {}
for el in csv_list:
    print(el.split(','))   # list로 뽑아 냄

    # ['이름', ' 연락처', ' 나이', ' 이메일']
    # ['철수', ' 010-1234-1234', ' 23', ' ch@ab.com']
    # ['영희', ' 010-2485-4728', ' 39', ' yh@ac.com']

#-------------------------------------------------
keys = []
for el in csv_list[0].split(','):
    keys.append(el.strip(' '))

print(keys)    # ['이름', '연락처', '나이', '이메일']

#-------------------------------------------------
results = []
for val in csv_list[1:]:
    result_dict = {}
    i = 0
    for el in val.split(','):
        result_dict[keys[i]] = el.strip(' ')
        i += 1
    results.append(result_dict)

# [{'이메일': 'ch@ab.com', '이름': '철수', '나이': '23', '연락처': '010-1234-1234'}, {'이메일': 'yh@ac.com', '이름': '영희', '나이': '39', '연락처': '010-2485-4728'}]

```

<br>

### Set 

```python
# 빈 set 만들기
set1 = set()

# set에 값 추가하기
set1.add(3)
set1.add(4)

# 합집합
set1.union(set2)

# set1만 갖고 있는 원소
set1.difference(set2)
```

<br>

```python
# set1 변수에 1 ~ 100까지 숫자 중 3, 5, 15의 배수

set1, set2, set3 = set(), set(), set() 

for i in range(1, 101):
    if i % 15 == 0:
        set3.add(i)
    elif i % 5 == 0:
        set2.add(i)
    elif i % 3 == 0:
        set1.add(i)

print("3의 배수 : ", set1)
print("5의 배수 : ", set2)
print("15의 배수 : ", set3)


# 3의 배수 :  {3, 6, 9, 12, 18, 21, 24, 27, 33, 36, 39, 42, 48, 51, 54, 57, 63, 66, 69, 72, 78, 81, 84, 87, 93, 96, 99}
# 5의 배수 :  {65, 35, 100, 5, 70, 40, 10, 80, 50, 20, 85, 55, 25, 95}
# 15의 배수 :  {75, 45, 15, 90, 60, 30}


# 두 set1, set2에서 겹치는 숫자를 출력
print(set1.union(set2))
    # {65, 66, 3, 69, 6, 5, 72, 9, 70, 10, 12, 78, 80, 81, 18, 84, 21, 20, 87, 24, 85, 25, 27, 93, 95, 96, 33, 99, 36, 35, 100, 39, 40, 42, 48, 50, 51, 54, 55, 57, 63}


# set3에서 set1에 포함되지 않은 숫자를 출력
print(set3.difference(set1))
    # {75, 45, 15, 90, 60, 30}
```

<br><br>







## Comprehensions

### List Comprehension

### for

```python
a = [i for i in range(1, 101)]
a = [i**2 for i in range(1, 101)]
```

<br>

### if

```python
a = [ i for i in range(1, 101) if i % 2 ==0]
```

<br>

#### [ [1, 2], [1, 2] ] 만들기

```python
#result = []
#for i in range(1, 3):
#    el = []
#    for j in range(1, 3):
#        el.append(j)
#    result.append(el)
    

result = [[x for x in range(1, 3)] for _ in range(2)]
# 인덱스 사용 안하고 횟수만 사용했을 때 _로 표기함
```

