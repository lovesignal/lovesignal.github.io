---
date: 2018-03-26
title: "[Python] Python Class note"
excerpt: "Inflearn에 있는 <프로그래밍, 데이터 과학을 위한 파이썬 입문> 강의를 듣고 정리한 강의노트 일부(계속 업로드 중...)"
categories: programming
comments: true
---



> Inflearn의 <프로그래밍, 데이터 과학을 위한 파이썬 입문> 강의를 정리한 강의노트 일부.
>
> 강의는 https://www.inflearn.com/course/python-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%9E%85%EB%AC%B8-%EA%B0%95%EC%A2%8C/ 에서 수강 가능.



# Chapter 5. Function

## Function Concept 1

### Function 함수

어떤 일을 수행하는 코드 덩어리

- 반복적인 수행을 회만 작성 후 호출


- 코드를 논리적인 단위로 분리


- 캡슐화 : 인터페이스만 알면 타인의 코드 사용 

<br>

### 함수 선언 문법

#### 함수 이름, parameter, return value(optional)

```python
def calculate_rectangle_area(x, y):
  return x * y

rectangle_x = 10
rectangle_y = 20
print("사각형 x의 길이: ", rectangle_x)
print("사각형 y의 길이: ", rectangle_y)

# 넓이를 구하는 함수 호출
print("사각형의 넓이: ", calculate_rectangle_area(rectangle_x, rectangle_y))
```

<br>

### Parameter vs. Argument

#### Prarmeter : 함수의 입력 값 인터페이스

```python
def f(x):
  return 2 * x + 7
```

#### Argument : Parameter에 실제 대입되는 값

```python
print(f(2))
```

<br>

### 함수 형태

Parameter 유무, return value 유무에 따라 함수의 형태가 다름

```python
def aRectangleArea():       # 인자 x, 리턴 값 x
  print(5 * 7)
```

35 출력 후 함수는 none이 됨

print(aRectangleArea()) 하면 none 출력

(예)

list_test = [5,4,3,2,1]

print(list_test.sort())

None 출력 됨. 왜냐하면 sort()는 return값이 없는 함수이므로.

<br>

* sort(), sorted() 차이

list_test.sort()는 반환 값이 없고, list_test 자체에서 순서 정렬

sorted(list_test)는 메모리 다른 곳에 복사 해서 정렬. 즉, list_test 원본은 변화 없음.



```python
def bRectangleArea(x, y):   # 인자 o, 리턴 값 x
  print(x * y)
  
def cRectangleArea():       # 인자 x, 리턴 값 o
  return(5 * 7)

def dRectangleArea(x, y):   # 인자 o, 리턴 값 o
  return(x * y)
```

<br><br>

## Function Concept 2

### 함수 호출 방식

#### 함수의 인자를 전달하는 방식

* Call by Value 값에 의한 호출 

함수에 인자를 넘길 때 값만 넘김

함수 내에 인자 값 변경 시, 호출자에게 영향을 주지 않음.

* Call by Reference 참조에 의한 호출

함수에 인자를 넘길 때 메모리 주소를 넘김.

함수 내에 인자 값 변경 시, 호출자의 값도 변경 됨.

<br>

#### 파이썬 함수 호출 방식

파이썬은 **객체의 주소가 함수**로 전달되는 방식

전달된 객체를 참조하여 변경 시 호출자에게 영향을 주지만, 새로운 객체를 만들 경우 호출자에게 영향을 주지 않음.

```python
def spam(eggs):
  eggs.append(1) # 기존 객체의 주소값에 [1] 추가
  eggs = [2, 3]  # 새로운 객체 생성
  
ham = [0]
spam(ham)
print(ham)   # [0, 1]
```

<br>

### 변수의 범위 (Scoping Rule)

변수가 사용되는 범위(함수 또는 메인 프로그램)

- Local Variable
- Global Variable : 함수 내 전역변수 사용 시 global 키워드 사용

전역변수는 함수에서 사용 가능. 하지만 함수 내에 전역 변수와 같은 이름의 변수를 선언하면 새로운 지역 변수가 생성 됨.

```python
def calculate(x, y):
  total = x + y
  print("In Function")
  print("a: ", str(a), "b:", str(b), "a+b: " str(a+b), "total: ", str(total))
  return total

a = 5        # a, b는 전역변수
b = 7
total = 0    # 전역변수 total
print("In Program - 1")
print("a: ", str(a), "b:", str(b), "a+b: " str(a+b))

sum = calculate(a, b)
print("After Calculation")
print("Total : ", str(total), "Sum:", str(sum)) # 지역변수는 전역변수에 영향x
```

<br>

### Swap

함수를 통해 변수 간 값을 교환하는 함수

Call by XXXX를 설명하기 위한 전통적인 함수 예시

<br>

**a = [1, 2, 3, 4, 5] 일 때 아래 함수 중 실제 swap이 일어나는 함수는?**

```python
def swap_value(x, y):
  temp = x
  x = y
  y = temp
  
  
def swap_offset(offset_x, offset_y):
  temp = a[offset_x]
  a[offset_x] = a[offset_y]
  a[offset_y] = temp
  

def swap_reference(list, offset_x, offset_y):
  temp = list[offset_x]
  list[offset_x] = list[offset_y]
  list[offset_y] = temp
```

<br>

**swap_offset : a 리스트의 전역 변수 값을 직접 변경**

**swap_reference : a 리스트 객체의 주소 값을 받아 값을 변경**

```python
a = [1, 2, 3, 4, 5]

swap_value(a[1], a[2])
print(a)     # [1, 2, 3, 4, 5]

swap_offset(1, 2)
print(a)     # [1, 3, 2, 4, 5]

swap_reference(a, 1, 2)
print(a)     # [1, 3, 2, 4, 5]
```

<br>

### 재귀함수 Recursive Function

자기 자신을 호출하는 함수

점화식과 같은 재귀적 수학 모형을 표현할 때 사용

재귀 종료 조건 존재, 종료 조건까지 함수 호출 반복

```python
def factorial(n):
  if n == 1 : 
    return 1
  else:
    return n * factorial(n-1)
print(factorial)
```

<br>

## Function arguments

### Passing arguments

- 함수에 입력되는 arguments는 다양한 형태를 가짐

1) Keyword arguments

2) Default arguments

3) Variable-length asterisk (가변인자)

<br>

#### Keyword arguments

함수에 입력되는 parameter의 변수명을 사용, arguments를 넘김.

```python
def print_something(my_name, your_name):
  print("Hello {o}, My name is {1}".format(your_name, my_name))
  
print_something("Jane", "John")
print_something(your_name = "Jane", my_name = "John")
```

<br>

#### Default arguments

parameter의 기본 값을 사용, 입력하지 않을 경우 기본값 출력

```python
def print_something(my_name, your_name="John"):
  print("Hello {o}, My name is {1}".format(your_name, my_name))
  
print_something("Jane", "John")
print_something("Jane")
```

<br>

#### Variable-length asterisk

함수의 parameter가 정해지지 않은 상태. 다항 방정식, 마트 물건 계산 함수 등..

##### 가변인자 using Asterisk

- 갯수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
- keyword arguments와 함께, argument 추가가 가능
- Asterisk(*) 기호를 사용하여 함수의 parameter를 표시함
- 입력된 값은 tuple type으로 사용할 수 있음
- 가변인자는 오직 한 개만 맨 마지막 parameter 위치에 사용 가능

#### 사용

가변인자는 일반적으로 *args를 변수명으로 사용

기존 parameter 이후에 나오는 값을 tuple로 저장

```python
def asterisk_test(a, b, *args):
  return a + b + sum(args)

print(asterisk_test(1, 2, 3, 4, 5))
```

```python
def asterisk_test2(*args):
  x, y, *z = args       # unpacking
  print(x)
  return x, y, z

print(asterisk_test2(3,4,5,10,11,12))
```

<br>

#### Keyword variable-length 키워드 가변인자

Parameter 이름을 따로 지정하지 않고 입력하는 방법

Asterisk(*) 두 개를 사용하여 함수의 parameter를 표시 : **kwargs

입력된 값은 dict type으로 사용할 수 있음

가변인자는 오직 한 개만 기존 가변인자 다음에 사용

```python
def kwargs_test1(**kwargs):
  print(kwargs)

kwargs_test1(first = 3, second = 4, third = 5)

# {'second':4, 'third':5, 'first':3}  으로 출력 됨. 순서 상관 없음.
```

```python
def kwargs_test2(**kwargs):
  print("First value is {first}".format(**kwargs))
  print("Second value is {second}".format(**kwargs))
  print("Third value is {third}".format(**kwargs))
  
kwargs_test2(first=3, second=4, third=5)
```

<br>

## Cording Convention and Function

PEP8 - 파이썬 코딩 컨벤션의 기준

들여쓰기 공백 4칸

한줄은 최대 79자

연산자는 1칸 이상 안 띄움

불필요한 주석 삭제

소문자 i, 대문자 O, 대문자 I 금지

flake8 모듈로 체크 : conda install flake8

<br>

<br>

# Chapter 6. String

## 문자열 String

시퀀스 자료형으로 문자형 data를 메모리에 저장.

영문자 한 글자는 1byte의 메모리 공간을 사용.

```python
>>> import sys    # sys 모듈 호출
>>> print(sys.getsizeof("a")	# a의 메모리 사이즈 출력
```

<br>

### 1 byte의 메모리 공간

이진수 한 자릿수는 1 bit. 0 or 1

1 byte = 8 bit = 2^8 = 256 까지 저장 가능

<br>

## 문자열 특징

### 인덱싱 Indexing

sequence = list

문자열의 각 문자는 개별 주소(offset)를 가짐

이 주소를 사용해 할당된 값을 가져오는 것이 인덱싱

List와 같은 형태로 데이터를 처리

```python
a = "abcde"
print(a[0], a[4])	# a e
print(a[-1], a[5])	# e a
```

<br>

### 문자열 함수

### 문자열 함수 예제

```python
title = "TEAMLAB X Inflearn"
title.upper()
title.split(" ")
title.isdigit()
title.count("a")
title.upper().count("a")
```

<br>

### 다양한 문자열 표현

문자열 선언은 큰따옴표 또는 작은 따옴표

#### It's OK는 어떻게 표현할까?

 1) a = 'lt\' ok.'

 2) a = "It's ok." #

#### 두줄 이상은 어떻게 저장할까?

 1) \n 

 2) 큰따옴표 또는 작은 따옴표 3개

<br>

### 특수문자

문자열을 표시할 때 백슬래시 \ 를 사용하여 키보드로 표시하기 어려운 문자 표현

<br>

<br>

## Lab : Yesterday Counter String

### Beatles의 노래 Yesterday에 Yesterday라는 말이 몇 번 나올까?

```python
wget https://raw.githubusercontent.com/TeamLab/cs50_example_code/master/12_string/yesterday.txt

# 데이터 읽어들이기  
f = open("yesterday.txt", 'r')
yesterday_lyric = ""
while 1:
  line = f.readline()
  if not line:
    break
  yesterday_lyric = yesterday_lyric + line.strip() + "\n"

f.close()

# Yesterday Counter String
n_of_yesterday = yesterday_lyric.upper().count("YESTERDAY")
print("Number of a Word 'Yesterday'", n_of_yesterday)
```

<br>

## Lab : Yesterday Counter 2

대소문자를 구분하여 "Yesterday"와 "yesterday"의 갯수를 나누어서 세는 프로그램을 작성하세요.

```python
n_title_of_yesterday = yesterday_lyric.count("Yesterday")
n_lower_of_yesterday = yesterday_lyric.count("yesterday")
```

<br>

<br>

# Chapter 7. Data Structure

##  데이터 구조

- 스택, 큐 (stack & queue)
- 튜플, 집합 (tuple & set)
- 사전 (Dictionary)



## Stack & Queue

### Stack

- 나중에 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조로 Last In First Out(LIFO)로 구현 됨

- Data의 입력을 Push, 출력을 Pop이라고 함


<br>

#### Stack in python

- 파이썬은 리스트를 사용하여 스택 구조를 활용


-  push를 **append()**, pop을 **pop()** 사용

```python
a = [1, 2, 3, 4, 5]
a.append(10)
a.append(20)
a.pop()		# 20 출력
a.pop()		# 10 출력
```

<br>

#### Stack Example

스택 구조를 활용, 입력된 글자를 역순으로 출력

```python
word = input("Input a word : ")
word_list = list(word)	# String to List
print(word_list)  # ['H', 'e', 'l', 'l', 'o']  : 입력값이 Hello일 경우 한 글자씩 리스트 생성

result = []
for _ in range(len(word_list)):		# _ : 사용하지 않는 것 표시
  result.append(word_list.pop())	# 하나씩 빼면서 출력

print(word[::-1])
```

<br>

### Queue

* 먼저 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조로 First In First Out으로 구현 됨
* Stack과 반대되는 개념

<br>

#### Que in python

 파이썬은 리스트를 사용하여 큐 구조를 활용

 put은 **append()**, get은 **pop(0)**를 사용

```python
a = [1, 2, 3, 4, 5]
a.append(10)
a.append(20)
a.pop(0)	# 1 출력
a.pop(0)	# 2 출력
```

<br>

## Tuple & Set 

### Tuple

- 값의 변경이 불가능한 리스트
- 선언시 "( )"를 사용
- 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용

```python
t = (1, 2, 3)
print(t + t, t * 2)    # (1,2,3,1,2,3)(1,2,3,1,2,3)
t[1] = 5    # error

t = (1)    # 일반정수로 1로 인식
t = (1, )  # 값이 하나인 Tuple은 반드시 ","를 붙여야 함 (1,)
```

#### 왜 쓸까?

프로그램을 작동하는 동안 변경되지 않은 데이터의 저장 (ex) 학번, 이름, 우편번호 등

<br>

### Set

* 값을 **순서 없이** 저장, **중복 불허** 하는 자료형
* set 객체 선언을 이용하여 객체 생성

```python
s = set([1,2,3,1,2,3])    # {1, 2, 3}
s.remove(1)			      # {2, 3}
s.update([1,4,5,6,7])     #{1,2,3,4,5,6,7}
s.discard(3)              #{1,2,4,5,6,7}
s.clear()
```



* 수학에서 활용하는 다양한 집합 연산 가능

```python
s1 = set([1,2,3,4,5])
s2 = set([3,4,5,6,7])

s1.union(s2)	       # {1, 2, 3, 4, 5, 6, 7}
s1|s2                  # {1, 2, 3, 4, 5, 6, 7}  / | : or
s1.intersection(s2)    # {3, 4, 5}
s1&s2                  # {3, 4, 5}
s1.difference(s2)      # {1, 2}
s1 - s2                # {1, 2}
```

<br>

## Dictionary

* 데이터를 저장할 때 구분 지을 수 있는 값을 함께 저장

  (ex) 주민등록번호, 제품 모델 번호

* 구분을 위한 데이터 고유 값을 Identifier 또는 Key 라고 함

* Key 값을 활용하여, 데이터 값(Value)를 관리 함



### 사용

* key와 value를 매칭하여 key로 value를 검색
* 다른 언어에서는 Hash Table이라는 용어를 사용
* {Key1:Value1, Key2:Value2, Key3:Value3 …} 

```python
student_info = {20140012:'Sungchul', 20131490: 'Dahae', 20159482: 'JaeHong'}
sudent_info[20140012]
student_info[2014003] = 'Wonchul'
```

<br>

### Dictionary Handling

```python
>>>country_code={}    # Dict생성
>>>country_code={"America":1,"Korea":82,"China":86,"Japan":81}
>>>country_code
{'America':1,'China':86,'Korea':82,'Japan':81}

>>>country_code.items()    # Dict데이터출력
dict_items([('America',1),('China',86),('Korea',82),('Japan',81)])

>>>country_code.keys()    # Dict키값만출력dict_keys(['America','China','Korea','Japan'])

>>>country_code["Gernman"]=49    # Dict추가
>>>country_code
{'America':1,'Gernman':49,'China':86,'Korea':82,'Japan':81}

>>>country_code.values()    # DictValue만출력
dict_values([1,49,86,82,81])


>>>fork,vincountry_code.items():
...print("Key : ",k)
...print("Value : ",v)
...
Key :America
Value :1
Key :Gernman
Value :49
Key :China
Value :86
Key :Korea
Value :82
Key :Japan
Value :81
>>> "Korea" in country_code.keys()    # Key값에 "Korea"가 있는지 확인
True
>>> 82 in country_code.values()    # Value값에 82가 있는지 확인
True
```

<br>

## Lab : Command Counter

### Command Analyzer

- Command : 사용자가 서버에 입력한 명령어

  어떤 사용자가 얼마나 많이 명령어를 입력하였을까?

```python
import csv

defgetKey(item):    # 정렬을 위한 함수
  returnitem[1]     # 신경쓸 필요 없음

command_data=[]     # 파일 읽어오기
with open("command_data.csv","r")as csvfile:
  spamreader=csv.reader(csvfile,delimiter=',',quotechar='"')
  for row inspamreader:
    command_data.append(row)


command_counter={}    # dict생성, 아이디를key값, 입력줄수를value값
for data in command_data:    # list 데이터를 dict로 변경
  if data[1] in command_counter.keys():    # 아이디가 이미 Key값으로 변경 되었을 때
    command_counter[data[1]]+=1    # 기존출현한아이디
  else:
    command_counter[data[1]]=1     # 처음나온아이디
    
dictlist=[]    # dict를 list로 변경
for key,value in command_counter.items():
  temp =[key,value]
  dictlist.append(temp)
  
sorted_dict=sorted(dictlist,key=getKey,reverse=True) # list를 입력 줄 수로 정렬
print(sorted_dict[:100])    # List의 상위 10개 값만 출력
```



##  Collection module 1

### Collections

* List, Tuple, Dict에 대한 python Built-in 확장 자료 구조(모듈)
* 편의성, 실행 효율 등을 사용자에게 제공함
* 아래의 모듈이 존재함

```python
form collections import deque
form collections import Counter
form collections import OrderedDict
form collections import namedtuple
```

<br>

### deque

* Stack, Queue를 지원하는 모듈
* List에 비해 효율적인 자료 저장 방식을 지원함

```python
from collections import deque

dequeList = deque()
for i in range(5):
 dequeList.append(i)
 
print(dequeList)

dequeList.appendleft(10)
print(dequeList)
```

<br>

* rotate, reverse 등 Linked List의 특성을 지원
* 기존 list 형태의 함수를 모두 지원

```python
dequeList.rotate(2)
print(dequeList)
dequeList.rotate(2)
print(dequeList)

dequeList.extend([5, 6, 7])
print(dequeList)

print(dequeList)
print(deque(reversed(dequeList)))
```

<br>

* deque는 기존 list 보다 효율적인 자료구조 제공
* 효율적 메로리 구조로 처리 속도 향상


<br>

## Collection module 1

### OrderedDict

* Dict와 달리, 데이터를 입력한 순서대로 dict를 반환함


* Dict type의 값을 value 또는 key 값으로 정렬할 때 사용 가능

<br>

### defaultdict

* Dict type의 값에 기본 값을 지정, 신규값 생성 시 사용하는 방법

```python
from collections import defaultdict
d = defaultdict(object)       # Default dictionary를 생성
d = defaultdict(lambda: 0)    # Default 값을 0으로 설정
pirnt(d["first"])             # 0 출력
```

<br>

* 하나의 지문에 각 단어들이 몇 개나 있는지 세고 싶을 경우
* text mining 접근법 : Vector Space Model

소문자로 만든 후, 띄어쓰기 기준으로 자름



```python
from collections import OrderedDict
word_count = defaultdict(object)     # Default dictionary를 생성
word_count = defaultdict(lambda: 0)  # Default 값을 0으로 설정

for word in text:
  word_count[word] += 1
  
for i, v in OrderedDict(scorted(word_cont.items(), 
                                key = lambda t: t[1] reverse = True)).items():
  print(i, v)
  

  
# 참고 : defaultdict 사용한 것과 동일
for word in text:
  if word in word_count.keys():
    word_count[word] += 1
  else:
    word_count[word] = 0
```

<br>

## Collection module 3

### Counter

* Sequence type의 data element들의 갯수를 dict 형태로 반환

```python
from collections import Counter

c = Counter()
c = Counter('gallahad')
print(c)    # Counter({'a':3, 'l':2, 'g':1, 'd':1, 'h':1}) 출력
```

<br>

* Dict type, keyword parameter 등도 모두 처리 가능

```python
c = Counter({'red': 4, 'blue':2})
print(c)
print(list(c.elements()))
# Counter({'red:4, 'blue':2})
#['blue', 'blue', 'red', 'red', 'red', 'red']

c = Counter(cats=4, dogs=8)
print(c)
print(list(c.elements()))
# Counter({'dogs': 4, 'cats': 4})
# ['dogs','dogs','dogs','dogs','cats','cats','cats','cats']

```

<br>

* Set의 연산들을 지원함

```python
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)  # c - d
print(c) 
# Counter({'a':3, 'b':0, 'c':-3, 'd':-6})
```

<br>

* word counter의 기능도 손쉽게 제공

```python
text = """A press release is the quickest and easiest wqy to get free ......""".lower().split()

print(Counter(text))
# Counter({'a':12, 'to'10, 'the':9, ....})
print(Counter(text)["a"])
# 12
```

<br>

### namedtuple

*   Tuple 형태로 data 구조체를 저장하는 방법
*   저장되는 data의 variable을 사전에 지정해서 저장

```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)
print(p[0] + p[1])

x, y = p    # unpacking
print(x, y)
print(p.x + p.y)
print(Point(x = 11, y = 22))
```

<br>

<br>

# Chapter 8.  Pythonic Code 1

## Split & Join

### Split

String Type의 값을 나눠서 List 형태로 변환

```python
items = 'zero one two three'.split()    # 빈칸을 기준으로 문자열 나누기
print(item)    # ['zero', 'one', 'two', 'three']

example = 'python, jquery, javascript'    # ',' 을 기준으로 문자열 나누기
example.split(",")    # ['python', 'jquery', 'javascript']

a, b, c = example.split(",")     # 리스트에 있는 각 값을 a, b, c 변수로 unpacking

example = 'cs50.gachon.edu'
subdomain, domain, tld = example.splic(.)    # '.'을 기준으로 문자열 나누기 -> unpacking
```

<br>

### Join

String List를 합쳐 하나의 String으로 반환할 때 사용

```python
colors = ['red', 'blue', 'green', 'yellow']
rusult = ''.join(colors)
print(result)    # 'redbluegreenyellow'

result = ' '.joing(colors)    # 연결 시 빈칸 1칸으로 연결
print(result)   # red blue green yellow

result = ', '.join(colors)    # 연결 시 ", "으로 연결
print(result)    # 'red, blue, green, yellow'

result = '-'.joing(colors)    # 연결 시 '-'으로 연결
print(result)    # 'red-blue-green-yellow'
```

<br>

<br>

## List Comprehension

### List Comprehension

* 기존 List 사용하여 간단히 새로운 List를 만드는 기법
* 포괄적인 List, 포함되는 리스트라는 의미로 사용 됨
* 파이썬에서 가장 많이 사용되는 기법 중 하나
* 일반적으로 for + append 보다 속도가 빠름

```python
## General Style
result = []
for i in range(10):
  result.append(i)

print(result)    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]


# List Comprehensions 1
result = [i for i in range(10)]
print(result)    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

result = [i for i in range(10) if i % 2 == 0]
print(result)    # [0, 2, 4, 6, 8]

# List Comprehensions 2
word_1 = "Hello"
word_2 = "World"

result = [i + j for i in word_1 for j in word_2]    # Nested For loop
# for i in word_1
#   for j in word_2
#    [i + j]

print(result)
# ['HW', 'Ho, 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er', 'el', 'ed', 'lW', 'lo', 'lr', 'll', 'ld', 'lW', 'lo', 'lr', 'll', 'ld', 'oW', 'oo', 'or', 'ol', 'od'] 
```

```python
# List Comprehensions 3
case_1 = ["A", "B", "C"]
case_2 = ["D", "E", "A"]

result = [i + j for i in case_1 for j in case_2]
print(result)
['AD', 'AE', 'AA', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']

result = [ i + j for i in case_1 for j in case_2 if not(i == j)]

# Filter: i와 j과 같다면 List에 추가하지 않음
result['AD', 'AE', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
result.sort()

print(result)
['AD', 'AE', 'BA', 'BD', 'BE', 'CA', 'CD', 'CE']




words ='The quick brown fox jumps over the lazy dog'.split()
# 문장을 빈칸 기준으로 나눠 list로 변환
print(words)
# ['The','quick','brown','fox','jumps','over','the','lazy','dog']

stuff = [[w.upper(),w.lower(),len(w)] for w in words]
# list의 각 elemente들을 대문자, 소문자, 길이로 변환하여 two dimensional list로 변환

for i in stuff : 
  print(i)
  
# ['THE','the',3]
# ['QUICK','quick',5]
# ['BROWN','brown',5]
# ['FOX','fox',3]
# ['JUMPS','jumps',5]
# ['OVER','over',4]
# ['THE','the',3]
# ['LAZY','lazy',4]
# ['DOG','dog',3]
```

<br>

### Two dimensional & One Dimensional

```python
case_1 = ["A","B","C"]
case_2 = ["D","E","A"]['AD','AE','AA','BD','BE','BA','CD','CE','CA']

result = [i + j for i in case_1 for j in case_2]
print(result)

result = [[i + j for i in case_1] for j in case_2]
print(result)
```

<br>

<br>

## Enumerate & Zip

### Enumerate

* List의 element(sequence type)를 추출할 때 번호(index)를 붙여서 추출

```python
for i,v in enumerate(['tic','tac','toe']):
  # list에 있는 index와 값을 unpacking 
  print(i,v)
  
# 0 tic
# 1 tac
# 2 toe

mylist = ["a", "b", "c", "d"]
list(enumerate(mylist))    # list에 있는 index와 값을 unpacking 하여 list로저장
# [(0,'a'),(1,'b'),(2,'c'),(3,'d')]

{i:j for i,j in enumerate('GachonUniversity is an academic institute located in South Korea.'.split())}
# 문장을 list로 만들고 list의 index와 값을 unpacking 하여 dict로 저장

# {0:'Gachon',1:'University',2:'is',3:'an',4:'academic',5:'institute',6:'located',7:'in',8:'South',9:'Korea.'}

```

<br>

### Zip

* 두 개의 list의 값을 병렬적으로 추출함

```python
alist=['a1','a2','a3']
blist=['b1','b2','b3']
for a,b in zip(alist,blist): # 병렬적으로 값을 추출
  print(a,b)
  # a1 b1
  # a2 b2
  # a3 b3
  
a,b,c = zip((1,2,3),(10,20,30),(100,200,300)) # 각 tuple의 같은 index 끼리 묶음
(1,10,100)(2,20,200)(3,30,300)

[sum(x) for x in zip((1,2,3), (10,20,30), (100,200,300))]
# 각 Tuple 같은 index를 묶어 합을 list로 변환
[111,222,333]
```

<br>

### Enumerate & Zip

```python
alist=['a1','a2','a3']
blist=['b1','b2','b3']
for i,(a,b)in enumerate(zip(alist,blist)):
  print(i,a,b) # index alist[index] blist[index] 표시

0 a1 b1 
1 a2 b2
2 a3 b3
```

<br>

<br>

# Chapter 9. Pythonic Code 2

## Map & Reduce

### Lambda

- 함수 이름 없이, 함수처럼 쓸 수 있는 익명함수
- 수학의 람다 대수에서 유래
- Python3 부터는 권장하지 않으나 여전히 많이 쓰임

```python
# General function
def f(x, y):
    return x + y
print(f(1, 4))

# Lambda Function
f = lambda x, y: x + y
print(f(1, 4))

f = lambda x: x**2
print(f(3))

f = lambda x: x/2
print(f(3))

print((lambda x: x + 1)(5))
```



```python
ex = [1, 2, 3, 4, 5]
f = lambda x: x**2
print(list(map(f, ex)))
```

<br>

### Map & Reduce

- Sequence(ex : list, tuple) 자료형 각 element에 동일한 function을 적용함

  ​

![a](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/map.png?raw=true)

즉, f가 ex 각각의 element마다 mapping이 되어서 결과가 출력 된다.

ex = [1, 2, 3, 4, 5]

ex의 1이 x ** 2에 대입 —> 1 출력

ex의 2가 x**2에 대입 —> 4 출력 , ….

<br>

#### Map function 

두 개 이상의 list에도 적용 가능. if filter도 사용 가능

```python
ex = [1, 2, 3, 4, 5]
f = lambda x, y: x + y
print(list(map(f, ex, ex)))

# lambda function에 if filter 적용
list(
	map(
    lambda x: x**2 if x % 2 == 0
    else x,		# lambda function에는 반드시 else문 작성해야 함
    ex)
)
```

<br>

* Python3는 iteration을 생성하는 식으로 바뀌어서 list를 붙여줘야 list 사용 가능


* generator : 실행시점의 값을 생성, 메모리에 효율적

```python
ex = [1, 2, 3, 4, 5]
#### list 사용
print(list(map(lambda x: x + x, ex)))
# 출력 결과 : [2, 4, 6, 8, 10]

#### generator
print((map(lambda x: x + x, ex)))    
# 출력 결과 : <map object at 0x10fc5103>
# 메모리 주소만 출력 됨. 즉, 생성이 아직 안된 것.

#------------------------------------------------
f = lambda x: x**2
print(map(f, ex))
# for문으로 돌리면 생성 됨.  generator의 특성때문. 
for i in map(f, ex):
    print(i)
# generator는 메모리 상태에서 대기하고 있다가 실행 시점에서 값을 생성해 줌.
    
result = map(f, ex)
print(result)       # <map object at 0x10fc5103>
print(next(result)) # 1
```

<br>

#### Reduce function

* map function과 달리 list에 똑같은 함수를 적용해서 통합

```python
from functools import reduce
print(reduce(lambda x, y: x + y, [1, 2, 3, 4, 5]))

# ((((1 + 2) + 3) + 4) + 5) 순서로 더해져서 값이 구해짐
# 출력 결과 : 15
```



Lambda, map, reduce는 간단한 코드로 다양한 기능을 제공한다. 그러나 **코드의 직관성이 떨어져서** python3에서는 사용을 권장하지 않는다. Legacy library나 다양한 머신러닝 코드에서 여전히 사용중이긴 하다.

<br>

## Asterisk

- 흔히 알고 있는 * 를 의미
- 단순 곱셈, 제곱연산, 가변인자 활용 등 다양하게 사용 된다.

##### *args

```python
def asterisk_test(a, *args):
    print(a, args)
    print(type(args))

asterisk_test(1, 2, 3, 4, 5, 6)

# 출력결과 -----------------------------
1 (2, 3, 4, 5, 6)
<class 'tuple'>
```

<br>

##### **kargs

```python
def asterisk_test(a, **kargs):
    print(a, kargs)
    print(type(kargs))
    
asterisk_test(1, b=2, c=3, d=4, e=5, f=6)

# 출력 결과 -----------------------------
1 {'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 6}
<class 'dict'>
```

<br>

#### Asterisk : unpacking a container

* Tuple, dict 등 자료형에 들어가 있는 값을 unpacking
* 함수의 입력값, zip 등에 유용하게 사용가능

```python
def asterisk_test(a, *args):
    print(a, args)
    print(type(args))
    
asterisk_test(1, *(2, 3, 4, 5, 6))
# 출력 결과 -----------------------------
1 (2, 3, 4, 5, 6)
<class 'tuple'>
# -------------------------------------

def asterisk_test(a, args):
    print(a, *args)
    print(type(args))

asterisk_test(1, (2, 3, 4, 5, 6))
# 출력 결과 -----------------------------
1 2 3 4 5 6
<class 'tuple'>
# -------------------------------------
```

<br>

```python
a, b, c = ([1, 2], [3, 4], [5, 6])
print(a, b, c)

data = ([1, 2], [3, 4], [5, 6])
print(*data)
# 출력 결과 -----------------------------
[1, 2] [3, 4] [5, 6]
[1, 2] [3, 4] [5, 6]
# -------------------------------------


def asterisk_test(a, b, c, d):
    print(a, b, c, d)
data = {"b":1, "c":2, "d":3}
asterisk_test(10, **data)
# 출력 결과 -----------------------------
10 1 2 3
# -------------------------------------


for data in zip(*([1,2], [3, 4], [5, 6])):
    print(data)
# 출력 결과 -----------------------------
(1, 3, 5)
(2, 4, 6)
# -------------------------------------
```

<br>

<br>

## Lab : Simple Linear algebra codes

* Vector를 파이썬으로 표시하는 다양한 방법 존재

```python
vector_a = [1, 2, 10]    # List로 표현
vector_b = (1, 2, 10)    # Tuple로 표현
vector_c = {'x': 1, 'y':1, 'z':10}    # dict로 표현

print(vector_a, vector_b, vector_c)
```

* 최선의 방법은 없음
* 값의 변경 유무, 속성값 유무에 따라 선택 가능



#### Vector handling with python

Python은 특유의 간결성이 최대 장점

Vector와 같은 수학 연산을 복잡하게 표현한다면 사용 어려움

최대한 파이썬만의 특징 살려서 간단하게 연산을 표시

Comprehension과 zip 같은 pythonic technique을 적극 활용

```python
u = [2, 2]
v = [2, 3]
z = [3, 5]

result = [sum(t) for t in zip(u, v, z)]
print(result)

# 출력 결과 : [7, 10]
```

<br>

#### Vector의 계산 : Scalar-Vector product

```python
u = [1, 2, 3]
v = [4, 4, 4]
alpha = 2

result = [alpha * sum(t) for t in zip(u, v)]
print(result)
```

<br>

#### Matrix representation of python

* Matrix 역시 python으로 표시하는 다양한 방법 존재

```python
mat_a = [[3, 6], [4, 5]]    # List
mat_b = [(3, 6), (4, 5)]    # Tuple
mat_c = {(0, 0): 3, (0, 1): 6, (1, 0): 4, (1, 1):5}    # dict
```

* 특히 dict로 표현할 때 수 많은 방법이 있음



#### Matrix 계산 : Matrix addition

```python
mat_a = [[3, 6], [4, 5]]
mat_b = [[5, 8], [6, 7]]
result = [[sum(row) for row in zip(*t)] 
          for t in zip(mat_a, mat_b)]
print(result)
```

위 코드에서   

```python
[t for t in zip(mat_a, mat_b)] 
```

만 출력해보면 `[([3, 6], [5, 8]), ([4, 5], [6, 7])]` 으로 zip으로 묶어준 것.

그 다음 아래 코드에서 

```python
[[row for row in zip(*t)] for t in zip(mat_a, mat_b)] 
```

를 출력해보면 `[[(3, 5), (6, 8)], [(4, 6), (5, 7)]]` 로 unpacking된 것을 확인할 수 있다. ( *t에 `[([3, 6], [5, 8]), ([4, 5], [6, 7])]`이 unpacking 되면서 들어간 것)

<br>

#### Matrix 계산 : Scala-Matrix Product

```python
mat_a = [[3, 6], [4, 5]]
alpha = 4
result = [[alpha * element for element in t] for t in mat_a]
```

<br>

#### Matrix 계산 : Matrix Transpose

```python
mat_a [[1, 2, 3], [4, 5, 6]]
result = [[element for element in t] for t in zip(*mat_a)]
print(result)    # [[1, 4], [2, 5], [3, 6]]
```

`[t for t in zip(*mat_a)]` 출력해보면 `[(1, 4), (2, 5), (3, 6)]`

<br>

#### Matrix 계산 : Matrix Product

```python
mat_a = [[1, 1, 2], [2, 1, 1]]
mat_b = [[1, 1], [2, 1], [1, 3]]
result = [[sum(a * b for a, b in zip(row_a, column_b))
          for column_b in zip(*mat_b)] for row_a in mat_a]
print(result)	# [[5, 8], [5, 6] ]
```

<br>

### 두 개 이상의 Argument가 존재할 때는?

```python
def vector_addtion(*args):
    return [t for t in zip(*args)]

vector_addtion([1, 2], [2, 3], [3, 4])
```

