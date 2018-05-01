---
layout : post 
date: 2018-02-21
title: "[Algorithms] 7. Reverse Integer"
excerpt: "LeetCode #7, Easy"
categories: algorithms
comments: true
tag : [algorithms]
---


# [LeetCode] 7. Reverse Integer

https://leetcode.com/problems/two-sum/description/



> Given a 32-bit signed integer, reverse digits of an integer.
>
> 주어진 32비트의 부호있는 정수의 자릿 수를 뒤집는 문제.
>
> **Example 1:**
>
> ```
> Input: 123
> Output:  321
>
> ```
>
> **Example 2:**
>
> ```
> Input: -123
> Output: -321
>
> ```
>
> **Example 3:**
>
> ```
> Input: 120
> Output: 21
>
> ```
>
> **Note:**
> Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
>
> 32비트의 부호 있는 정수의 범위 안에서만 정수를 저장할 수 있다고 가정한다. 반전된 정수가 오버플로우되면 함수가  0을 반환한다고 가정한다.


<br>
<br>

## Approach

### 1. The flow of thought

 문제를 보고 처음 든 생각은 조건을 어떻게 처리할 것인가이다.

 조건은 총 2가지인데, <u>32비트 범위</u>라는 것과 <u>부호가 있다는 것</u>이다. 둘다 따로 처리하는 게 편할 것 같아서 각각 따로 처리하는 조건문을 만들었다. (J가 부호를 따로 처리하라고 힌트를 줌)

1) 입력값 x의 부호가 양수인지, 음수인지 판단 `sign = 1 ``if (x<0): sign = -1` <br>

2) 자릿수 뒤집는 연산 시행 `int(str(sign(x)*x)[::-1]` <br>

3) 32비트 내의 정수인지 판단 `r > 2**31 -1` <br>

<br>

### 2. Solution

```python
def reverse(x):
    sign = 1
    if (x < 0):
        sign = -1

    r = int(str(sign*x)[::-1])
    return (sign*r, 0)[r > 2**31 - 1]
```



### 3. Another solution

python 솔루션 중 Vote를 가장 많이 받은 코드이다.

```python
def reverse(x):
    s = cmp(x, 0)
    r = int(`s*x`[::-1])
    return s*r * (r < 2**31)
```

