---
layout: post
date: 2018-07-03
title: "[React] Movie app clone coding : Practicing this.setState"
excerpt: "movie app 만들기 - this.setState() 실습"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
comments: true
---



# 4-2. Practicing this.setState()

<br>

* this.setState() documentation :

  https://reactjs.org/docs/react-component.html#setstate

<br>

<br>

`App.js` 의 Component 외부에 있는 movie list `const movies = [...]` 를 아래와 같이 수정하여 state( `class App extends Component {...}` ) 안으로 옮긴다. 그런데 아래와 같이 넣으면 component movies를 찾을 수 없으므로 에러가 발생한다.

```javascript
// App.js
class App extends Component {

  state = {
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
      }
    ]
  }

  render() {
    return (
      <div className="App">
        {movies.map((movie, index) => {
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}

```

<br>

그러므로 `{movies.map((movie, index) => {...` 에 `this.state.` 를 앞에 붙여준다.

```javascript
// App.js
    ...
  render() {
    return (
      <div className="App">
        {this.state.movies.map((movie, index) => {
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
```

<br>

여기에 movie list에서 영화를 한개 더 추가하고 싶으면 아래와 같이 작성한다.

```javascript
// App.js
    ...
class App extends Component {

  state = {
    movies: [
        ...
    ]
  }

  // 아래 componentDidMount 부분을 추가 작성
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          ...this.state.movies,
          {
            title: "Trainspotting",
            poster: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXZIzbi2UWobCwSZbNtYjdUNvyhhvTt4I9_-7Gf06ZXHdm0trT"
          }
        ]
      })
    }, 1000)       // 1000 = 1초
  }

  render() {
    ....
}
```

<br>

<br>

### componentDidMount

```javascript
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          ...this.state.movies,
          {
            title: "Trainspotting",
            poster: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXZIzbi2UWobCwSZbNtYjdUNvyhhvTt4I9_-7Gf06ZXHdm0trT"
          }
        ]
      })
    }, 1000)       // 1000 = 1초
  }
```

<br>

`componentDidMount()` 를 살펴보면, `component` 가 `mount` 하면 페이지 로드 후 1초에 새로운 영화가 보여진다. ( `timeout` 은 작성한 일정 시간 후에 작업을 수행할 때 사용한다.) movie list에 영화를 추가하는 것이다. 

여기서 만약 `...this.state.movies,` 부분을 삭제하게 되면 모든 영화가 사라지고 마지막에 추가한 영화(Trainspotting)만 남는다. 전체 movie list를 대체해버리는 것이다. `...this.state.movies` 가 명령하는 것은 `setState` State를 그대로 두고, 영화를 추가하라는 의미이다.  

만약 `...this.state.movies,` 를 아래와 같이 `movies: [ {}` 다음에 입력하게 되면 리스트가 맨 위에 추가되게 된다.

```javascript
  componentDidMount(){
    setTimeout(() => {
      this.setState({
        movies: [
          {
            title: "Trainspotting",
            poster: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTXZIzbi2UWobCwSZbNtYjdUNvyhhvTt4I9_-7Gf06ZXHdm0trT"
          },
          ...this.state.movies   // 여기에 추가
        ]
      })
    }, 1000)     
  }
```



이와같이 `state` 를 응용해서 다양하게 사용할 수 있다. 예를들어 `infinite scroll` 같은 페이지 로딩할 때 스크롤을 아래로 내릴 수록 더 많은 영화가 로딩되는 효과 등을 구현할 수 있다 (페이스푹, 인스타그램 같은 로딩 방식).

