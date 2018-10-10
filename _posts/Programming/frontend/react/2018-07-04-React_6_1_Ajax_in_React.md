---
key: 20180704
title: "[React] Movie app clone coding : Ajax in React"
excerpt: "movie app 만들기 - Fetch 이용해서 API 불러오기"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 6-1. Ajax in React

<br>

## Ajax

Ajax는 Asynchronous Javascript and XML의 약자이다.

JSON은 Javascript Object Notation의 약자이다. Object를 Javascript로 작성하는 기법이다. 

<br>

<br>

<br>

## Fetch

FETCH를 이용해서 URL에서 정보를 GET 하는 방법을 배운다. movie app에 사용할 URL은 API-YTS torrent movie database에서 가져 온다. ( https://yts.am/api#list_movies )



https://yts.am/api#list_movies 에서 Examples에 있는 URL을 복사한다. 

복사한 `https://yts.am/api/v2/list_movies.json` 를 열면 javascript object를 볼 수 있다. 이것을 react에서 불러올 수 있어야 한다. 

사이트에서 보면 아래와 같은 정보가 나오는데 이것을 활용하여 리스트를 필터, 정렬을 할 수 있다. 

<br>

**Endpoint Parameters**

| Parameter         | Required | Type                                                         | Default    | Description                                                  |
| ----------------- | -------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| `limit`           |          | Integer between 1 - 50 (inclusive)                           | 20         | The limit of results per page that has been set              |
| `page`            |          | Integer (Unsigned)                                           | 1          | Used to see the next page of movies, eg limit=15 and page=2 will show you movies 15-30 |
| `quality`         |          | String (720p, 1080p, 3D)                                     | All        | Used to filter by a given quality                            |
| `minimum_rating`  |          | Integer between 0 - 9 (inclusive)                            | 0          | Used to filter movie by a given minimum IMDb rating          |
| `query_term`      |          | String                                                       | 0          | Used for movie search, matching on: Movie Title/IMDb Code, Actor Name/IMDb Code, Director Name/IMDb Code |
| `genre`           |          | String                                                       | All        | Used to filter by a given genre (See http://www.imdb.com/genre/ for full list) |
| `sort_by`         |          | String (title, year, rating, peers, seeds, download_count, like_count, date_added) | date_added | Sorts the results by choosen value                           |
| `order_by`        |          | String (desc, asc)                                           | desc       | Orders the results by either Ascending or Descending order   |
| `with_rt_ratings` |          | Boolean                                                      | false      | Returns the list with the Rotten Tomatoes rating included    |

<br>

<br>

예를들어 `https://yts.am/api/v2/list_movies.json` 에 `sort_by=rating` 를 붙여서 `https://yts.am/api/v2/list_movies.json?sort_by=rating` 에 접속하면 DB가 평점순으로 정렬된 것을 확인할 수 있다. 최종적으로 이 URL이 React에서 불러들이려고 하는 것이다. 

<br>

<br>

<br>

### componentDidMount() Fetch

root component ( `class App extends Component` )로 가서 `componentDidMount` 에 이전에 작업한 timeout, 매트릭스, 올드보이 등 영화대신  영화 DB를 넣는다.

component가 DidMount 했을 때 불러들이게 만들려고 한다.

```javascript
// App.js
class App extends Component {

  state = {}

  componentDidMount(){
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=rating')
  }

  ...
```

<br>

<br>

네트워크 상태를 살펴보면 아래와 같은 순서로 불러들인다. 

<img src="https://gitlab.com/goudacheese/image/raw/master/frontend/javascript/react_movieapp/fetch.png">

<br>

다시 정리하면, `component` 가 `mount` 되면 (`componentDidMount`) , `fetch()` 안의 URL로 가서 fetch해 오는 것이다.

💡 **Ajax는 URL을 javascript로 `asynchronous (비동기화) 방법` 으로 불러온다.** **데이터를 불러올 때마다 페이지를 새로고침 하고 싶지 않기 때문에 Ajax를 사용한다.** 예를들어, 로딩을 하면 API를 불러온다. 동시에 평점을 가져오기도 한다. 즉, **Javascript와 함께 데이터를 다룰 수 있다.** 