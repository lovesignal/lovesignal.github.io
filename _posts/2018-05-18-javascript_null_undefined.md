---
key: 20180518
title: "[Javascript] null과 undefined"
excerpt: "Javascript의 null과 undefined 비교 정리"
categories: programming
comments: true
tags: [javascript, programming]
---

## null, undefined

ECMAScript 내용에 따르면 아래와 같다.

ECMAScript : <https://www.ecma-international.org/ecma-262/7.0/#sec-undefined-value>



>  4.3.10   undefined value
>
> primitive value used when a variable has not been assigned a value
>
> 
>
> 4.3.11   Undefined type
>
> type whose sole value is the undefined value
>
> 
>
> 4.3.12   null value
>
> primitive value that represents the intentional absence of any object value
>
> 
>
> 4.3.13   Null type
>
> type whose sole value is the null value

<br>

<br>

## null

null은 객체 값의 의도적인 부재를 나타내는 프리미티브 값이다. 즉, 값이 비어다는 것을 개발자가 명시적으로 나타낼 때 null을 사용할 수 있다.

```javascript
let a = null;
console.log(typeof a);
console.log(a);
```

위 코드를 실행하면 타입은 object가 실행되고, a의 값으로는 null이 출력된다.

자바스크립트에서 대부분의 것은 객체이기 때문에 null인지 구분하기 위해서는 typeof를 사용할 수 없다.

아래와 같이 null과 일치하는지 직접 비교해서 null의 변수인지 구분 가능하다.

```javascript
let a = null;
console.log(a === null);
```

<br>

## undefined

undefined는 변수에 값이 할당되지 않은 경우 사용되는 기본값이다. 

아무런 값이 할당되지 않으면 자바스크립트는 자동으로 undefined를 할당한다.

아래 코드를 실행하면 undefined가 출력된다. 즉, **undefined라는 타입**인 것이다.

```javascript
let a;
console.log(typeof a);
```



아래 코드를 실행해도 undefined가 출력된다. 즉, **undefined라는 값**인 것이다.

```javascript
let a;
console.log(a);
```

<br>

<br>

아래 링크 글을 참고하면 이해에 도움이 된다.

A brief history of Null and Undefined in JavaScript: <https://medium.com/@stephenthecurt/a-brief-history-of-null-and-undefined-in-javascript-c283caab662e>

