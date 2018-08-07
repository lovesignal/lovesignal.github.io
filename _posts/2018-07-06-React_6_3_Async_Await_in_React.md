---
layout: post
date: 2018-07-06
title: "[React] Movie app clone coding : Async Await in React"
excerpt: "movie app 만들기 - Async Await 기능 및 적용"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
comments: true
---



# 6-3. Async Await in React

## Async, Await

```javascript
componentDidMount(){
  fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
  .then(response => response.json())
  .then(json => console.log)
  .catch(err => console.log('error'))
}
```

`Async` 와 `Await` 는 위 코드들을 좀더 분명하게 작성해주는 도구이다.  

<br>

영화들을 state에 올리려면 아래와 같은 작업을 해야 한다.  하지만 세련되지 않고, 어플리케니션으 크면 then 안에 then으로 이어지면서 `callback hell` 에 빠지게 된다.  그래서 `Async` , `Await` 를 쓸 것이다. 

```javascript
.then(json =>{
    this.setState({
        movies: json.data.movies
    })
    .then(() => .then())    // ... callback hell
})
```

<br>

<br>

## Async, Await 적용

먼저 새로운 function을 두개 만든다.

```javascript
// App.js
_getMovies = () => {}
_callApi = () => {}
```

<br>

큰 사이즈의 `componentDidMount` 를 갖고 싶지 않으므로, 안에 있던 내용을 ` _callAPI` 로 옮기고, `this._getMovies()` 를 작성한다. 작은 function들이 각기 다른 곳에 있는 것이 좋다. 

```javascript
// App.js
componentDidMount(){
  this._getMovies();    // 큰 사이즈의 componentDidMount를 갖고 싶지 않으므로
}

_getMovies = () => {

}

_callApi = () => {
  fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
  .then(response => response.json())
  .then(json => console.log)
  .catch(err => console.log('error'))
}
```

<br>

그다음 `async` 라는 것을 한다. (`asynchronous` )

```javascript
_getMovies = async() => {}
```

<br>

이 안에 `await` 라는 것을 작성한다.

```javascript
_getMovies = async() => {
  const movies = await this._callApi()
}
```

`didMount` 하고 나면, `get movies` 를 한다. 그리고 이것은 `asynchronous function` 인데 `movie` 라는 `variable` 을 갖고 있는 것이다. 그리고 `movie` 는  `callApi` 라는 function을 `await` 모드에서 `value` 를 갖고 있다. 

<br>

```javascript
_getMovies = async() => {
  const movies = await this._callApi()
  this.setState({
    movies
  })
}
```

`await` 하는 것은  `callApi` 기능이 끝나는 것을 기다리고(성공적인 수행이 아니라 끝나는 것을 기다린다), `callApi` 의 `return value` 가 무어이든 그 `value` 를 `movies` 에 넣는다.

<br>

다시 정리하면, `callApit` 의 `return value` 를 `movies` 에 `set` 한다. 그리고 해당 컴포넌트의 `setState` 를 `movies` 로 할 것이다. 이것은 `this._callApi` 의 `return value` 이다. 

 <u>`this.setState({ movies })` 부분은 `setstate` 는 `callApi` 작업이 **완료되기 전까지** 실행되지 않는다.</u> 

`callApi` 작업이 완료된 후에 `  this.setState({ movies })` 가 실행된다. 이를 하는 방법은 아래 코드와 같다.

`fetch` 라는 이름의 `promise` 를 return 한다.

```javascript
_callApi = () => {
  return fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response => response.json())
    .then(json => json.data.movies)
    .catch(err => console.log('error'))
}
```

<br>

`movie object` 가 변경되었으므로 `_renderMovies` 의 코드를 아래와 같이 수정해준다.

```javascript
_renderMovies = () => {
  const movies = this.state.movies.map((movie, index) => {
    return <Movie title={movie.title} poster={movie.large_cover_image} key={movie.id} />       
    // poster = movie.large_cover_image, key = movie.id 로 수정
  })
  return movies
}
```

component의 key는 느리기 때문에 인덱스를 사용하는 것은 좋지않다. 그러므로 `key` 로 `movie.id` 를 사용한다.

<br>

<br>

<br>

## 정리

1. `fetch` 를 `callApi` 로 변경
2. `getMovies` 라는 asynchronous function 작성
3. 그 안에 `movies` 라는 `const variable` 생성
4. `callApi` 작업이 완료되고 return 하는 것을 `await` 함
5. `callApi` 는 `fetch promise` 를 return하는데, 데이터는 Json
6. 그러므로 `json.data.movies` 라는 value는 `const movies` 의 결괏값이 되는 것
7. 그리고 component의 `state` 를 `movies` 로 `set` 한 것
8. `state` 안에 `movies` 가 있으면 `render movies` 라는 fucntion 을 불러옴
9. `render movies` 는 `movies` 라는 const를 불러오는데 이는 타이틀, 포스터 순으로 맵핑 함

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
    this._getMovies();    // 큰 사이즈의 componentDidMount를 갖고 싶지 않으므로
  }

  _renderMovies = () => {
    const movies = this.state.movies.map((movie, index) => {
      return <Movie title={movie.title} poster={movie.large_cover_image} key={movie.id} />
    })
    return movies
  }

  _getMovies = async() => {
    const movies = await this._callApi()
    this.setState({
      movies
    })
  }


  _callApi = () => {
    return fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
    .then(response => response.json())
    .then(json => json.data.movies)
    .catch(err => console.log('error'))
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

