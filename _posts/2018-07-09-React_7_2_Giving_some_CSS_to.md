---
layout: post
date: 2018-07-09
title: "[React] Movie app clone coding : Giving some CSS to"
excerpt: "movie app 만들기 - Giving some CSS to"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
comments: true
---



## 7-2. Giving some CSS to

<br>

* To install it run:

  ```shell
  yarn add react-lines-ellipsis
  ```

<br>

## CSS 꾸미기

### App.css

```css
.App {
    padding: 50px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    font-size: 14px;
}

.App--loading{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}
```

<br>

<br>

### App.js

```javascript
  render() {
    const {movie} = this.state;
    return (
      <div className={movie ? "App" : "App--loading"}>
        {movies ? this._renderMovies() : 'Loading'}
      </div>
    );
  }
}
```

* `<div className={movie ? "App" : "App--loading"}>`

  movies가 있으면 div의 이름은 app이 되고, movies가 없으면 app-loading이 된다.

* 그리고 각각의 css를 `App.css` 에 정했다. 



<br>

<br>

### index.css

```css
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color:#EFF3F7;
  height: 100%;
}

html, #root{
  height:100%;
}
```

<br>

<br>

### Movie.css

```css
.Movie{
    background-color:white;
    width:40%;
    display: flex;
    justify-content: space-between;
    align-items:flex-start;
    flex-wrap:wrap;
    margin-bottom:50px;
    text-overflow: ellipsis;
    padding:0 20px;
    box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3), 0 5px 12px rgba(133, 133, 133,0.22);
}

.Movie__Column{
    width:30%;
    box-sizing:border-box;
    text-overflow: ellipsis;
}

.Movie__Column:last-child{
    padding:20px 0;
    width:60%;
}

.Movie h1{
    font-size:20px;
    font-weight: 600;
}

.Movie .Movie__Genres{
    display: flex;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.Movie__Genres .Movie__Genre{
    margin-right:10px;
    color:#B4B5BD;
}

.Movie .Movie__Synopsis {
    text-overflow: ellipsis;
    color:#B4B5BD;
    overflow: hidden;
}

.Movie .Movie__Poster{
    max-width: 100%;
    position: relative;
    top:-20px;
    box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3), 10px 15px 12px rgba(80,80,80,0.22);
}

/* Mobile Phone */
@media screen and (min-width:320px) and (max-width:667px){
    .Movie{
        width:100%;
    }
}

/* Mobile-portrait */
@media screen and (min-width:320px) and (max-width:667px) and (orientation: portrait){
    .Movie{
        width:100%;
        flex-direction: column;
    }
    .Movie__Poster{
        top:0;
        left:0;
        width:100%;
    }
    .Movie__Column{
        width:100%!important;
    }
}
```

<br>

<br>

### Movie.js

```javascript
import LinesEllipsis from 'react-lines-ellipsis'
import './Movie.css';

function Movie({title, poster, genres, synopsis}){
  return(
       ...
        <p className="Movie__Synopsis">
         
      /* Synopsis를 줄여주는 역할 : 
       * npm install --save react-lines-ellipsis 
       */
          <LinesEllipsis      
            text={synopsis}
            maxLine='3'
            ellipsis='...'
            trimRight
            basedOn='letters'
          />   
        </p>
      ...
  )
}
```

<br>

<br>

<br>

## 전체코드

### App.js

```javascript
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
    const {movies} = this.state;
    return (
      <div className={movies ? "App" : "App--loading"}>
        {movies ? this._renderMovies() : 'Loading'}
      </div>
    );
  }
}

export default App;
```

<br>

### App.css

```css
.App {
    padding: 50px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    font-size: 14px;
}

.App--loading{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}
```

<br>

### Movie.js

```javascript
import React from 'react';
import propTypes from 'prop-types';
import LinesEllipsis from 'react-lines-ellipsis'
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
          <LinesEllipsis      
            text={synopsis}
            maxLine='3'
            ellipsis='...'
            trimRight
            basedOn='letters'
          />   
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

### Movie.css

```css
.Movie{
    background-color:white;
    width:40%;
    display: flex;
    justify-content: space-between;
    align-items:flex-start;
    flex-wrap:wrap;
    margin-bottom:50px;
    text-overflow: ellipsis;
    padding:0 20px;
    box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3), 0 5px 12px rgba(133, 133, 133,0.22);
}

.Movie__Column{
    width:30%;
    box-sizing:border-box;
    text-overflow: ellipsis;
}

.Movie__Column:last-child{
    padding:20px 0;
    width:60%;
}

.Movie h1{
    font-size:20px;
    font-weight: 600;
}

.Movie .Movie__Genres{
    display: flex;
    flex-wrap:wrap;
    margin-bottom:20px;
}

.Movie__Genres .Movie__Genre{
    margin-right:10px;
    color:#B4B5BD;
}

.Movie .Movie__Synopsis {
    text-overflow: ellipsis;
    color:#B4B5BD;
    overflow: hidden;
}

.Movie .Movie__Poster{
    max-width: 100%;
    position: relative;
    top:-20px;
    box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3), 10px 15px 12px rgba(80,80,80,0.22);
}

/* Mobile Phone */
@media screen and (min-width:320px) and (max-width:667px){
    .Movie{
        width:100%;
    }
}

/* Mobile-portrait */
@media screen and (min-width:320px) and (max-width:667px) and (orientation: portrait){
    .Movie{
        width:100%;
        flex-direction: column;
    }
    .Movie__Poster{
        top:0;
        left:0;
        width:100%;
    }
    .Movie__Column{
        width:100%!important;
    }
}
```

<br>

### index.css

```css
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color:#EFF3F7;
  height: 100%;
}

html, #root{
  height:100%;
}
```

