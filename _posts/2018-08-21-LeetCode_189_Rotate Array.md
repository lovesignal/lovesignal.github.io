---
layout : post
date: 2018-08-21
title: "[Algorithms] LeetCode 189. Rotate Array"
excerpt: "LeetCode 189 문제 풀이"
categories: algorithms
comments: true
tag : [algorithms, leetcode]
---



Given an array, rotate the array to the right by k steps, where k is non-negative.

<br>

### Example 1:
```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

<br>

### Example 2:

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation:
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

<br>

### Note:

  * 	Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
  * 	Could you do it in-place with O(1) extra space?

<br>


## Solutions Code with JavaScript
### Solution 1

Input k = 3
[1, 2, 3, 4, 5, 6]
Output:
[4, 5, 6, 1, 2, 3]

<br>

맨 뒤의 원소가 앞으로 이동하면 되므로 pop으로 맨 뒤 원소 한개를 꺼내서 unshift로 다시 앞에 추가 시켰다. Stack을 떠올리거나 젠가에서 블록을 빼서 위에 얹는 것과 유사하고 생각했다.
```javascript
for(let i = 0; i < k; i++) {
    nums.unshift(nums.pop(1))
};
```

<br>

### Solution 2

Leetcode discuss에 있던 다른 솔루션이다. unshift와 splice를 이용했다.
```javascript
let rotate = function(nums, k) {
    for(var i = k; i > 0; i--){
        nums.unshift(nums.splice(nums.length- 1 , 1)[0])
    }
};
```