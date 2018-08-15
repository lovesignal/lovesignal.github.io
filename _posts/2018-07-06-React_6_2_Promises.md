---
layout: post
date: 2018-07-06
title: "[React] Movie app clone coding : Promises"
excerpt: "movie app 만들기 - Promise 기능 및 적용"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
comments: true
---



# 6-2. Promises

<br>

## Promise 기능

Promise는 새로운 javascript 컨셉이다. 두가지 기능이 있는데 하나는 asynchronous programming이라는 것이고, 또다른 기능은 시나리오 잡는 방법을 알려준다는 것이다.

<br>

### asynchronous

순서대로 완료시키고 다음 넘어가는 것은 동기적인 것이라 하고, <u>하나가 완료됨과 상관없이 동시에 일을 처리하는 것을 비동기적(asynchronous)인 것</u>이라고 한다.

<br>

### scenario

`Promise` 는 두가지 시나리오가 있고, 이를 관리하는 것이 가능하다.

* 좋은 시나리오 : promise대로 작동한다.
* 나쁜 시나리오 : promise대로 작동하지 않는다.

<br>

<br>

## Promise 적용

* `.then()` :  `fetch()` 작업이 성공적 수행이 아니라 단순히 작업이 완료되면 `.then()` 을 불러온다. 

  `then()` 은 1개의 `object attribute` 만 준다(`fetch()` 의 결과물)

* `catch()` :  `fetch()` 가 에러가 나면 `catch` 해서 설명하라는 의미

```javascript
// App.js
    ...
class App extends Component {

  state = {}

  componentDidMount(){
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response => console.log(response))
    .catch(err => console.log('error'))
  }
    ...
```

<br>

Console에서 response를 살펴보면 아래 그림과 같다.

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/promise_reponse.png">

`headers` 의 ok가 `true` 이므로 request가 성공이라는 의미이다.

`redirected` 는 `false` 이므로 redirected 되지 않았고, `status` 는 200이므로 OK라는 의미이다.

`statusText` 는 `""` 이므로 없고, `url` 은 `fetch` 에 있는 것을 잘 받아왔다. 

`body` 의 `readable stream` 은 `byte` 로 이루어졌다는 의미이다. 이것을 `JSON` 으로 바꾸어야 한다.

위 내용은 `fetch` 에 어떤 결과가 나타났느냐에 대한 것이다.

<br>

<br>

### response object → JSON

아래와 같이 입력하여 byte를 JSON으로 바꾼다.

```javascript
// App.js
.then(response => response.json())
.then(json => console.log(json)) // JSON을 출력
```

Cosole 에서 아래 내용 확인 가능하다.

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/promise_reponse2.png">

<br>

<br>

## 정리

`promise` 는 작업을 성공적으로 수행하고, 그렇지 않은 경우 결과물을 `catch`, `then` 으로 받아볼 수 있다. 그리고 `then` 은 원하는 만큼 변경 가능하다. 

`fetch` 가 좋은 이유는 URL을 Ajax로 간단하게 불러올 수 있기 때문이다. 이전에는 `xml http request` 라는 것으로 했는데 아주 못생기고 어려웠다.

<br>

<br>

<br>

## 전체코드

```javascript
// App.js
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {

  state = {}

  componentDidMount(){
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response => response.json())
    .then(json => console.log(json))
    .catch(err => console.log('error'))
  }

  _renderMovies = () => {
    const movies = this.state.movies.map((movie, index) => {
      return <Movie title={movie.title} poster={movie.poster} key={index} />
    })
    return movies
  }

  render() {
    return (
      <div className="App">
        {this.state.movies ? this._renderMovies() : 'Loading'}
      </div>
    );
  }
}

export default App;
```

