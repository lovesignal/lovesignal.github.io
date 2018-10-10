---
key: 20180703
title: "[React] Movie app clone coding : Loading States"
excerpt: "movie app 만들기 - API call을 timeout 기능으로 유사하게 구현"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 4-3. Loading States

우리에게 필요한 데이터가 항상 즉시 존재하는 것은 아니다. 데이터 없이 component가 로딩하고, 데이터를 위해 API를 읽어오고, API가 데이터를 주면 component state를 업데이트 한다.

`API call`을 `timeout` 기능으로 유사하게 구현해본다. 

이를 위해, `movie list` 를 `function` 으로 이동한다.

```javascript
  state = {
   // 비워짐
  }

  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [      // movie list를 여기로 이동
          {
            title: "Matrix",
            poster: "https://displate.com/displates/2016-09-30/60a3501bd3167cf9330acef43ab51ab3.jpg?w=280&h=392"
          },
          {
            title: "Full Metal Jacket",
            poster: "https://cf5.s3.souqcdn.com/item/2016/05/17/10/74/99/15/item_XL_10749915_14378548.jpg"
          },
          {
            title: "Oldboy",
            poster: "https://posterspy.com/wp-content/uploads/2016/02/Oldboy-by-Clay-Disarray-oct.jpg"
          },
          {
            title: "Start Wars",
            poster: "http://aidanmoher.com/blog/wp-content/uploads/2011/01/Olly-Moss-Star-Wars.jpeg"
          },
          {
            title: "Trainspotting",
            poster: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXZIzbi2UWobCwSZbNtYjdUNvyhhvTt4I9_-7Gf06ZXHdm0trT"
          }
        ]
      })
    }, 5000)       // 1000 = 1초
  }
```

<br>

`{this.state.movies.map((movie, index)` 에서 `map` 을 실행하려는데 `states.movies` 가 사라졌으므로 에러가 발생한다. 아래와 같이 수정해준다.

```javascript
// App.js
 ...
   render() {
    return (
      <div className="App">
        Loading       // 수정
      </div>
    );
  }
  ...
```

<br>

영화가 `state` 에 없을 때는 ` Loading` 을 띄우거나 `영화 리스트` 가 보이게 만든다.

영화 리스트를 불러올 function을 만든다. 아래와 같이 작성한다.

```javascript
// App.js
    ...
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

    ...
```

<br>

위 코드를 살펴보면 `movies` 라는 `variable` 에 데이터를 저장한다. : `const movies =` 

데이터가 없을 때 `loading` 을 띄우고 있으면 영화정보가 보이게 한다. : `{this.state.movies ? this._renderMovies() : 'Loading'}`

`_renderMovies()` 에서 underscore `_` 를 쓰는 이유는 리액트는 자체 기능이 많기 때문에 리액트 자체 기능과 개발자가 만든 기능에 차이를 두기 위해서이다. 

<br>

<br>

<br>

## 정리

찾고 있는 데이터가 있는지 체크하고 자바스크립트에 물어본 후 true이면 영화 정보를 출력하고, 없으면 loading을 출력한다.

`render movies` 라는 기능을 실행할 때, 위와 같은 `variables` 를 출력할 것이다.

해당 `variables` 에는 `mapping` 을 통해서 제목, 포스터가 보이게 된다. 

`movies` 를 출력할 때 정렬된 항목(`array`) 를 보여주는 것이다.

<br>

<br>

<br>

## 전체 코드

### App.js

```javascript
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {

  state = {

  }

  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          {
            title: "Matrix",
            poster: "https://displate.com/displates/2016-09-30/60a3501bd3167cf9330acef43ab51ab3.jpg?w=280&h=392"
          },
          {
            title: "Full Metal Jacket",
            poster: "https://cf5.s3.souqcdn.com/item/2016/05/17/10/74/99/15/item_XL_10749915_14378548.jpg"
          },
          {
            title: "Oldboy",
            poster: "https://posterspy.com/wp-content/uploads/2016/02/Oldboy-by-Clay-Disarray-oct.jpg"
          },
          {
            title: "Start Wars",
            poster: "http://aidanmoher.com/blog/wp-content/uploads/2011/01/Olly-Moss-Star-Wars.jpeg"
          },
          {
            title: "Trainspotting",
            poster: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXZIzbi2UWobCwSZbNtYjdUNvyhhvTt4I9_-7Gf06ZXHdm0trT"
          }
        ]
      })
    }, 1000)       // 1000 = 1초
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

