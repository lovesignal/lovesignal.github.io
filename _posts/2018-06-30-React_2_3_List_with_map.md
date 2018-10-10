---
key: 20180630
title: "[React] Movie app clone coding : List with .map"
excerpt: "movie app 만들기 - map을 이용하여 새로운 array 생성하기"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 2-3. List with .map

<br>

앞서 리스트를 만든 방법은 효율성이 떨어지므로 갖고 있는 영화 정보의 양에 관계없이 이를 토대로 리스트를 만든다. 

API에서 가져온 영화 정보를 불러올 때 `Array` 를 만든다.

<br>

리스트에는 여러 object가 있다. (ex)  `title`, `poster`

아래와 같이 영화정보를 array로 만들 수 있다.

```javascript
// App.js
	...
const movies = [
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
	...
```



<br>

이제 정렬된 array를 보면서 최종 리스트를 만든다.

`array` 는 `map` 이라는 기능이 있다. <u>`map` 은 사용자가 제공한 기능/명령의 결과값을 array로 만든다.</u> 

*참고 : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map

`movies` 는 `array` 이다. 그 다음 `map` 기능을 통해 새로운 `array` 를 만든다. 

```javascript
// App.js
    ...
class App extends Component {
    ...
    return (
      <div className="App">
        {movies.map(movie => {
          return <Movie title={movie.title} poster={movie.poster} />
        })}
      </div>
    ...
}
    ...
```

정리하면, 이 작업은 `movies` array를 가져다가 해당 `movies array` 안의 element를 활용해서  `mapping` 해서 새로운 `component` 를 만드는 것이다. 해당 `array` 의 `element` 를 토대로 한  `component` 인 것이다.  

💡movies array를 활용한다는 것이 포인트.

<br>

<br>

## map() syntax

```javascript
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
    // Return element for new_array
}[, thisArg])
```

`currentValue` 값에 들어가는 것이 `movies` array 이다.

<br>

map으로 작업한 것을 코드로 표현해보면 아래와 같다. 즉, 아래 두 코드는 같은 결과의 코드이다.

```javascript
// mapping
{movies.map(movie => {
    return <Movie title={movie.title} poster={movie.poster} />
})}
```

<br>

```javascript
// 위 코드를 풀어서 표현
{[
    <Movie title={movies[0].title} poster={movies[0].poster} />
    <Movie title={movies[1].title} poster={movies[1].poster} />
    <Movie title={movies[2].title} poster={movies[2].poster} />
    <Movie title={movies[3].title} poster={movies[3].poster} />
]}
```

<br>

<br>

## 전체코드

```javascript
// App.js
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

const movies = [
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

class App extends Component {
  render() {
    return (
      <div className="App">
        {movies.map(movie => {
          return <Movie title={movie.title} poster={movie.poster} />
        })}
      </div>
    );
  }
}

export default App;
```