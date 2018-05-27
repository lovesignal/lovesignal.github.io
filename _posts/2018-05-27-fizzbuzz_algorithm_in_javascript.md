---
date: 2018-05-27
layout : post
title: "[Algorithms] FizzBuzz in Javascript"
excerpt: "알고리즘 문제 fizzbuzz를 이해하고 javascript로 풀기"
comments: true
tags: [algorithms]
use_math: true
---



# 문제

3으로 나누어떨어지는 수일 때는 fizz, 5로 나누어떨어지는 수일 때는  buzz, 3과 5 둘 다 나누어떨어질 때는 fizzbuzz로 숫자를 대체한다.



## Modulus Operator

나누어서 나머지를 출력해주는 연산자로 '%'를 사용할 수 있다.

```javascript
console.log(100%30);    // 10
console.log(7%3)        // 1
```



## Algorithm 

먼저 문제를 해결할 function을 만든다.

```javascript
function fizzbuzz(num){}
```



예를들어, 20이 주어지면 결과가 1부터 20까지 출력되고, 위 조건의 숫자만 fizz, buzz, fizzbuzz로 대체 된다. 그러므로 1부터 20까지 출력될 수 있는 for문을 작성한다.

```javascript
function fizzbuzz(num){
    for(let i=1; i <= num; i++){
        /* each number which is represented by the variable i */
    }
}
```



num이나 i가 3으로 나누어 떨어지면 숫자 대신에 fizz, 5로 나누어 떨어지면 buzz, 3과 5 둘다 나누어 떨어지는 수이면 fizzbuzz가 출력되어야 한다. 앞에서 정리한 modulus operator를 사용하여 조건문을 만들 수 있다.

```javascript
function fizzbuzz(num){
    for (let i = 1; i <= num; i++){
        if (i % 3 === 0) console.log('fizz');      // the number is divisible by 3.
        else if (i % 5 === 0) console.log('buzz'); // the number is divsible by 5.
        else if (i % 15 === 0) console.log('fizzbuzz'); // the number is divisible by both 3 and 5.
        // else if (i % 3 === 0 && i % 5 === 0) console.log('fizzbuzz')
    }
}
```



위 조건문은 한가지 문제점이 있는데 3이나 5로 나누어 떨어지는 조건에 먼저 부합하게 되면 3과 5 둘다 나누어 떨어지는 수는 buzzfizz로 출력될 수 없게 된다. 그러므로 이를 해결하기 위해 3과 5 둘다 나누어지는 조건이 맨 첫번째 if 문으로 위치해야 한다.

나머지 값은 i 값이 그대로 출력되도록 마지막 else문을 만든다.

```javascript
function fizzbuzz(num){
    for (let i = 1; i <= num; i++){
        if (i % 15 === 0) console.log('fizzbuzz'); 
        else if (i % 3 === 0) console.log('fizz'); 
        else if (i % 5 === 0) console.log('buzz');
        else console.log(i);
    }
}
```

