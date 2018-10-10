---
key: 20180709
title: "[React] Movie app clone coding : Updating Component"
excerpt: "movie app 만들기 - Updating Component"
categories: programming
tags: [clonecoding, react, javascript, jsx]
comments: true
---



# 7-1. Updating Component

## 정보확인 및 업데이트

요소 검사를 통해서 movie DB에서 어떤 종류의 정보를 받고 있는지 파악한다.

```javascript
// App.js
_renderMovies = () => {
  const movies = this.state.movies.map((movie, index) => {
    console.log(movie)     // 정보를 프린트
   ...
}
```

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/movie_console.png">

<br>

Console에 받아오는 정보가 출력된 것을 확인할 수 있다. 받아오는 정보 중에 포스터, 제목, 장르, 평점, 설명 등이 필요하다.

* 제목 :  `title-english`
* 포스터 : `small_cover_image`
* 장르 : `genres`
* 평점 : `rating`
* 설명 : `synopsis`

<br>

받아오는 정보를 아래와 같이 수정한다. 

```javascript
// App.js
_renderMovies = () => {
  const movies = this.state.movies.map((movie, index) => {
    console.log(movie)
    return <Movie 
      title={movie.title_english} 
      poster={movie.medium_cover_image} 
      key={movie.id} 
      genres={movie.genres}
      synopsis={movie.synopsis} 
    />
  })
  return movies
}
```

<br>

Movie component에 props를 업데이트 한다.

```javascript
// Movie.js
Movie.propTypes = {
  title: propTypes.string.isRequired,
  poster: propTypes.string.isRequired,
  genres: propTypes.array.isRequired,
  synopsis: propTypes.string.isRequired
}
```

<br>

<br>

<br>

## HTML 꾸미기

```javascript
// Movie.js
import React from 'react';
import propTypes from 'prop-types';
import './Movie.css';

function Movie({title, poster, genres, synopsis}){
  return(
    <div className="Movie">
      <div className="Movie__Columns">
        <MoviePoster poster={poster} alt={title} />  
      </div>
      <div className="Movie__Columns">
        <h1>{title}</h1>
        <div className="Movie__Genres">
          {genres.map((genre, index) => <MovieGenre genre={genre} key={index} />)}
        </div>
        <p className="Movie__Synopsis">
          {synopsis}
        </p>

      </div>
    </div>
  )
}

function MoviePoster({poster, alt}) {
  return(
    <img src={poster} alt={alt} title={alt} className="Movie__Poster" />
  )
}


function MovieGenre({genre}){
  return(
    <span className="Movie__Genre">{genre}</span>
  )
}


Movie.propTypes = {
  title: propTypes.string.isRequired,
  poster: propTypes.string.isRequired,
  genres: propTypes.array.isRequired,
  synopsis: propTypes.string.isRequired
}

MoviePoster.propTypes = {
  poster: propTypes.string.isRequired,
  alt: propTypes.string.isRequired
}

MovieGenre.prototype ={
  genre: propTypes.string.isRequired
}

export default Movie;
```

<br>

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
      return <Movie 
        title={movie.title_english} 
        poster={movie.medium_cover_image} 
        key={movie.id} 
        genres={movie.genres}
        synopsis={movie.synopsis} 
      />
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