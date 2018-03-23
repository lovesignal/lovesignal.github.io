---
layout: "post"
date: 2018-02-14
title: 1. Two Sum
excerpt: "LeetCode #1, Easy"
categories: algorithms
comments: true
use_math : true
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# [LeetCode] 1. Two Sum 

https://leetcode.com/problems/two-sum/description/

> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
>
> You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.
>
> 주어진 정수 배열을 이용하여, 임의의 두 수 합계가 타겟(target) 값이 되는 두 숫자의 인덱스를 반환해라.
>
> 각 입력에는 정확히 하나의 솔루션이 있다고 가정 할 수 있으며, 동일한 원소를 두 번 사용할 수 없다.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```


## Approach

### 1. Brute Force

 CS를 전공한 친구에게 문제를 처음 접근할 때 가장 나이브한 방법으로 해 보라는 조언을 들어서 일단 brute force로 접근해보았다. index 0부터 순차적으로 더해서 target과 비교해보는 방법이다.  ` nums[0]+nums[1]==target`  해서 같으면 True로 두 index를 반환하고, 다르면 False이므로   ` nums[0]+nums[2]==target`  처럼 다음 index와 더한다.

### 1.1 Complexity Analysis

 위 알고리즘을 짜 보면 for문이 두개 생성되어서 시간 복잡도가 $O(n^2)$ 이 된다. 각각의 for문의 시간복잡도는 $O(n)$ 이다.

### 1.2 문제 쪼개기

1) i 에 nums의 길이만큼 숫자 대입 `i in len(nums)-1` <br>
2) 기준 숫자와 순차적으로 대입되는 숫자 더하기  `nums[i] + nums[j]`, `j는 1부터 len(nums)`  <br>
3) 더한 숫자와 타겟 비교 `nums[i] + nums[j] == target` <br>
4) `True`일 경우 인덱스 출력 <br>
5) `False`일 경우 비교대상 숫자 하나 증가 <br>

### 1.3 Solution

```python
nums = [2, 11, 14, 7, 15]
target = 9

class Solution:
    def twoSum(self, nums, target):
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if (nums[i] + nums[j]) == target:
                    return i, j
                
test = Solution()
i, j = test.twoSum(nums,target)
print(i, j)
```


### 1.4 문제점

![Leetcode_1](https://lovesignal.github.io/img/post/Algorithms/2018/Feb/Leetcode_1.png)

 시간복잡도가 초과했다는 결과가 나온다. 다른 방법을 찾아보니까 Hash를 이용한 방법이 있다. 



### 2. Hash

Two-pass Hash Table, One-pass Hash Table이 있다. 둘다 Solutions에 나온대로 따라해보고 익혔다.



### 2.1 Two-pass Hash Table

> (발번역이므로 참고만...)
>
> 시간복잡도를 개선하기 위해서, 배열에 보수가 존재하는지 확인하기 위한 효율적인 방법이 필요하다. 보수가 존재하는 경우 해당 index를 탐색할 필요가 있다. Index에 배열의 각 element의 mapping을 유지하기 위한 가장 좋은 방법은 **hash table** 이다.
>
> 속도를 위해 space를 trade함으로써 O(n)에서 O(1)으로 탐색 시간을 감소 시킨다. 해시 테이블은 정확히 이 목적에 맞게 구축되었으며, 거의 일정한 시간의 빠른 탐색을 지원한다. "거의"라고 말한 이유는 충돌이 발행사면 탐색은 O(n) 시간으로 나빠질 수 있다. 하지만 hash 함수가 주의깊에 선택되기만 한다면 hash table의 탐색은  O(1)로 분할된다.  
>
> 심플한 구현은 두개의 반복문이 사용된다. 첫번째 반복문에는,  테이블에 각 요소의 값과 인덱스를 추가한다. 그 다음, 두 번째 반복에서 각 요소의 보수 (target - nums[i])가 테이블에 있는지 확인한다. 보수는 nums[i]가 아니어야한다.



solution처음에 어려워서 stack overflow에 질문했는데 아래와 같은 답변을 받았다.

(stackoverflow 없었으면 CS 공부는 포기했을듯;;)



- stack overflow 질문에 달린 답변 : 

> `Complement` refers to the other number that when added to the current number will give you the value of the `target`.
>
> If (for all) `a` + `b` = `target`, then `a`'s complement is `b`.
>
> In order to see if a complement of **a number** is there, instead of looping through the array (which is O(n)), they are storing it (the elements in the source array) is a hash map.



### 2.1.1 Solution

참고하여 Discuss에 있는 코드를 공부해보았다.

```python
class Solution(object):
    def twoSum(self, nums, target):
        if len(nums) <= 1:
            return False
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]], i]
            else:
                buff_dict[target - nums[i]] = i
```



- nums, target을 인수로 받는 함수를 정의한다.

- nums의 길이가 1이거나 그보다 작으면 계산할 수 없으므로 False를 반환한다.

  ​

- `buff_dict={}` : buff_dict 라는 빈 딕셔너리(해시)를 생성한다.

- `for i in range(len(nums)):` nums의 길이만큼 for문이 loop된다.

- ```if nums[i] in buff_dict: return [buff_dict[nums[i]], i]``` : 

  `nums[i]`가 `buff_dict` 안에 있는 값이면 `buff_dict[nums[i]]와 i` 를 반환한다.

- `else: buff_dict[target - nums[i]] = i` :  

  `nums[i]`가 `buff_dict` 안에 없는 값이면 `buff_dict[target - nums[i]] = i` 를 반환한다.



### 2.1.3 Example

```python
nums = [2, 11, 7, 5]
target = 9

buff_dict = {}

for i in range(len(nums)):
    if nums[i] in buff_dict:
        return [buff_dict[nums[i]], i]
    else:
        buff_dict[target - nums[i]] = i
```

1) **i = 0**

nums[0] = 2 —> buff_dict 에 key 존재 안함 —> buff_dict[9 - 2] = buff_dict[7] = 0

buff_dict 이라는 딕셔너리에 key:7, value:0 이 들어가게 된다. 즉, buff_dict= {7:0} 



2) **i = 1**

nums[1] = 11 —> buff_dict에 key 존재 안함 —> buff_dict[9 - 11] = buff_dict[-2] = 1

buff_dict = {7:0, -2:1}



3) **i = 2** 

nums[2] = 7 —> buff_dict에 key = 7 존재 —> buff_dict[7], 2 를 반환 —> return(0, 2) 

확인해보면, nums[0] = 2, nums[2] = 7 이므로 더하면 target 값 9와 같다.

