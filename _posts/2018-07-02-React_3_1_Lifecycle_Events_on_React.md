---
key: 20180702
title: "[React] Movie app clone coding : Lifecycle Events on React"
excerpt: "movie app 만들기 - React의 Component Lifecycle에 대한 이해"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



## 3-1. Lifecycle Events on React

<br>

## React Component Lifecycle

* Compenent Lifecycle

  https://reactjs.org/docs/react-component.html#the-component-lifecycle

<br>

### Render

Component가 여러 기능들을 정해진 순서대로 실행하는 것을 학습한다. Render를 할 때(Componenet를 띄울 때) 아래 순서대로 하게 된다.

<br>

* **Render** : `componentWillMount()` → `render()` → `componentDidMount()`

<br>

Component가 `존재`하기 시작하면, react 안에서는 `willMount → render → DidMount()` 를 수행한다.

예를들어 영화앱을 만든다면, `wiiMount` 를 진행할 때 api에 작업을 요청한다. 해당 작업 수행이 완료되면 그 다음에 데이터 관련 작업을 한다.  

이 cycle이 중요한 이유는 component를 만드는데 도움이 되기 때문이다. `willMount` 를 보면 사이클이 시작되었음을 알 수 있고, `render` 를 보면 component가 react 내부에 존재하게 되었음을 알게되고, `didMount` 를 보면 성공적으로 react 안에 component가 자리잡았음을 알 수 있다. 

<br>

<br>

<br>

### Update

**Update** : `componentwillReceiveProps()` → `shouldComponentUpdate()` → `componentiwillUpdate()` → `render()` → `componentDidUpdate()`

<br>

* `componentwillReceiveProps()` : 컴포넌트가 새로운 proprs을 받음

* `shouldComponentUpdate()` : 리액트는 old props, new props를 살펴본 다음, 이전과 새로운 props가 다르면 `update=true` 라고 생각한다. 즉, `shouldComponentUpdate() === true` 하여 업데이트가 된다.



* `componentiwillUpdate()` : componenet가 업데이트 할거라는 단계

<br>

예를들어 `componentWillUpdate()` 를 수행할 때는 어플리케이션에 빙글빙글 도는 spinner를 붙일 수 있다. 업데이트 후에 돌고 있던 '로딩 중' 메시지나 아이콘을 숨기면 된다.

<br>

💡NOTE : Component는 많은 functions을 갖고 있고 그것들은 `자동으로` , `순서대로` 작동한다.

