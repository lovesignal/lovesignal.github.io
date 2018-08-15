---
layout: post
date: 2018-04-05 
title: Python & Django Day3
tags: [django, python]
categories: programming
comments: true
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## 흐름제어 if, for while

#### Algorithms : 1~100 사이 숫자 맞추기

```python
import random
n = random.randint(1, 100)
while True :
    guess = int(input("정답을 맞춰보세요. :"))
    if n == guess :
        print("정답입니다.")
        break
    elif abs(n - guess) < 10 :
        print("아 아깝습니다.")
    else : 
        print("틀렸습니다.")
```

<br>

### For문

```python
for el in [1, 2, 3, 4]:
    print(el)

# 1
# 2
# 3
# 4

for i in range(100):
    print(i)
```

<br>

### list()

```python
list("python")
# ['p','y','t','h','o','n']

var = []
for i in range(100):
    var.append(i)
print(var)
# [0, 1, 2, 3, ..., 99] # 0부터 99까지 담긴 리스트가 생성된다.

list(range(100))    # 0부터 99까지 들어간 리스트 생성
                    # range() 자체로는 리스트가 아니다.
```

<br>

#### 1부터 100까지 출력하기

```python
n = 1
while n <= 100:
    print(n)
    n += 1

for i in range(100):
    print(i)
    if i > 100:
        break

# 참고
for i in range(1, 101):
    if i % 2 == 0:
        print("{} 짝수입니다.".format(i))
    else:
        pass

```

<br>

#### 1부터 100까지 다 더하기

```python
n = 0
for i in range(1, 101):
    n += i

print(n)
```

<br><br>

### sum()

```python
numbers = [1, 2, 3, 4, 5]
sum(numbers)
# 15

numbers = list(range(1, 101))
sum(numbers)
```

<br>

#### 1부터 100까지 중 2와 3의 약수만 더하기

```python
n = 0
for i in range(1, 101):
    if i % 2 == 0:
         n += i
    elif i % 3 == 0:
        n += i

print(n)
    
```

<br>

#### fizz buzz
1) 1 ~ 100까지 숫자를 순서대로 출력한다
2) 그 숫자가 3의 배수일 때는 숫자 대신 fizz
3) 그 숫자가 5의 배수일 때는 숫자 대신 buzz
4) 그 숫자가 15의 배수일 때는 숫자 대신 fizzbuzz 를 출력

```python
for i in range(1, 101):
    if i % 15 == 0 :
        print('fizz')
    elif i % 5 == 0 : 
        print('buzz')
    elif i % 3 == 0 :
        print('fizzbuzz')
    else : 
        print(i)
```

<br><br>

#### Algorithms : 소수 판별

1) 1 ~ 1000까지 숫자 중에 소수만 출력

소수는 1과 자기자신으로만 나누어 떨어지는 숫자
```python
for i in range(1, 1001):
    key = True
    for j in range(2, i):
        if i % j == 0:
            key = False
            break
    if key:
        print(i)
```
