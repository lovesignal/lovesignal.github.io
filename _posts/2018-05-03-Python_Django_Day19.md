---
layout: post
title: Python & Django Day19 프레임워크
tags: [django, python]
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>



## 프레임워크, 라이브러리

### 차이점

#### 라이브러리

필요한 기능들이 구현되어 있는 라이브러리에서 기능을 불러와서 사용하는 것이다.

직접 작성했기 때문에 프로그램 흐름의 전체를 이해하기 쉽다.



<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_library.png" width="80%">



(예시)

```python
import requests
response = requests.get("https://www.fastcampus.co.kr")
response.text
```

<br>

#### 프레임워크

이미 구성되어진 틀.

프레임워크 자체가 하나의 프로그램이다. 그러므로 실행 흐름이 결정되어 있고 필요한 기능들이 채워져 있다. 그러므로 라이브러리처럼 가져다 쓰는 것이 아니라 내가 필요한 기능으로 대체해서 사용하는 것이다.

실행 흐름이 이미 정해져 있기 때문에 어떤 방식과 흐름으로 코드가 실행되는지 파악하기 어렵다.



<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_framework.png" width="80%">

<br>

#### 프레임워크 허들

1. 정해진 약속대로 사용해야 한다.
2. 흐름을 이해하기 어렵다.



<br><br>

## 수업 순서

1. 간단한 계산기 프레임워크를 사용
2. 계산기 프레임워크를 만들기



<br><br>

## 계산기 프레임워크

디렉토리 구조

* main.py			# 프레임워크 코드 파일

  * models

    ______init______.py

    number.py		# 숫자 포맷

    operators.py		# 연산자 등록하는 곳

<br>

#### main.py

```python
import operator as op

try:
    from models import operators
except ImportError:
    operators = None

try:
    from models import Number
except ImportError:
    Number = None

default_operators = {
    '+': op.add,
    '-': op.sub,
    '*': op.mul,
    '/': op.truediv
}

operators = operators if operators else default_operators
num_format = Number if Number else float

def select_operator():
    print("계산한 연산을 선택해주세요.")
    for i, op in enumerate(operators):
        print("{simbol} 연산".format(
            simbol=op,
        ))
    try:
        op = operators[input('연산자 입력 : ')]
    except KeyError:
        print("연산자를 바르게 입력해주세요")
        return select_operator()
    return op


def select_number(n):
    print("계산할 {n}번째 숫자를 선택해주세요.".format(n=n))
    number = num_format(input('숫자입력 : '))
    return number


if __name__=='__main__':
    print("지정 표현 맞춤형 계산기 프로그램 작동!")
    while True:
        print("종료는 Ctrl + c")
        try:
            op = select_operator()
            num1 = select_number(1)
            num2 = select_number(2)
        except KeyboardInterrupt:
            break
        print('연산 결과는 {}입니다. '.format(op(num1, num2)))
```

<br>

#### ______init______.py

```python
# __init__.py 를 폴더에 만들어야 모듈 인식할 수 있다.

from .operators import operators    # operators라는 dictionary 등록
from .number import Number
```



<br>

#### number.py

```python
class Number(float):
    num1 = {
        0: '',
        1: '일',
        2: '이',
        3: '삼',
        4: '사',
        5: '오',
        6: '육',
        7: '팔',
        9: '구'
    }

    num2 = ['', '십', '백', '천', '만']

    def __repr__(self):
        str_num = str(self.real)
        temp = str_num.split('.')
        str_num = temp[0]
        floating_value = '' if temp[1] == '0' else '.' + temp[1]

        if len(str_num) > 5:
            retrun str_num
        
        result = ''
        for i, n in enumerate(str_num):
            result += ( self.num1[int(n)] + self.num2[len(str_num) -i -1] if self.num1[int(n)] else '')
        
        if not result:
            result = '영' + floating_value
        return result + floating_value
    
    def __str__(self):
        return self.__repr__()

    def __add__(self, other):
        return Number(self.real + other.real)

    def __sub__(self, other):
        return Number(self.real - other.real)

    def __mul__(self, other):
        return Number(self.real * other.real)

    def __truediv__(self, other):
        return Number(self.real / other.real)
```



<br>

#### operators.py

```python
# 연산자 등록

import operator

def sharp(x, y):
    return x + y + 100

def custom_sub(x, y):
    return x - y + (y + x)

operators = {
    "+" : operator.add,      # operator.add(3, 4) : 3 + 4 실행
    "-" : operator.sub,
    "*" : operator.mul,
    "/" : operator.truediv,
    "#" : sharp,
    "@" : custom_sub
    
}
```