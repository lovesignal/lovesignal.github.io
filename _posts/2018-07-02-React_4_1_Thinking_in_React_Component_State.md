---
layout: post
date: 2018-07-02
title: "[React] Movie app clone coding : Component State"
excerpt: "movie app 만들기 - Component State의 이해"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
comments: true
---



# 4-1. Thinking in React: Component State

* setTimeout documentation : https://www.w3schools.com/jsref/met_win_settimeout.asp

<br>

## State

`State` 는 react component 안에 있는 object 이다.

`state` 가 바뀔 때마다, `component` 는 다시 `render` 한다. 즉, `component` 안에 `state` 가 바뀔 때마다 `render` 가 발생한다.

```javascript
class App extends Component {    // (1) component 안에 state가 바뀔 때마다
  render() {                     // (2) render() 가 발생
   ... 
  }
}

```

<br>

<br>

### state를 만드는 방법

```javascript
class App extends Component {    
  state = {                  // State 작성
      greeting : 'Hello!'
  }

/* component가 mount 되면 5초를 기다리고 greeting을 업데이트한다. 
 * 아래 코드는 component가 mount할 때마다, 
 * greeting을 'hello' → 'hello again' 으로 변경한다는 의미이다.
 * 아래의 render가 다시 작동해서 5초 후에 'hello again'으로 변경이 된다.
 */

  componentDidMount() {
      setTimeout(() => {
          this.setState({   // 새로운 state를 만든다.
              greeting: 'Hello again!'
          })
      }, 5000)
  }

/* 아래의 render가 5초후 다시 작동되면 hello again으로 변경*/
  render() {
    return (
      <div className="App">
        {this.state.greeting}    // render에서 읽어들임
        {movies.map((movie, index) => {
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}
```

<br>

`state ={ greeting : 'Hello!' }` 는 component 를 default state와 함께 load 하는 방법이고, component가 `componentDidMount() {setTimeout(() => ...)}` 한 후에는  5초 후에 'Hello again!' 이 되도록 입력했다.

<br>

* **주의** 💡

  아래와 같이 작성하여 greeting을 업데이트 하지는 않는다.  `this.state.greeting` 처럼 state를 직접적으로 쓰면 안된다. 직접적으로 변경하면 render 설정들이  작동하지 않는다. `this.setState`를 사용해야 한다.  

```javascript
 componentDidMount() {
      setTimeout(() => {
        this.state.greeting = 'something'
      }, 5000)
  }
```

<br>

<br>

## 정리

`state` 를 바꿀 때는 `setState` 를 설정하고 업데이트할 때마다 새로운 `state`와 함께 `render` 가 작동한다.

