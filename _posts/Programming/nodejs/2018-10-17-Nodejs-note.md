---
key: 20181017
title: "[Node.js] Node.js 학습 및 정리"
excerpt: "Node.js 공부노트 (작성 중..)"
categories: programming
comments: true
tags: [nodejs, programming, javascript, backend]
---



# 1.1 Node.js 정의

* Node.js 정의

  Chrome V8 Javascript 엔진으로 빌드된 Javascript runtime이다. 

* Runtime 정의

  컴퓨터 프로그램이 실행되고 있는 동안의 동작.

* Runtime Environment 정의

  컴퓨터가 실행되는 동안 프로세스나 프로그램을 위한 소프트웨어 서비스를 제공하는 가상 머신의 상태



즉, 노드는 가상머신이라고 봐도 된다. 실제로 Node 안에 가상머신이 들어 있다. 런타임은 자바스크립트를 웹브라우저 바깥에서 동작할 수 있게 해주는 프로그램이라고 생각해도 무방하다. 원래 자바스크립트는 웹브라우저 안에서 돌아가는 언어였고 노드의 등장으로 자바스크립트가 웹브라우저 바깥에서도 동작할 수 있게 되었다. 





# 1.2 REPL과 헬로 노드

* REPL (Read Evaluate Print Loop)





# 1.3 호출 스택과 이벤트 루프

## Node의 핵심 개념 3가지

🔘 Event 기반

🔘 Non blocking I/O Model

🔘 Single Thread





## 이벤트 루프

*참고 : 

https://www.zerocho.com/category/JavaScript/post/597f34bbb428530018e8e6e2

https://goo.gl/JrGkZs

http://asfirstalways.tistory.com/362



### Stack

```javascript
function first(){
    second();
    console.log('첫 번째');
}
function second(){
    third();
    console.log('두 번째');
}
function third(){
    console.log('세 번째');
}
first(); // 첫 번째, 두 번째, 세 번째
```



### Task Queue

```javascript
function run(){
    console.log('3초 후 실행');
}
console.log('시작');
setTimeout(run, 3000);
console.log('끝');     // 시작, 끝, 3초 후 실행
```



Task Queue는 Stack의 반대되는 개념. 

Stack은 차곡차곡 쌓이면 위에서 부터 사라지게 된다(LIFO). 반대로 Queue는 먼저 들어온 순서대로 나간다(FIFO).



`setTimeout(run, 3000)` 부터 실행을 도식화 해보면 아래와 같다.

<img src="https://raw.githubusercontent.com/lifeisgouda/img/master/programming/nodejs/img1.png">

최종적으로 stack과 Queue가 모두 비워지면 프로그램이 종료된다.



🔘 언제 Task Queue에 들어가는가

1. setTimeout
2. setInterval
3. setImmediate
4. Promise resolve, reject
5. async, await
6. EventLister의 callback



💡 프로그램이 실행되다 보면 Queue가 여러개 있고 계속 쌓이게 되는데, 이때  **Task Queue에서 정해진 순서대로 꺼내오는 것이 Event Loop의 역할이다.** (Event Loop는 순서를 알고 있다.) 이것을 잘 사용하면 실행순서를 바꿔서 실행시킬 수 있다.



<img src="https://raw.githubusercontent.com/lifeisgouda/img/master/programming/nodejs/task_queue.png" width="70%">







# 1.4 Event driven, Non blocking I/O Model, Single Thread 

### 생각해보기

Node가 서버의 역할을 하려면 어떻게 해야 할까?



🔘서버

<u>클라이언트가 요청을 보낸 것을 받아서 응답을 하는 것.</u> 서버가 서버한테 요청을 보낼 수도 있다. 이 경우 서버가 클라이언트가 된다. 예를들어 웹 주소를 입력하는 것도 요청이다. 웹주소를 입력하면 서버를 찾아가서 서버에게서 html을 받아온다(즉, 응답으로 html을 받는 것). 인터넷 브라우저는 받아온 것을 파싱해서 화면으로 만들어 주는 것이다.  

* 요청의 특징 : 언제 올지 모른다. 이때 대기할 때 사용하는 것이 `EventListener` 이다. 



## Event Driven

호출 stack과 task queue가 비어 있지만 EventListener에 등록해둔 것 덕분에 프로그램이 계속 동작한다. 이 동작 방식을 Event Driven이라고 한다.



<img src="https://raw.githubusercontent.com/lifeisgouda/img/master/programming/nodejs/event-driven.png">

* 참고 : http://jasonim.me/dev/146



## Non Blocking I/O

### Non Blocking 

위에서 봤던 `setTimeout(run, 3000)` 에서 `run ` 을 Task Queue로 보낸다. 이렇게 **Task Queue로 보내고 실행 순서가 바뀌게 되는 동작을 Non blocking**이라고 한다. (실행 순서의 문제)



### I/O (Input Output)

* 파일시스템 I/O
* 네트워크 I/O

위 두가지는 자체적으로 Non Blocking으로 동작한다. 

파일시스템의 경우는 더 나아가서 알아서 Multi thread를 돌린다. 즉, Non blocking에 팔까지 여러개 달아서 Multi thread로 작업하는 것이다.





## Single Thread

사람으로 치면 팔의 갯수라고 보면 된다. Single Thread는 팔이 한개라서 한번에 한가지 일만 할 수 있다. Multi Thread는 팔이 여러개이기 때문에 동시에 작업이 가능하다. 

<u>자바스크립트는 Single Thread이다. 그래서 blocking이 일어나는데, 그것을 극복하기 위해 Non blocking으로 순서를 바꾸어서 효율적으로 처리할 수 있게 만드는 것이다.</u> 



Multi thread로 프로그래밍 하는 것이 어려운 측면이 있다. Node가 쓰는 Multi thread를 흉내내는 방식은 왼팔만 여러개를 달아놓은 것과 비슷해서 흉내는 냈지만 부족한 면이 있다.

정확하게 말하면 thread 보다 상위 개념으로 proccess가 있는데 Node가 Multi thread를 흉내내는 방식은 이 proccess를 여러개 만들어서 Multi proccessing을 하는 것이 Node가 single thread의 단점을 극복하는 방법중 하나이다.





# 2.1 const와 let

const에 객체가 할당된 경우 객체 내부 속성은 바꿀 수 있다. 즉, 참조에 대한 상수는 변경 가능.

```javascript
const val = {a: 1, b: 2, c: 3};
val.a = 3;
val.b = 1;     // 객체 내부속성 변경 가능

const h = [1, 2, 3, 4]
h[0] = 4;
h[3] = 2;     // 객체 내부속성 변경 가능
```





# 2.2 템플릿 문자열(백틱, `)

백틱을 양 끝에 사용하면 하나의 문자열로 인식한다.

```javascript
const a = 'hello';
const b = true;
const c = 3;

const d = a + ' ' + b + ' ' + c;
const e = `${a} ${b} ${c}`     // 위에 코드와 같은 의미

const f = `${a}는 ${b}이고 ${c}은 몰라요.` 
```







# 2.3. 객체 리터럴의 변화

객체 리터럴 : `let val = {}`



```javascript
var sayNode = function(){
    console.log('Node')
};
var es = 'ES';

// ES6 이전 문법
var oldObject = {       
    sayJS: function(){
        console.log('JS');
    },
    sayNode: sayNode,     // key와 value 같음
};

oldObject[es + 6] = 'Fantastic';   // Fantastic
oldObject.sayNode();    // Node



// ES6 이후 문법
let newObject = {
    sayJS(){
        console.log('JS');
    },
    sayNode,   // key와 value가 같은 경우 한 번만 작성할 수 있게 바뀜
    [es + 6]: 'Fantastic',  // 동적 속성 할당을 리터럴 안에 표현 가능. {[변수]: 값} ***
};

newObject.sayJS();    // JS
newObject.sayNode();  // Node
console.log(newObject.ES6);  // Fantastic
```





# 2.4 화살표 함수

### 함수 선언문

변수를 선언하고 함수를 대입.

```javascript
let add = function(x, y){
    return x + y;
}

let add = (x, y) => x + y ;
```



### 함수표현식

함수에 이름 붙여서 선언하는 것.

```javascript
function add(x, y){ return x + y };
```





## function() 이 살아남은 이유

### function()과 화살표 함수의 가장 큰 차이 : this

function()과 화살표 함수의 this는 동작하는 방식이 다르다. 



#### function() 사용한 경우 this 동작

```javascript
let relationship1 = {      // let relationship = {} : 객체 리터럴 생성
    name: 'zero',
    friends: ['nero', 'hero', 'xero'],
    logFriends: function() {
        let that = this;   // relationship1을 가리키는 this를 that에 저장
        this.friends.forEach(function(friend){
            console.log(that.name, friend);  // 바깥의 this를 가져오기 위해 that에 대입해서 가져옴
        });
    },
};

relationship1.logFriends();
/* zero nero
 * zero hero
 * zero xero
 */
```



#### 화살표 함수 사용한 경우 this 동작

* ** 부분 : 여기서 화살표함수 `friend =>` 를 쓰면 **화살표 함수 내부의 this** `this.name`  를 **화살표 함수 밖의 this** `this.friends.forEach` 와 <u>같은 것으로 만들어준다.</u>

  즉, `this.friends.forEach( ... => ... this)` 화살표 함수 통해서 바깥의 `this` 가 안의 `this` 에 적용된다.

```javascript
let relationship2 = {
    name: 'zero',
    friends: ['nero', 'hero', 'xero'],
    logFriends() {
        this.friends.forEach(friend => {     // **
            console.log(this.name, friend);   // this : 원래 window
        });
    },
};

relationship2.logFriends();
```





# 2.5 비구조화 할당 (destructuring)

## 객체에서 비구조화 할당

```javascript
let candyMachine = {
    status: {
        name: 'node',
        count: 5,
    },
    getCandy(){
        this.status.count--;
        return this.status.count;
    }
}

var status = candyMachine.status;     // 변수와 속성의 이름이 같다
let getCandy = candyMachine.getCandy;
```



`var status = candyMachine.status;` 처럼 변수와 속성의 이름이 같을 때 ES6에서는 간단하게 표현할 수 있게 새로운 문법을 제공한다.  (🔑 활용도가 매우 높은 문법) 

```javascript
let {status, getCandy} = candyMachine;
```



* Example

```javascript
const { Router } = require('express');    
// require express라는 객체에서 Router라는 속성값을 Router 변수에 대입
```



📌 비구조화 할당 시 `this` 가 의도와 다르게 동작하는 현상이 있을 수 있다. ⛔️⛔️⛔️

```javascript
candyMachine.getCandy();  // 4

const { getCandy } = candyMachine;
getCandy();              // undefined
```

`candyMachine.getCandy();` 에서 `getCandy()` 를 갖고 있는 객체 `candyMachine.` 이 앞에 붙어 있으면 `getCandy()` 가 호출이 될 때 `this` 를 앞에 붙어 있던 객체  `candyMachine.` 로 만든다. 

마지막줄의 비구조화 할당 후 `getCandy()` 를 보면 앞에 객체가 안붙어 있다. 그래서 `getCandy()` 가 `this` 인 `candyMachine` 을 못찾는다.  `getCandy` 를 호출해도 `candyMachine` 이 바뀌지 않고 undefined가 출력되는 것이다. 

그러므로 **반드시 앞에 객체를 붙여줘야 한다**. 구조분해 할당으로 `candyMachine` 과 분리되면서 나타나는 현상이다. 





## 배열에서 비구조화 할당

```javascript
const a = array[0];
const b = array[1];

const [a, b] = array;

// 참고 : array[array.length - 1]  배열의 마지막 요소 가져오는 코드
```



* Example

```javascript
const array = ['node', {}, 10, true];
const [node, obj, ...bool] = array;
console.log(bool); // (2) [10, true]


const m = (x, y) => console.log(x, y);
m(5, 6);   // 5 6
m(5, 6, 7, 8, 9)  // 5 6


const n = (x, ...y) => console.log(x, y);
n(5, 6, 7, 8, 9);  // 5 [6, 7, 8, 9]
                   // ** argumnet는 배열처럼 보이지만 배열이 아님. 유사배열.

const p = (...rest) => console.log(rest);    // rest는 배열. 이 방식이 더 좋음.
p(5, 6, 7, 8, 9);   // [5, 6, 7, 8, 9]
```





# 2.6 rest 문법

### rest 문법

```javascript
const n = (x, ...y) => console.log(x, y);
n(5, 6, 7, 8, 9);  // 5 [6, 7, 8, 9]
                   // ** argumnet는 배열처럼 보이지만 배열이 아님. 유사배열.

const p = (...rest) => console.log(rest);    // rest는 배열. 이 방식이 더 좋음.
p(5, 6, 7, 8, 9);   // [5, 6, 7, 8, 9]
```



### 참조

변수는 메모리에 위치하는데 이 경우 y는 x를 참조하고 있다. 즉, x가 저장된 메모리 값을 가리키고 있는 것이다. 

```javascript
const x = {a: 1, b: 2};
let y = x;     // y가 x를 참조하고 있는 것
```

const는 가리키고 있는 위치를 바꿀 수 는 없지만 그 안에 있는 값은 바꿀 수 있는 것이다.







# 2.7 Callback과 Promise 비교

## 전형적인 콜백 코드

```javascript
Users.findOne('zero', (err, user) => {
    if (err) {
        return console.error(err);
    }
    console.log(user);
})
console.log('다 찾았니?');
```

예를들어, 데이터 베이스에 `Users` 라는 폴더가 있고 `findOne` 이 `zero` 라는 한 사람을 찾아오는 것이라고 한다면,

`zero` 를 찾았을 때 콜백이 실행되는 것이다.  ( `(err, user) => { ....` 이하가 콜백)

콜백을 쓰는 이유는 코드가 non-blocking으로 작동하기 때문이다. 



`console.log(user);` 보다 `console.log('다 찾았니?');` 가 먼저 뜨게 된다. 왜냐하면 `Users.findOne('zero'` 은 네트워크를 통해서 데이터 베이스에서 검색하므로 시간이 얼마나 걸릴 지 모르기 때문에 Non blocking 방식으로 먼저 요청만 보내놓고 그 다음 코드를 실행하기 때문이다.

다 찾은 경우 event loop로 콜백을 넣어줘서 실행되는 것이다. 찾는 과정에서 에러가 있다면 `console.error(error);` 가 실행되는 것이다. 



단점은 순서가 매우 애매하다. 콜백이 연달아 있는 경우 실행순서가 어떻게 흘러가는지 파악하기 어려운 문제가 있다. (callback hell)

```javascript
Users.findOne('zero', (err, user) => {
    if (err) {
        return console.error(err);
    }
    console.log(user);
    Users.update('zero', 'nero', (err, updatedUser)=> {
        console.log(updateUser);
        Users.remove('nero', (err, removeUser) => {
            if (err) {
                return console.error(err);
            }
            console.log(removeUser);
        });
    });
});
console.log('다 찾았니?');
```



## Promise

위 코드에 Promise를 적용하면 아래와 같다.

```javascript
Users.findOne('zero')
  .then((user) => {
    console.log(user);
    return Users.update('zero', 'nero');
  })
    .then((updatedUser) => {
      console.log(updatedUser);
      return Users.remove('nero');
  })
    .then((removedUser) => {
      console.log(removeUser);
  });
  .catch((err) => {        // 에러처리는 마지막에 한번
    console.error(error);
  });
  console.log('다 찾았니?'); 
```





# 2.8 Promise 이해하기

## Promise를 만드는 방법

함수의 맨 첫글자가 대문자이면 생성자라는 의미이다. 앞에 `new` 를 써서 생성가능하다는 것을 알려준다.

```shell
> Promise
  Promise() { [native code] }
```



### Promise 생성 구조

Promise를 생성할 때 구조는 아래와 같다.

```javascript
new Promise((resolve, reject) => { 
    // resolve와 reject가 매개변수인 함수를 넣는다 
});

plus
    .then(() => {  // resolve가 되면 then이 실행되고
    
  })
    .catch(() => {    // reject가 되면 catch가 실행된다
    
  })
```



#### Example

```javascript
const plust = new Promise((resolve, reject) => { 
    const a = 1;
    const b = 2;
    if (a + b > 2){
        resolve(a + b);   // resolve( 성공 메시지 )
    } else {
        reject(a + b);    // reject( 실패 메시지 )
    }
});


plus
  .then((success) => {  // resolve가 되면 then 실행
    console.log(success);
  })
  .catch((fail) => {    // reject가 되면 catch 실행
    console.log(fail);    
  })
```

`.then` , `.catch` 는 함수 내부적으로 이미 `promise` 를 return 하도록 정의되어 있기 때문에 사용할 수 있는 것이다. 즉, 내부적으로 promise 지원 되는 것들만 적용할 수 있다. 왠만한 라이브러리들은 모두 지원한다. 



```javascript
const condition = true; // true면 resolve, false면 reject
const promise = new Promise((resolve, reject) => {
    if (condition) {
        resolve('성공');
    } else {
        reject('실패');
    }
});

promise
  .then(message) => {
    console.log(message); // 성공(resolve)한 경우 실행
  })
  .catch((error) => {
    console.error(error);  // 실패(reject)한 경우 실행      
  })
```



## then이 여러개인 구조

then에 **<u>리턴값이 있으면</u> 다음 then으로 넘어간다.** Promise를 리턴하면 resolve나 reject되어 넘어간다.

```javascript
promise
  .then(message) => {
    return new Promise((resolve, reject) => {
        resolve(message2);
    });
  })
  .then(message2) => {
    return new Promise((resolve, reject) => {
        resolve(message3);
    });
  })
  .then(message3) => {
    return new Promise((resolve, reject) => {
        resolve(message3);
    })
  })
  .catch((error) => {
    console.error(error); 
  });
```





# 2.9 Promise API

무조건 성공하거나 실패하는 Promise는 아래와 같이 줄일 수 있다.

```javascript
// 무조건 성공
const successPromise = Promise.resolve('성공');
  .then();

// 무조건 실패
const failurePromise = Promise.reject('실패');
  .catch();

// 아래 코드를 줄인 것
const promise = new Promise((res, rej) => {
    rej('실패');
});
```



## Promise의 장점

`Promise.all` 을 이용해서 한꺼번에 실행 가능하다. 다만, 하나라도 실패하면 모두 에러가 되는 단점이 있다. 

```javascript
Promise.all([Users.findOne(), Users.remove(), Users.update()])
  .then((results) => {})
  .catch((error) => {})
```



## 정리 및 활용

Promise는 결과를 실행했는데 바깥에 표시를 안해준 것이라고 생각하면 된다.

```javascript
const promise = new Promise((res, rej) => {
    res('성공');
});
```

promise 변수는 이미 성공했다는 것을 이미 알고 있지만 바깥으로 꺼내지 않은 것이다. `promise.then(() => {})` 으로 꺼낼 때 바깥으로 드러난다. 이것의 장점은 바로 꺼내지 않았기 때문에 언제든지 필요할 때 쓸 수 있는 것이다. (비장의 카드 느낌?!) 결과를 갖고 있는 부분과 드러내는 부분이 분리된다는 것도 장점이다. 



아래 콜백 코드의 문제점은 바로 결과를 사용하는 부분이 이어지게 된다. 중간에 다른 코드 삽입 불가.

```javascript
Users.findOne('zero', (err, user) => {
    console.log(user);
})
```

Promise로 바꾸면,

```javascript
const zero = Users.findOne('zero');

// 다른 로직...

zero.then((z) => {
    console.log(z);
});
```





# 2.10 async / await

콜백이 한번 콜백으로 넘어가면 모두 콜백 안에서 로직이 구성되어야 하는 것 처럼, 

`Promise` 도 한번 `.then` 이나 `.catch` 로 넘어가면 모든 로직이 `.then`, `.catch` 안에서 이루어져야 하는 문제점이 있다.

```javascript
Users.findOne('zero')
  .then((user) => {
    console.log(user);
    return Users.update('zero', 'nero');
  })
    .then((updatedUser) => {
      console.log(updatedUser);
      return Users.remove('nero');
  })
    .then((removedUser) => {
      console.log(removedUser);
  });
  .catch((err) => {        
    console.error(error);
  });
  console.log('다 찾았니?'); 
```



`console.log('다 찾았니?'); ` 는 첫 번째 `.then` 보다 먼저 실행된다. 즉, Promise로 가독성을 높였다고는 하지만  순서대로 실행되지 않는다는 것은 동일하다. 그래서 `*`, ` yield` 생성자가 만들어졌다가 ES6부터 `async` / `await` 가 공식적으로 등록 되었다. 순서대로 실행되는 것 처럼 보이게 만들 수 있다. 



위 코드를 `async` / `await` 으로 바꾸면 아래와 같다.

```javascript
async func() => {
    try{
      const user = await Users.findOne('zero');
      console.log(user);
      const updatedUser = await Users.update('zero', 'nero');
      console.log(updatedUser);
      const removedUser = await Users.remove('nero');
      console.log(removedUser);
      console.log('다 찾았니?');
    } catch (err) {
       console.error(error);   // 이 경우 에러가 나도 어느 부분인지 알 수 없다. 
    }
}

func();
```

`await` 쓸 때는 함수가 필요하다. 함수 이름 앞에 `async` 를 붙여주면 된다. 익명함수도 가능.



어느 부분에서 에러가 낫는지 알고 싶으면 try-catch를 개별적으로 해줘야 한다.

```javascript
async func() => {
    try{
      const user = await Users.findOne('zero');
      console.log(user);
    } catch (err) {
       console.error(error);   
    }
    try{ 
      const updatedUser = await Users.update('zero', 'nero');
      console.log(updatedUser);
      const removedUser = await Users.remove('nero');
      console.log(removedUser);
      console.log('다 찾았니?');
    } catch (err) {
       console.error(error);   
    }
}

func();
```





# 3.1 Node Module System

## Module System

**모듈 시스템**은 ES2015에서 나온 획기적인 변화이다. 자바스크립트는 예전부터 리소스 관리가 어려워서 말이 많았다. 리소스는 웹 페이지를 구성하는 자원들이다. 현재 웹에서는 해당 페이지에 필요한 모든 파일을 미리 불러와야 하고, 그 파일들이 사용하는 변수가 겹치지 않나 잘 살펴봐야 한다. 이런 부분을 해결한 것이 모듈 시스템이다.



## 모듈 만들기

아래 만든 JS파일을 다른 프로그램에서 쓰고 싶다면 어떻게 해야 할까?

```javascript
// var.js
const odd = "홀수입니다.";
const even = "짝수입니다.";

console.log(odd);
even = even + 'zero';
```

```javascript
// func.js
console.log(odd);
console.log(even);
```



### HTML

프론트엔드 방식(HTML)이면 아래처럼 불러들여서 사용한다.

```html
<!-- example.html -->
<script src="var.js"></script>
<script src="func.js"></script>
```



### Javascript

먼저 불러들여지는 파일에서 export가 가능하도록 `module.exports` 를 입력해준다.

```javascript
// var.js
const odd = "홀수입니다.";
const even = "짝수입니다.";

// 모듈로 만들어질 준비가 되었다는 선언
module.exports = {    // ES6의 문법. 이전에는 module.exports={ odd: odd, even:even }으로 입력
    odd,
    even,
};
```

위 코드의 모듈 선언과 동일한 의미로 아래와 같이 작성할 수 있다.

```javascript
// 위 코드와 동일한 의미로 아래와 같이 쓸 수도 있다.
exports.odd = odd;
exports.even = even;
```

`module.exports === exports` . 

exports는 **객체 속성만** 담을 수 있다. 그러므로 아래 코드에서 `module.exports = checkOddEven;` 는 위 코드처럼 `exports.checkOddEven = checkOddEven` 으로 바꿀 수 없다.





 `var.js` 에 있는 변수 odd와 even을 `require` 를 통해서 불러온다. 변수로 불러들이게 되면 문제가 발생했을 때 역추적이 용이하다.

```javascript
// func.js
const { odd, even } = require('./var.js');  // var.js 에 있는 변수 odd와 even을 불러온다.

console.log(odd);
console.log(even);

function checkOddEven(num) {
    if (num % 2) {
        return odd;
    }
    return even;
}

module.exports = checkOddEven;
```

위 코드처럼 비구조화 할당을 하지 않게 되면 아래처럼 통째로 불러들인 후 매개변수를 통해서 읽어들어야 한다.

```javascript
const variable = require('./var.js');

console.log(variable.odd);
console.log(variable.even);
```



아래 코드는 `var.js` 변수와 `fund.js` 의 checkNumber를 모두 가져왔다.

```javascript
// index.js
const { odd, even } = require('./var.js');
const checkNumber = require('./func.js');

function checkStringOddEven(str) {
    if (str.length % 2) {
        return odd;
    }
    return even;
}

console.log(checkNumber(10));
console.log(checkStringOddEven('hello'));
```







# 3.2 global 객체

## 브라우저의 내장 객체

Node의 전역 객체는 `global` 이다. (window 아님. 최신 브라우저는 node와 통일하기 위해 global이 반영 됨.)

(global은 사용하지 않는 것이 가장 좋다. 프로그래밍에서 리스크가 매우 크다.)

```javascript
// globalA.js
module.exports = () => global.message;
```

```javascript
// globalB.js
const A = require('./globalA,js')
global.message = '안녕하세요'

console.log(A());    // 안녕하세요
```







# 3.3 console 객체

```javascript
> console
console {debug: ƒ, error: ƒ, info: ƒ, log: ƒ, warn: ƒ, …}
assert:ƒ assert()
clear:ƒ clear()
context:ƒ context()
count:ƒ count()
debug:ƒ debug()
dir:ƒ dir()
dirxml:ƒ dirxml()
error:ƒ error()
group:ƒ group()
groupCollapsed:ƒ groupCollapsed()
groupEnd:ƒ groupEnd()
info:ƒ info()
log:ƒ log()
markTimeline:ƒ markTimeline()
memory:(...)
profile:ƒ profile()
profileEnd:ƒ profileEnd()
table:ƒ table()
time:ƒ time()
...
```



### Example

* `console.time()`

```javascript
console.time('전체시간');

console.log('a');
console.log('b');

console.time('시간측정');
for(let i = 0; i < 100000; i++){
    continue;
}
console.timeEnd('시간측정');

console.timeEnd('전체시간');
```

`console.time('인자')`, `console.timeEnd(인자)` 에서 인자가 같아야 그 사이의 시간을 측정한다.



* `console.dir()` : 객체 전용 로그

```javascript
const obj = {
    outside: {
        inside: {
            key: 'value',
        },
    },
};


console.dir(obj, {color: false, depth:2});
console.dir(obj, {color: true, depth:1});
```



* `console.trace()` : 호출되는 경로를 추적해준다.

```javascript
function b(){
    console.trace('에러 위치 추적');
}
function a(){
    b();
}
a();
```







# 3.4 타이머 : setTimeout, setInterval, setImmediate

### setTimeout, setInterval

```javascript
const timeout = setTimeout(() => {
    console.log('1.5초 후 실행');
}, 1500);

const interval = setInverval(() => {
    console.log('1초마다 실행');
}, 1000);

const timeout2 = setTimeout(() => {
    console.log('실행되지 않습니다.');
}, 3000);

setTimeout(() => {
    clearTimeout(timeout2);
    clearInterval(interval);
}, 2500);
```



```javascript
clearTimeout(timeout); // ex) 비밀번호 맞추면 타이머 해제
clearInterval(interval); 
```



### setImmediate()

Node에는 setImmediate도 있다. 안에 들어 있는 함수를 이벤트루프로 보내줘서 비동기로 실행순서가 달라질 수 있어서 setImmediate를 사용한다. 즉, 바로 이벤트루프로 보내고 싶을 때 사용한다.

```javascript
cost im = setImmediate(() => console.log('즉시 실행'));
clearImmediate(im);
```





# 3.5 ______filename, __dirname, process

## ______filename, __dirname

* `__filename` : 현재 파일경로
* `__dirname` : 현재 파일이 들어 있는 경로

```javascript
console.log(__filename);   // /Users/gouda/dev/JavaScript/exercise/test1.js
console.log(__dirname);    // /Users/gouda/dev/JavaScript/exercise 
```

node는 브라우저 바깥에서 작동되므로 위 코드로 파일이 어디에서 실행되고 있는지 알 수 있다.



## process

`global.process` = `process`

스레드보다 좀더 큰 개념이 process. 

하나의 프로그램이라고 생각해도 무방.

현재 노드가 실행하고 있는 JS 프로그램에 대한 정보들이 process에 담겨 있는 것이다.



```shell
> proecess.version    # node version
> process.arch        # bit
> process.platform    # mac, windows 등 platform 정보
> process.pid         # process id
> process.uptime()    # node 프로그램이 실행된지 얼마나 지났는지 알려줌
> process.cwd()       # node를 어디에서 실행했는지
> process.execPath    # node가 설치된 경로
> process.cpuUsage()  # 현재 CPU 사용량
> process.exit()      # process 종료
```







# 3.6 OS 모듈

OS 모듈은 내장 모듈. 운영체제와 관련된 모듈.

```javascript
require('os')
const os = require('os');
os.arch()
os.type()
os.uptime()
os.hostname()
os.release()
os.homedir()
os.tmpdir()
os.freemem()   // 추가로 사용 가능한 메모리
os.totalmem()  // 전체 사용 가능한 메모리
os.cpus()      // cpu 정보 알려줌
```





# 3.7 path 💡

매우 빈번하게 쓰이고 중요.

```javascript
const path = require('path');

path.sep         // 경로 구분자
path.deilimiter  // 환경변수 구분자
path.dirname     // 파일에서 사용가능
path.extname     // 확장자
path.basename    // 파일명
path.parce       // 구조 분해
path.format      // parsing 했던 것을 다시 합쳐줌
path.normalize   // 경로 잘못 친 부분 수정해서 입력해줌
path.isAbsolute  // 절대경로인지 상대경로인지 알려줌
path.relative    // 첫 번째 경로에서 두번째 경로로 가는 상대 경로를 알려줌
path.join        // 조각난 경로들을 하나로 합쳐줌 
path.resolve     // join과 비교 해보기. resolve는 절대 경로 고려하고 합침
```







# 3.8 url 모듈 💡

## URL 구조

위 쪽은 기존 방식의 주소 체계 (**url.parse**)

<img src="https://raw.githubusercontent.com/lifeisgouda/img/master/programming/nodejs/url.png">

아래쪽은 WHATWGQ방식의 주소 체계(**url.URL**)



```javascript
const url = require('url');  // url 모듈을 불러옴

const URL = url.URL;
const myURL = new URL("https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23")

console.log(myURL); 

// output
URL {
  href:
   'https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23',
  origin: 'https://www.youtube.com',
  protocol: 'https:',
  username: '',
  password: '',
  host: 'www.youtube.com',
  hostname: 'www.youtube.com',
  port: '',
  pathname: '/watch',
  search:
   '?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23',
  searchParams:
   URLSearchParams {
  'v' => 'm8C37nS8zh8',
  'list' => 'PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw',
  'index' => '23' },
  hash: '' }


console.log(url.format(myURL));

// output
https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23
```



```javascript
const parsedUrl = url.parse('https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23')

console.log(parsedUrl)

// output
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'www.youtube.com',
  port: null,
  hostname: 'www.youtube.com',
  hash: null,
  search:
   '?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23',
  query:
   'v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23',
  pathname: '/watch',
  path:
   '/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23',
  href:
   'https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23' }
```



📌 기존 방식(url.parse)은 호스트가 없을 때도 쓸 수 있다. WHATWG방식(url.URL)은 search 처리가 편리하다.

```javascript
const url = require('url');  // url 모듈을 불러옴

const URL = url.URL;
const myURL = new URL("https://www.youtube.com/watch?v=m8C37nS8zh8&list=PLcqDmjxt30RsbFOspFG3EsxMwhFSnGFLw&index=23")

console.log(myURL.searchParams);

myURL.searchParams.getAll('category');
myURL.searchParams.get('list');
myURL.searachParams.has('page');

myURL.searachParams.keys();
myURL.searachParams.values();

myURL.searachParams.append('filter', 'es3');   // &filter=es3 이 주소에 추가 됨
myURL.searachParams.append('filter', 'es5');   // append는 기존에 있던 것에 추가
myURL.searachParams.getAll('filter');

myURL.searachParams.set('filter', 'es6'); // set은 기존 것을 지우고 수정
myURL.searachParams.getAll('filter');

myURL.serachParams.toString();
myURL.search = myURL.searchParams.toString();

```









# 3.9 querystring 모듈







# 3.10 crypto 단방향 암호화(해시)





# 3.11 crypto 양방향 암호화







# 3.12

# 3.13

# 3.14

# 3.15

# 3.16

# 3.17







