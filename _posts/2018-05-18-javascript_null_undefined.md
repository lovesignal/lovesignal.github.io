---
layout: post
date: 2018-05-18
title: "[Javascript] null과 undefined 비교"
excerpt: "Javascript의 null과 undefined 비교"
categories: programming
comments: true
tags: [javascript, programming]
comments: true
---



## 공통점

null, undefined 둘다 값이 비어있다.

<br>

## 차이점

### null

```javascript
let a = null;
console.log(typeof a);
console.log(a);
```

위 코드를 실행하면 타입은 object가 실행되고, a의 값으로는 null이 출력된다.

null은 비어 있거나 존재하지 않는 값을 나타낸다. 

자바스크립트에서 대부분의 것은 객체이기 때문에 null인지 구분하기 위해서는 typeof를 사용할 수 없다.

아래와 같이 null과 일치하는지 직접 비교해서 null의 변수인지 구분 가능하다.

```javascript
let a = null;
console.log(a === null);
```

프로그래밍에서 암묵적인 것보다 명시적인 것이 선호된다. 값이 비어있고, 할당되지 않았음을 개발자가 명시적으로 나타낼 때 null을 사용할 수 있다.

<br>

### undefined

아무런 값이 할당되지 않으면 자바스크립트는 undefined를 할당한다.

아래 코드를 실행하면 undefined가 출력된다. 즉, **undefined라는 타입**인 것이다.

```javascript
let a;
console.log(typeof a);
```

<br>

아래 코드를 실행해도 undefined가 출력된다. 즉, **undefined라는 값**인 것이다.

```javascript
let a;
console.log(a);
```

undefined는 타입, 값 둘다 가능하다.  undefined는 최대한 사용을 배제하고 정해지지 않은 값에 대해서는 null을 할당해주는 것이 좋다.

<br>

Javascript는 7일만에 만든 언어라고 한다. undefined는 짧은 개발 기간탓에 발생한 오류인 것으로 추정된다.