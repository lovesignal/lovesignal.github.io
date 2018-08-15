---
layout: post
date: 2018-04-13
title: Python & Django Day5
tags: [django, python]
categories: programming
comments: true
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>



## 함수(packing, unpacking), 재귀함수(예외처리)

### 함수(Function)

#### 추상화

 별도 공간에 존재하여, 변수간 간섭이 방해를 일으키지 않는 방법

#### 분리

 코드는 다른 곳에 작성되어, 우리가 필요한 경우 호출만 하여 사용할 수 있는 방법



```python
def func_name(arg):
    # code
    print("Hello, Func")
    return arg

func_name()
```



```python
def add(a, b):
    c = a + b
    return c

x = add(5, 5)
print(x)
```

<br><br>

### **parameter(매개변수), argument(인자) 란?**

#### parameter

함수 정의할때 어떤 값을 받겠다 라고 선언하고, 실행부에서 사용하는 변수를 의미

<br>

#### argument

함수를 호출할때 함수에게 넘기는 값들

```python
def func(parameter1, parameter2): # parameter1, parameter2는 parameter
    print(parameter1 + parameter2)
    return parameter1 + parameter2

func(3, 4) # 3, 4는 argument
```


 정리하면 "func이라는 함수를 호출할때 argument(인자)로 3과 4를 넘겼고,
func에서는 parameter(매개변수)에 3, 4를 받아서 실행되었다" 라고 정리될 수 있다.

<br>

### 연습

다음 연산을 담당하는 함수를 만들어서 순서대로 실행하기

1) 1~9까지 숫자를 하나 선택

2) 선택한 숫자에 2를 곱한다.

3) 5를 더한다.

4) 1769를 더한다.

5) 자신이 태어난 년도를 뺀다.

```python
def choice_number():
    number = input('1~9까지 숫자 중 정수 하나를 선택하세요.')
    return int(number)

def multi2(number):
    return number * 2

def add5(number):
    return number + 5

def add1769(number):
    return number + 1769

def sub_birth_year(number):
    return number - 1987

number = choice_number()
number = multi2(number)
number = add5(number)
number = sub_birth_year(add1769(number))
print(number)
```

<br>

### 함수2

#### default value

```python
def func_name(위치인자, 키워드인자):
```



```python
def range_list(start, end=None):
    if not end:
        return list(range(start))
    return list(range(start, end))

print(range_list(10))
# default 값은 항상 뒤만 가능하므로 start=0으로 지정하는 것 불가
```



```python
def range_list(start, end=None, step=None):
    if not end and not step:
        return list(range(start))
    elif not step:
        return list(range(start, end))
    return list(range(start, end, step))
```



```python
def test(a, b, c):
    print('a :', a)
    print('b :', b)
    print('c :', c)

test(b=1, c=2, 3) # Error : 위치인자 맨 앞에 들어가야 함
test(a=1, 2, c=3) # Error : 위치인자 에러
test(1, a=2, c=3) # Error : b=1로 인식되지 않음
test(1, b=2, c=3)
```

<br><br>



### packing, unpacking

#### packing

```python
def sum_all(a, b, c):
    return a + b + c

print(sum_all(1, 2, 3))


### packing
## EX1
def sum_all(*args):   # 위치인자 값이 tuple로 들어옴
    return sum(args)    

print(sum_all(1,2,3,4,5,6))

## EX2
def print_f_name(**kwargs): # 키워드인자 값이 dictionary로 packing 되어서 들어옴
    for key in kwargs:
        print(key, '의 이름은', kwargs[key])

print_f_name(faterh="임꺽정", mother="김말숙", cat="자두", bro="곰")
    
```

<br>

#### unpacking

```python
## EX1
def sum_all(*args):
    return sum(args)    

print(sum_all(*[1,2,3,4,5,6])) 
# list를 값으로 넣는 경우 앞에 *을 붙여주면 unpacking 된다


## EX2
family_dict = {
    "father": "임꺽정", 
    "mother": "김말숙", 
    "cat": "자두, 
    "bro": "곰"
}

def print_f_name(**kwargs): 
    for key in kwargs:
        print(key, '의 이름은', kwargs[key])

print_f_name(**family_dict)
```

<br>

#### 연습

##### 전연 변수 활용하기

1) 함수를 호출할 때마다 좋아하는 것을 묻고 입력 받아서 likes라는 변수에 리스트로 담기

2) 원하는 횟수만큼 호출하고 최종 결과물을 출력해보기

```python
def likesList():
    likes = []
    flag = True
    while flag:
        like = input("좋아하는 것을 입력하세요")
        if like == "종료":
            flag=False
            break
        likes.append(like)
    print(likes)

likesList()
```



<br><br>

### 함수가 변수를 참조하는 방법



<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/%ED%95%A8%EC%88%98.png" width="90%">



### Recursion Function 재귀함수

```python
# n! => n * (n-1) * (n-2) * ... * 1

def factorial(n):
    result = 1
    for i in range(1, n+1)
    
```



```python
# 정수 a와 n을 받아서 a에 n을 더하는 재귀함수 만들기
def add_n(a, n):
    if n == 0:
        return a
    return 1 + add_n(a, n-1)

print(add_n(10,7))
```

<br>

### 예외처리

```python
try:
    Error 발생할 우려가 있는 코드
except:
    Error 발생시 작동하는 코드
```



```python
num = input('숫자를 입력하세요.:')
num = int(num)
print(num + 2)


# 예외처리
try:
    num = input('숫자를 입력하세요.:')
    num = int(num)
    print(num + 2)
except:
    print("숫자를 아라비아 문자로 입력하세요.")

# 예외처리
def addingTwo():
    flag = True
    while flag:
        try:
            num = input("숫자를 입력하세요(종료를 원하면 종료를 입력하세요) :  ")
            if num == "종료":
                flag = False
                break
            num = int(num)
            print(num + 2)
        exceptValueError, ZeroDivisionError:
            print("아바리아 문자로 입력하세요 ")
            continue
```

* except 뒤에 반드시 **ValueError** 등 입력해 주어야 0 입력시 발생하는 에러가 따로 처리 됨.

  입력하지 않으면 대형 프로그램 작정시 에러가 제대로 출력되지 않는 문제가 발생.

  디버깅 어려워지게 됨. 예상되는 에러 모두 입력해주는 게 좋음.