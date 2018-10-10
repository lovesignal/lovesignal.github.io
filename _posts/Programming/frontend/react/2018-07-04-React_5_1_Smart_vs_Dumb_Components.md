---
key: 20180704
title: "[React] Movie app clone coding : Smart vs Dumb Components"
excerpt: "movie app 만들기 - Smart vs Dumb Components"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 5-1. Smart vs Dumb Components

<br>

## State 존재 여부에 따른 Component 분류

모든 컴포넌트가 state가 있는 것은 아니다. 어떤 component는 state가 없는 `stateless functional component` 이다. 

두 가지 component를 아래와 같이 분류할 수 있다.

* `smart component`  : state가 있는 component
* `dump component` : state가 없고, 필요하지도 않은 component. `props` 만 갖고 있다.

<br>

state는 없고 props 밖에 없을 때는 `class component` (ex : `class App extends Component{...}` ) 를 쓰는 대신에   `stateless functional component` 로 바꾸면 된다.  

<br>

예를들어, `class MoviePoster extends Component{...}` 를 쓰는 대신 아래와 같이 작성한다.

```javascript
// Movie.js
function MoviePoster({poster}) {
    return(
    	<img src={this.props.poster} alt="Movie Poster" />
    )
}


/*
위에 작성한 component와 아래 작생한 component는 같은 것이다.
둘다 image와 props를 return 한다.

class MoviePoster extends Component{

  static propTypes = {
    poster: PropTypes.string.isRequired    
  }

  render(){
    return(
      <img src={this.props.poster} />
    )
  }
}
*/
```

<br>

<br>

어떤 component는 단순히 return을 하기 위해 존재한다. 위에서 작성한 `function component` 는 `componentDidMount`, `function`, `update state` 등이 필요 없다.  `poster` 과 같은 한 개의  `props` 만 있으면 된다. 

이렇게 하면 이전보다 적은 양의 코드를 사용할 수 있다.

<br>

<br>

`movie component` 도 functional로 변경하면 아래와 같다.

```javascript
// Movie.js
function Movie({title, poster}){
  return(
    <div>
      <MoviePoster poster={poster} />
      <h1>{title}</h1>
    </div>
  )
}
```

<br>

<br>

## Props type 확인하기

```javascript
Movie.PropTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired

}

MoviePoster.PropTypes = {
  poster: PropTypes.string.isRequired
}
```

<br><br>

<br>

## 전체 코드

```javascript
// Movie.js
import React from 'react';
import PropTypes from 'prop-types';
import './Movie.css';

function Movie({title, poster}){
  return(
    <div>
      <MoviePoster poster={poster} />
      <h1>{title}</h1>
    </div>
  )
}

function MoviePoster({poster}) {
  return(
    <img src={poster} alt="Movie Poster" />
  )
}

Movie.PropTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired

}

MoviePoster.PropTypes = {
  poster: PropTypes.string.isRequired
}

export default Movie;
```



