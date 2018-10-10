---
key: 20180629
title: "[React] Movie app clone coding : Dataflow with Props"
excerpt: "movie app 만들기 - props를 통해서 정보를 전달하기"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 2-2. Dataflow with Props

<br>

React에는 <u>**state** 와 **props** 라는  2개의 주요 컨셉</u>이 있다. 먼저 Props를 다룬다.



데이터가 어디에선가 오고, 소스가 있어야 한다.

메인 컴포넌트인 app은 모든 영화를 가져온다. 그리고 영화가 카드 형태로 보여지게 된다.

그러므로 메인컴포넌트는 무비 리스트를 가지고 있다. `main component > movie list`

리스트 안의 무비 카드에는 해당 영화의 정보가 각각 담긴다. `movie card > movie info `

즉, 부모 컴포넌트는 칠드런 컴포넌트에게 각각 정보를 준다. 이때 **props를 통해서 정보를 전달**하게 된다.

<br>

## 제목 리스트 만들기

예를들어, app.js에 아래와 같은 영화 제목 데이터가 있다고 하자.

```javascript
// App.js
import .....

const movieTitles = [
  "Matrix",
  "Full Metal Jacket",
  "Oldboy",
  "Start Wars"
]

    ....
```

이 영화의 '제목'을 칠드런 컴포넌트인 movie컴포넌트에 보내고 싶으면, 아래와 같이 작성하면 된다. 

movie 컴포넌트는 '제목'이라는 데이터를 얻게 된다. 

```javascript
// App.js
	....
class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={movieTitles[0]}/>
        <Movie title={movieTitles[1]}/>
        <Movie title={movieTitles[2]}/>
        <Movie title={movieTitles[3]}/>
      </div>
    );
  }
}
	....
```

<br>

Movie.js에서 movie 컴포넌트로 가보면, render 아래에 다음과 같이 작성한다.

```javascript
// Movie.js
import React, { Component } from 'react';
import './Movie.css';

class Movie extends Component {
  render() {
    console.log(this.props);     // 이 부분을 작성
    return ( ......
}
```

<br>

크롬에서 요소검사를 보면, Console에서 제목을 확인할 수 있다.

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/props-console_log.png" />

<br>

위 console 내용을 보면 제목을 데이터고 갖고, 각각 영화에 다른 제목을 부여했다. 그리고 각각 영화의 props (`console.log(this.props)`)는 Matrix, Oldboy, … 등등 이다.

<br>

**전달받은 요소를 액세스** 하려면,

아래와 같이 어떤 `object(props)` 가 있으면, 괄호를 한번 치고`this.props."title"` 이라고 쓰면 된다. 그러면 각 제목이 데이터를 전달받아 바뀌어 있는 것을 볼 수 있다. JSX의 경우 명령을 실행시키려면 반드시 `{ }`괄호를 쳐야 한다.

```javascript
// Movie.js
    ...
class Movie extends Component {
  render() {
	...
          <MoviePoster />
          <h1>{this.props.title}</h1>     // this.props."title"
      </div>
    )
  }
}
```

이 경우는 `movie > title` 이 있고, **`Movie.js` 에서 title을 props로 불러오는 것**이다. 왜냐하면 <u>movie 컴포넌트는 title이라는 요소가 있기 때문</u>이다. 

<br>

<br>

## 이미지 리스트 만들기

App.js 에 `movieImages` 데이터 생성

```javascript
// App.js
import React, { Component } from 'react';

	...

const movieImages = [
  "https://displate.com/displates/2016-09-30/60a3501bd3167cf9330acef43ab51ab3.jpg?w=280&h=392",

  "https://cf5.s3.souqcdn.com/item/2016/05/17/10/74/99/15/item_XL_10749915_14378548.jpg",
  
  "https://posterspy.com/wp-content/uploads/2016/02/Oldboy-by-Clay-Disarray-oct.jpg",
  
  "http://aidanmoher.com/blog/wp-content/uploads/2011/01/Olly-Moss-Star-Wars.jpeg"
]

	...
```

<br>

`Movie title` 에 `Poster` 를 읽어들이고  `Movie image(number)` 를 입력한다.

```javascript
// App.js
	...

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={movieTitles[0]} poster={movieImages[0]} />
        <Movie title={movieTitles[1]} poster={movieImages[1]} />
        <Movie title={movieTitles[2]} poster={movieImages[2]} />
        <Movie title={movieTitles[3]} poster={movieImages[3]} />
      </div>
    );
  }
}
    ...
```

```javascript
// Movie.js
	...
class Movie extends Component {
  render() {
    console.log(this.props);     // Movie 컴포넌트에 console
    return (
      <div>
          <MoviePoster poster={this.props.poster} />   // 전달받은 요소 엑세스
          <h1>{this.props.title}</h1>
      </div>
    )
  }
}
    
class MoviePoster extends Component{
  render(){
    return(
      <img src={this.props.poster} />   // 전달받은 요소 엑세스
    )
  }
}
    ...
```

<br>

📎 데이터를 갖고 있는 것은 메인 컴포넌트 한 곳 뿐이다. 한개의 데이터 소스를 가지고 각 컴포넌트별로 출력만 하면 된다.

<br><br><br>

### 전체 코드

#### App.js

```javascript
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

const movieTitles = [
  "Matrix",
  "Full Metal Jacket",
  "Oldboy",
  "Start Wars"
]

const movieImages = [
  "https://displate.com/displates/2016-09-30/60a3501bd3167cf9330acef43ab51ab3.jpg?w=280&h=392",
  "https://cf5.s3.souqcdn.com/item/2016/05/17/10/74/99/15/item_XL_10749915_14378548.jpg",
  "https://posterspy.com/wp-content/uploads/2016/02/Oldboy-by-Clay-Disarray-oct.jpg",
  "http://aidanmoher.com/blog/wp-content/uploads/2011/01/Olly-Moss-Star-Wars.jpeg"
]

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={movieTitles[0]} poster={movieImages[0]} />
        <Movie title={movieTitles[1]} poster={movieImages[1]} />
        <Movie title={movieTitles[2]} poster={movieImages[2]} />
        <Movie title={movieTitles[3]} poster={movieImages[3]} />
      </div>
    );
  }
}

export default App;
```

<br>

<br>

#### Movie.js

```javascript
import React, { Component } from 'react';
import './Movie.css';

class Movie extends Component {
  render() {
    console.log(this.props);
    return (
      <div>
          <MoviePoster poster={this.props.poster} />
          <h1>{this.props.title}</h1>
      </div>
    )
  }
}

class MoviePoster extends Component{
  render(){
    return(
      <img src={this.props.poster} />
    )
  }
}

export default Movie;
```

