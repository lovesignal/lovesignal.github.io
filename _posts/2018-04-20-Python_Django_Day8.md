---
layout: post
date: 2018-04-20
title: Python & Django Day8 lambda, map, filter, 데코레이터
tags: [django, python]
categories: programming
comments: true
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## lambda

함수만 만들고 함수가 들어갈 변수를 지정하지 않는 식.

(깔끔하다는 장점은 있으나 가독성이 떨어질 수 있어서 python3 부터는 권장하지 않는 추세이다.)

```python
students = []
student1_info = {
    "first_name": "sol",
    "las_name" : "hyun",
    "student_no": 3498

}

student2_info = {
    "first_name": "suzy",
    "las_name" : "bae",
    "student_no": 1345

}

student3_info = {
    "first_name": "coca",
    "las_name" : "hyun",
    "student_no": 4728

}

for i in range(1, 4):
    students.append(eval('student%d_info'% (i)))
```

<br>

student_no를 기준으로 정렬해주려고 한다. 정렬해주는 함수를 한 번만 사용할 것이기 때문에 함수를 만들어서 변수에 저장하는 것은 비효율적이다. 이때 람다식을 이용하면 간결하게 해결할 수 있다.

```python
# lambda식 이용하기 전
def sort_help(d):
    return d['student_no']

sorted_student = sorted(students, key = sort_help)


# lambda식 이용해서 수정
sorted_student = sorted(students, key = lambda x: x['student_no'])
print(sorted_student)
```

<br>

### lambda식 연습

```python
# +1 해주는 함수
lambda x : x + 1

# 3개의 값을 더해주는 함수
lambda x, y, z : x + y + z

# 2개의 값을 각각 제곱해서 더해주는 함수
lambda x, y : x**2 + y**2
```

```python
### lambda 함수 만들기
## 1개의 숫자를 받아서 2의 배수이면 True, 아니면 False 리턴하는 함수
# 함수 정의
def multiples_of_two(n):
    if n%2 == 0:
        return True
    else:
        return False

# lambda식 이용
lambda x: True if x%2 == 0 else False

## 0~n개의 정수를 받아서 다 합쳐주는 함수
def f(*x) : return sum(x)
lambda *x : sum(x)
```



<br><br>

## map

어떤 함수를 각각의 리스트에 적용 시키는 것.

```python
### map
# for문 이용
a = list(range(1, 11))

result  = []
for el in a :
    result.append(el + 1)

# map 이용
a = list(range(1, 11))

result = map(lambda x : x + 1, a)
list(result)
```

<br>

### map 연습

```python
# 1) 1~100이 담긴 리스트를 fizzbuzz하기 (3의 배수이면 fizz, 5의 배수이면 buzz, 15의 배수이면 fizzbuzz)
raw_list = list(range(1, 100+1))

result = map(lambda x : 'fizzbuzz' if x%15 == 0 else
('buzz' if x%5 == 0 else ('fizz' if x%3 == 0 else x)), raw_list)

print(list(result))
```



<br><br>

## filter

어떤 함수를 각각의 리스트에 적용 시키는 것은 map과 동일하고, return값이 boolean값으로 나온다.

```python
a = list(range(1, 10+1))
result = []
for el in a :
    if el % 2 == 0:
        result.append(el)

# filter 사용
list(filter(lambda x : x % 2 == 0, a))
```

<br>

### filter 연습

```python
# 1~100까지 가진 리스트에서 50보다 큰 값만 남겨보기
raw_list = list(range(1, 100+1))
result = filter(lambda x : x > 50, raw_list)

# 위 결과값을 받아 2의 배수만 가진 리스트 만들기
result = filter(lambda x : x % 2 == 0, result)
print(list(result))
```

<br><br>



## reduce

``````python
from functools import reduce

a = [1, 2, 3, 4]

result = reduce(lambda x, y: x + y, a)
print(result)
``````

<br>

* 코드 실행 과정 :

```python
a = [1, 2, 3, 4]에서 x, y에 1,2 받아서 더해 준다.
a = [3, 3, 4]가 된다.

다시 x, y에 3, 3을 받아서 더해준다.
a = [6, 4] 가 된다.

다시 x, y에 6, 4를 받아서 더해준다.
result는 최종 10이 된다.
```

<br>

* 연습

1 ~ 10까지 가진 리스트에서 각 요소의 제곱을 더하기.

```python
a = list(range(1, 10+1))
from functools import reduece
redeuce(lambda x, y: x**2 + y**2, a)
```

<br>

#### 함수를 인자로 보내는 예시 : 함수를 변수처럼 사용하기

```python
# 함수를 인자로 받아서 변수처럼 사용하기
def print_start_end(func):
    print("함수가 시작됩니다.")
    result = func()
    print("함수가 끝났습니다.")
    return result

def print_1_to_100():
    for i in range(1, 100+1):
        if i < 100:
            print(i, end=', ')
        else:
            print(i)

print_start_end(print_1_to_100)

#----------- 결과 -------------
함수가 시작됩니다.
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100
함수가 끝났습니다.
#-----------------------------


# 함수를 받아서 함수 생성
def make_print_start_end(func):
    def new_func():
        print("함수가 시작됩니다.")
        result = func()
        print("함수가 끝났습니다.")
        return result
    return new_func

new_func = make_print_start_end(print_1_to_100)

#------------------------------------------------------------

def make_print_start_end(func):
    def new_func(n):
        print("함수가 시작됩니다.")
        result = func(n)
        print("함수가 끝났습니다.")
        return result
    return new_func

def print_1_to_n(n):
    for i in range(1, n+1):
        if i < n:
            print(i, end=', ')
        else:
            print(i)

new_func = make_print_start_end(print_1_to_n)
new_func(100)

#----------- 결과 -------------
함수가 시작됩니다.
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100
함수가 끝났습니다.
#----------------------------- 
```

```python
# 인자가 여러개
def make_print_start_end(func):
    def new_func(*args, **kwargs):    # 하나의 튜플과 딕셔너리로 packing
        print("함수가 시작됩니다.")
        result = func(*args, **kwargs)    # unpacking
        print("함수가 끝났습니다.")
        return result
    return new_func


def print_a_to_b(a, b, c):
    for i in range(a, b+1, c):
        if i < b:
            print(i, end=', ')
        else:
            print(i)

new_func = make_print_start_end(print_a_to_b)
new_func(1, 100, 2)


def sum_a_to_b(a, b):
    result = 0
    for i in range(a, b+1):
        result += i
    return result

new_func2 = make_print_start_end(sum_a_to_b)
print(new_func2(1, 10))
```



<br><br>

## Decorator

함수를 꾸미는 기능.

```python
### 함수를 꾸미자, Decorator
def make_print_start_end(func):
    def new_func(*args, **kwargs):    
        print("함수가 시작됩니다.")
        result = func(*args, **kwargs)    
        print("함수가 끝났습니다.")
        return result
    return new_func

@make_print_start_end
def print_a_to_b(a, b, c):
    for i in range(a, b+1, c):
        if i < b:
            print(i, end=', ')
        else:
            print(i)

print_a_to_b(1, 100, 3)
```

<br>

함수를 만드는 함수를 호출 받아서, 넣고, 다시 결괏값으로 나온 함수를 리턴 받아서 실행시키는 구간(`new_func = make_print_start_end(print_a_to_b)`  `new_func(1, 100, 2)` ) 을  `@make_print_start_end`

으로 대체한다. 

(참고 : https://jonnung.github.io/python/2015/08/17/python-decorator/)

<br>

* 연습

  1) 다음 모듈의 기능을 이용하여 함수의 실행시간을 측정하는 데코레이터 만들기

  `from time import time`

  `start_time = time()`

  `end_time = time()`

  `executed_time = end_time - start_time`

```python
from time import time
start_time = time()
end_time = time()

def check_time(func):
    def new_func(*args, **kwargs):
        start_time = time()
        result = func(*args, **kwargs)
        end_time = time()
        print("함수 실행에 걸린 시간은 ", end_time - start_time)
        return result
    return new_func

@check_time
def sum_1_to_n(n):
    result = 0
    for i in range(1, n+1):
        result += i
    return result

result = sum_1_to_n(12345)
print(result)

#-----결과-------
함수 실행에 걸린 시간은  0.001059055328369140676205685


@check_time
def gauss_sum(n):
    return (n * (n + 1))/2

gauss_sum(12345)
#----결과------
함수 실행에 걸린 시간은  6.9141387939453125e-06
```



