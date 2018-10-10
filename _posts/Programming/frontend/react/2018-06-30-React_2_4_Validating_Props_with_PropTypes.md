---
key: 20180630
title: "[React] Movie app clone coding : Validating Props with PropTypes"
excerpt: "movie app 만들기 - PropTypes 이용하여 받아오는 정보 체크하기"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---





# 2-4. Validating Props with PropTypes

<br>

## Install Props

**Install Prop-Types with npm:**

```
 npm install --save prop-types 
```

**Install Prop-Types with Yarn:**

```
 yarn add prop-types 
```

<br>

<br>

<br>

## key prop

Console log를 살펴보면 아래와 같은 에러 메시지를 확인할 수 있다.

<br>

>  Warning: Each child in an array or iterator should have a unique "key" prop.
>
> 경고 : array 또는 interator 안의 각각의 child는 반드시 고유한 key prop을 가져야 한다.

<br>

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/console_error.png">

<br>

앞서 작업한 `mapping` 은 새로운 array를 만든다. 이 의미는 array 안에 많은 영화정보를 담게 된다는 것이다. 그런데 <u>react는 `element` 가 많을 경우 **고유한 `key` **를 부여해야 한다.</u> 

<br>

map 기능을 실행해서 1개의 argument "movie"를 얻게 되어 있다. `movies.map(movie => …` 에서 movie는 현 사이클의 현재 element를 의미한다. 그 외에 다른 것은 `index` 라고 정한다. `index` 는 현재 제공하는 리스트의 숫자를 의미한다. 그러므로 `key prop` 으로 `index` 를 넣는다.

```javascript
// App.js
    ...
    {movies.map((movie, index) => {
      return <Movie title={movie.title} poster={movie.poster} key={index} />
    })}
    ...
```

<br>

<br>

<br>

## PropTypes

props에 원하는 값을 출력하고 싶을 때는 어떻게 해야 할까?

예를들어, 영화 제목에 숫자만 출력되는 것을 원하지 않는다면 또는 포스터에 출력되는 값이 숫자나 boolean 같은 값이 되는 걸 원하지 않을 경우.

이것을 확인하는 방법은 상단에  `static propTypes` 라고 작성하고, 2가지 type (title, poster)를 원한다고 쓴다. 

먼저 `import PropTypes from 'prop-types';` 으로 `PropTypes` 를 import 한다.

`title` 과 `poster`  모두  `react.propTypes.number` 으로 작성한다. 에러메시지를 발생시키기 위해 일부러 `string` 이 아닌 `number` 로 적는다.

```javascript
// Movie.js
import PropTypes from 'prop-types';
    ...
class Movie extends Component {

    static propTypes = {
        title: PropTypes.number,
        poster: PropTypes.number
    }
    
    render() {
    ...
  }
}
```

이렇게 작성하면 title, poster는 number 라는 의미가 된다.

콘솔창에서 아래와 같은 메시지를 확인할 수 있다.

> index.js:2178 Warning: Failed prop type: Invalid prop `title` of type `string` supplied to `Movie`, expected `number`.
>     in Movie (at App.js:30)
>     in App (at index.js:7)

얻게 되는 정보가 숫자가 아니라는 것을 확인할 수 있다. 만약 부모 컴포넌트가 string을 보내면, PropTypes로 string이라는 것을 체크할 수 있다. 

<br>

또한 이것이 필수 required 인지 아닌지 알 수 있다. 예를들어, `title: PropTypes.string.isRequired` 라고 작성하면 movie component 는 title이라는 prop 을 제공하는 것이 필수로 설정되는 것이다.

<br>

📌 **정리하면, 이 기능으로 부모 컴포넌트에서 얻은 정보의 종류가 무엇인지 또는 있는지 없는지 알 수 있다. 즉, 부모 컴포넌트에게 받는 정보를 체크할 수 있다.** API를 통해 정보를 불러온다면, user 이름은 string이 필수요건이 되는 것이다.

<br>

<br>

<br>

## 전체코드

### Movie.js

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import './Movie.css';

class Movie extends Component {

  static propTypes = {
    title: PropTypes.string.isRequired,    // isRequired 체크
    poster: PropTypes.string.isRequired
  }

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

  static propTypes = {
    poster: PropTypes.string.isRequired    // MoviePoster라는 부모 컴포넌트에게 받는 정보를 체크. 
                                           // 이미지를 반드시 보여줘야 하므로
  }

  render(){
    return(
      <img src={this.props.poster} />
    )
  }
}

export default Movie;
```

