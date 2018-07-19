---
layout: post
title: Python & Django Day9 기초알고리즘(정렬)
tags: [django, python]
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## 알고리즘

어떤 문제를 풀기 위한 절차 혹은 방법

<br>

### 계산복잡도

알고리즘의 계산복잡도를 나타내는 방법 중 하나로 **Big O 표기법**이 있다.

* O(n) : n이 커질 수록 시간복잡도가 올라간다.

  ​

![Big O Complexity](https://cdn-images-1.medium.com/max/800/1*yekzNjsqZzGCET2KotEROQ.png)

<br><br>

### 정렬문제

1. 선택정렬
2. 삽입정렬
3. 병합정렬
4. 퀵정렬

<br>

#### 선택정렬 : O(n)

```python
from random import choice

raw_list = list(range(0, 100+1))
# raw_list = [0, 1, 2, 3, ..., 100]

target = []
for _ in range(100):
    target.append(choice(raw_list))

def selection_sort(A):
    result = []

    while len(A) != 0:
        min_num = 100
        for i in A:
            if min_num > i:
                min_num = i
    
        result.append(min_num)
        A.remove(min_num)
    return result

print(selection_sort(target))
```

<br>

* 연습

  1) 랜덤한 숫자를 포함하는 리스트를 역순으로 선택정렬하는 함수 만들기

```python
from random import choice

raw_list = list(range(-50, 50+1))
# raw_list = [0, 1, 2, 3, ..., 100]

target = []
for _ in range(100):
    target.append(choice(raw_list))

def selection_sort(A):
    result = []

    while len(A) != 0:
        max_num = A[0] 
        for i in A:
            if max_num < i:
                max_num = i
    
        result.append(max_num)
        A.remove(max_num)
    return result

print(selection_sort(target))
```



<br>

   2) 0, 1로만 이루어진 리스트(순서는 랜덤)을 정렬하기. 가장 빠른 방법을 찾아보기

```python
from random import choice

raw = [0, 1]

target = []
for _ in range(1000):
    target.append(choice(raw))

def solution(A):
    length = len(A)
    sum_1 = sum(A)
    string_value = '0' * (length - sum(A)) + '1' * sum_1
    return list(map(int, list(string_value)))

print(solution(target))
```



<br>

#### 병합정렬 : O(n log n)

![](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif) 

출처 : Wikipedia

<br>

```python
from random import choice

raw = list(range(-50, 50+1))

target = []
for _ in range(100):
    target.append(choice(raw))

print(target)

def _merge(A, B):
    result = []
    length = len(A) + len(B)
    for _ in range(length):
        try:
            if A[0] > B[0]:
                result.append(B[0])
                B.remove(B[0])
            else:
                result.append(A[0])
                A.remove(A[0])
        except IndexError:
            if len(A):
                result += A
                break
            else:
                result += B
                break
    return result

def merge_sort(A):
    if len(A) < 2:
        return A
    left_list = merge_sort(A[:len(A)//2])
    right_list = merge_sort(A[len(A)//2:])
    return _merge(left_list, right_list)

print(merge_sort(target)
```

<br><br>

## Memorization

### fibonacci

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


def fib(n):
    if n <=2:
        return 1
    return fib(n-1) + fib(n-2)

@check_time
def find_fib(n):
    return fib(n)

print(find_fib(34))


### Memorization 이용하여 속도 개선
MEMO = {}

def fib2(n):
    if n <= 2:
        return 1
    if MEMO.get(str(n-1)):
        fib_n_1 = MEMO[str(n-1)]
    else:
        fib_n_1 = fib2(n-1)
        MEMO[str(n-1)] = fib_n_1
    if MEMO.get(str(n-2)):
        fib_n_2 = MEMO[str(n-2)]
    else:
        fib_n_2 = fib2(n-2)
        MEMO[str(n-2)] = fib_n_2
    f_n = fib_n_1 + fib_n_2
    MEMO[str(n)] = f_n
    return f_n

@check_time
def find_fib2(n):
    return fib2(n)

print(find_fib2(34))


#----결과-----
함수 실행에 걸린 시간은  1.6375880241394043
5702887
함수 실행에 걸린 시간은  6.4849853515625e-05
5702887
```


