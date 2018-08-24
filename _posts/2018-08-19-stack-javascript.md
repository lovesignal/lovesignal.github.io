---
date: 2018-08-19
layout : post
title: "[Data Structure] JavaScript Stack 구현"
excerpt: "JavaScript Stack 구현하기"
comments: true
tags: [algorithms, javascript]
use_math: true
categories: algorithms
---



## Stack 구현

```javascript
function Stack(){
    let items = [];

    this.push = function(element) {
        items.push(element);
    };

    this.pop = function() {
        return items.pop();
    };

    this.peek = function() {
        return items[items.length-1];
    };

    this.isEmpty = function(){
        return items.length === 0;
    };

    this.size = function(){
        return items.length;
    };

    this.clear = function(){
        items = [];
    };

    this.print = function(){
        console.log(items.toString());
    };
};

let stack = new Stack();
console.log(stack.isEmpty());


// Test
stack.push(1);
stack.push(2);
stack.push(3);
stack.print();
console.log(stack.size());
console.log(stack.isEmpty());

stack.pop();
stack.pop();
stack.print();
```

<br>

<br>

## 예제 : 10진수 -> 2진수 변환

10진수를 2진수로 바꾸는 방법 : 몫이 0이 될 때까지 2로 나눈다. 

```javascript
function diviedeBy2(decNumber) {
    let remStack = new Stack();
    let rem;
    let binaryString = '';

    while (decNumber > 0){
        rem = Math.floor(decNumber % 2);
        remStack.push(rem);
        decNumber = Math.floor(decNumber / 2);
    }

    while (!remStack.isEmpty()){
        binaryString += remStack.pop().toString();
    }

    return binaryString;
}

console.log(diviedeBy2(240)); // 11110000
```

