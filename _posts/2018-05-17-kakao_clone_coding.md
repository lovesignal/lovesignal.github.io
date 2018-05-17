---
layout: post
date: 2018-05-17
title: "[FrontEnd] KAKAO Talk on HTML"
excerpt: "Nomadcoders Kakao talk clone coding 강의 정리 노트"
categories: programming
comments: true
tags: [clone coding, nomadcoders, frontend, html, css]
comments: true
---



# 1. 파일과 폴더 생성

**구성할 화면 6가지**

1. Friend
2. Chats
3. Find
4. More
5. Chat
6. profile

<br>

구성할 화면이 6가지라는 의미는 6개의 html 파일을 만들어야 한다는 것이다.

6개의 html 파일과 2개의 폴더를 아래와 같이 만든다.

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/structures.png" width="200">



<br><br>

# 2. 헤더 만들기

헤더는 바로 맨 위에 프로필명 있는 구획을 의미한다. 

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/header.png" width="50%">

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/header2.png" width="50%">

<br><br>

## index.html

## Header

```html
// head
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Friends</title>
</head>
```

<br>

헤더 안에 2개의 div 만든다. 

* Top Header : 맨 상단(와이파이, 시간 표시된 곳)
* Bottom Header : manage, Friends라고 작성된 헤더

Top Header에는 column이 3개 있으므로 만들어준다.

```html
<div class="header__top"></div>
    <div class="header__column"></div>
    <div class="header__column"></div>
    <div class="header__column"></div>
<div class="header__bottom"></div>
```

<br><br>

### Top Header

첫번째 Header column에는 비행기, 와이파이 아이콘이 필요.

두번째 Header column에는 header__time이라는 span 만듦.

세번째 Header column에는 달 아이콘, 블루투스 아이콘, header__battery라는 span 만듦

```html
<header>
    <div class="header__top"></div>
    <div class="header__column"></div>
        <!-- plane icon -->
        <!-- wifi icon -->
    <div class="header__column"></div>
        <span class="header__time">18:38</span>
    <div class="header__column"></div>
        <!-- moon icon -->
        <!-- bluetooth icon -->
        <span class="header__battery">66% <!--battery icon--> </span>
    <div class="header__bottom"></div>
</header>
```

<br><br>

### 아이콘 가져오기

fontawesome(https://fontawesome.com/icons?from=io)이라는 사이트에서 css를 이용하여 다양한 아이콘을 가져올 수 있다. 

https://fontawesome.com/get-started 참고해서 링크를 문서에 붙여넣기 한다. 이 링크를 붙이고 나면, fontawesome에 있는 다양한 아이콘들을 불러와서 쓸 수 있다.



위치 : 상단 head > meat > 다음 줄

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    ....
</head>
```

<br>

적절한 아이콘을 찾아서 제공하는 링크를 붙여 넣는다.

```html
<div class="header__top">
	<div class="header__column">
		<i class="fas fa-plane"></i>  <!-- plane icon -->
		<i class="fas fa-wifi"></i>   <!-- wifi icon -->
    </div>
	<div class="header__column">
		<span class="header__time">18:38</span>
    </div>
	<div class="header__column">
		<i class="fas fa-moon"></i>    <!-- moon icon -->
		<i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
		<span class="header__battery">100% <i class="fas fa-battery-full"></i>
		</span>
    </div>
</div>
```

<br><br>

### Bottom Header

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/bottomHeader.png" width="50%">

화면을 살펴보면 중앙에 큰 텍스트가 있고, 왼쪽, 오른쪽에 아이콘이 있다.

div column을 3개 만든다.

column1 : manaege

column2 : Friends

column3 : setting

```html
<div class="header__bottom">
	<div class="header__column">
		<span class="header__text">Manage</span>
	</div>
	<div class="header__column">
		<span class="header__text">Friends <span class="header__number">1</span></span>
	</div>
	<div class="header__column">
		<i class="fa fa-cog fa-lg"></i>
	</div>
</div>
```

<br><br>

### 전체코드

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Friends</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <span class="header__text">Manage</span>
            </div>
            <div class="header__column">
                <span class="header__text">Friends <span class="header__number">1</span></span>
            </div>
            <div class="header__column">
                <i class="fa fa-cog fa-lg"></i>
            </div>
        </div>
    </header>
</body>
</html>

```

<br>

* **결과**

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/index_header.png" width="30%">

<br>

<br>

## chats.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chats_header.png" width="50%">

<br>

index.html 내용을 복사 붙여넣기 한 후 수정한다.

title -> Chats 

숫자 span -> 화살표 아이콘

컬럼이 3개가 아니라 두개.

Manage -> Edit

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Chats</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <span class="header__text">Edit</span>
            </div>
            <div class="header__column">
                <span class="header__text">Chats<i class="fa fa-caret-down"></i></span>
            </div>
        </div>
    </header>
</body>
</html>

```

<br>

- **결과**

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chats_1.png" width="25%">

<br>

<br>

## Find.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/find.png" width="50%">



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Find</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <span class="header__text">Edit</span>
            </div>
            <div class="header__column">
                <span class="header__text">Find</span>
            </div>
        </div>
    </header>
</body>
</html>

```

<br>

* **결과**

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/find_header.png" width="25%">

<br>

<br>

## more.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/more.png" width="50%">

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>More</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <span class="header__text">More</span>
            </div>
            <div class="header__column">
                <i class="fa fa-cog fa-lg"></i>  <!-- fa-lg : icon 크기 확대 -->
            </div>
        </div>
    </header>
</body>
</html>
```

* **결과**

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/more_header.png" width="25%">

<br>

<br>

## Chat.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/header.png" width="50%">

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Chat</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <i class="fa fa-chevron-left fa-lg"></i>     
            </div>
            <div class="header__column">
                <span class="header__text">LYNN</span>
            </div>
            <div class="header__column">
                <i class="fa fa-search"></i>
                <i class="fa fa-bars"></i>
            </div>
        </div>
    </header>
</body>
</html>
```

<br>

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chat_header.png" width="25%">

<br>

<br>

## profile.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/profile.png" width="50%">

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Profile</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <i class="fa fa-times fa-lg"></i>     
            </div>
            <div class="header__column">
                <i class="fa fa-user fa-lg"></i>
            </div>
        </div>
    </header>
</body>
</html>
```

<br>

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/profile_header.png" width="25%">

<br>

<br>

# 3. 네비게이션 만들기

## index.html

헤더 아래에 nav를 작성한다. 클래스명은 **tab-bar**로 한다. 그 안에 **4개의 링크**가 있다.

첫번째 링크는 index.html로 이동.

두번째 링크는 chats.html로 이동.

세번째는 find.html로 이동.

네번째는 more.html로 이동.

```html
<nav class="tab-bar">
    <a href="index.html" class="tab-bar__tab"></a>
    <a href="chats.html" class="tab-bar__tab"></a>
    <a href="find.html" class="tab-bar__tab"></a>
    <a href="more.html" class="tab-bar__tab"></a>
</nav>
```

<br>

각 4개의 링크 안에 모두 아이콘이 있는 span을 만든다. span 이름은 tab-bar-title이라고 한다. 각각 아이콘과 이름을 입력한다.

```html
<nav class="tab-bar">
    <a href="index.html" class="tab-bar__tab">
        <i class="fa fa-user"></i>
        <span class="tab-bar__title">Friends</span>
    </a>
    <a href="chats.html" class="tab-bar__tab">
        <i class="fa fa-comment"></i>
        <span class="tab-bar__title">Chats</span>
    </a>
    <a href="find.html" class="tab-bar__tab">
        <i class="fa fa-search"></i>
        <span class="tab-bar__title">Find</span>
    </a>
    <a href="more.html" class="tab-bar__tab">
        <i class="fa fa-ellipsis-h"></i>
        <span class="tab-bar__title">More</span>
    </a>
</nav>
```

<br>

다른 html 파일에 내비게이션 코드를 복사-붙여넣기 하기 전에, **해당 페이지가 선택되었을 때 다르게 보이는 class를 작성**해야 한다.

예를들어, index.html에서는 Friends 링크가 활성화 된다. 이에 맞추어 클래스명을 **tab-bar_tab-selected** 로 변경 해준다.

```html
<nav class="tab-bar">
    <a href="index.html" class="tab-bar__tab tab-bar__tab--selected">
        <i class="fa fa-user"></i>
        <span class="tab-bar__title">Friends</span>
    </a>
    <a href="chats.html" class="tab-bar__tab">
        <i class="fa fa-comment"></i>
        <span class="tab-bar__title">Chats</span>
    </a>
    <a href="find.html" class="tab-bar__tab">
        <i class="fa fa-search"></i>
        <span class="tab-bar__title">Find</span>
    </a>
    <a href="more.html" class="tab-bar__tab">
        <i class="fa fa-ellipsis-h"></i>
        <span class="tab-bar__title">More</span>
    </a>
</nav>
```

chats, find, more의 각각 html 파일의 활성화 되는 탭의 코드를 위와 같이 변경해준다.

* 결과 : index.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/index_nav.png" width="50%">

<br>

<br>

<br>

# 4. 친구리스트 목록 만들기

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/friends_list.png" width="50%">

<br>

섹션이 총 3개이다. 

search bar, My Profile, Friends

<br>

## index.html

### Search bar

header와 nav 사이에 main이라는 태그를 만든다. 이 main의 클래스명을 friends라고 정한다.

가장 상단에 있는 검색창을 만들어야 하므로 div를 만들고, 이름은 search-bar로 한다. 검색창 내부에 search 아이콘을 불러온다. 그 다음 input 창을 만든다. 

"Find friends, chats, Plus Friends"라고 placeholder를 작성한다. 

```html
<main class="friends">
    <div class="search-bar">
        <i class="fa fa-search"></i>
        <input type="text" placeholder="Find friends, chats, Plus Friends">
    </div>
</main>
```

<br>

### My Profile

다음은 검색창 아래 my profile 섹션을 만든다. main 안에 클래스명 friends_profile의 섹션을 만든다. 왜냐하면 main 클래스가 friends이기도 하고, 이후 profile과 혼동되면 안되기 때문이다. 

헤더를 작성하고, h6 크기의 타이틀을 만든다. 클래스명을 friends__section-title로 입력한다.

헤더 밖에 2개의 줄이 있다. 그러므로 div를 생성하고 클래스명은 friends__section-rows라고 정한다. 첫번째 row는 'me'이고, 두번째 row는 이다.

div를 만들고 프로필 이미지를 추가한다.( 이미지 주소값은 추후 설정)

span 태그로 이름을 입력한다. 클래스명은 friends__section-name으로 한다.

```html
<main class="friends">
    <div class="search-bar">
        <i class="fa fa-search"></i>
        <input type="text" placeholder="Find friends, chats, Plus Friends">
    </div>

    <section class="friends__section">
        <header class="friend__section-header">
            <h6 class="friends__section-title">My profile</h6>
        </header>
        <div class="friends__section-rows">
            <div class="friends__section-row">
                <img src="" art="">
                <span class="friends__section-name">Nicolas</span>
            </div>
        </div>
    </section>
</main>
```

 <br>

두번째 row는 Friends' Names Display 이다.

위와 마찬가지 방법으로 작성하고, span의 내용을 Friends' Name Display를 넣어준다.

```html
<div class="friends__section-row">
    <img src="" art="">
    <span class="friend__section-name">Friends' Name Display</span>
</div>
```

 <br>

### Friends

기본 구조는 My Profile과 유사하고, 상태 메시지가 있으므로 div를 생성한다 클래스명은 friends-section-column으로 정한다.

```html
<section class="friends__section">
    <header class="friend__section-header">
        <h6 class="friends__section-title">Friends</h6>
    </header>
    <div class="friends__section-rows">
        <div class="friends__section-row">
            <div class="friends-section-column">
                <img src="" art="">
                <span class="friends__section-name">Lynn</span>
            </div>
            <span class="friends__section-tagline">
                Life is short. So live your life.
            </span>
        </div>
    </div>
</section>
```

<br>

### 전체코드

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css" integrity="sha384-DNOHZ68U8hZfKXOrtjWvjxusGo9WQnrNx2sqG0tfsghAvtVlRW3tvkXWZh58N9jp" crossorigin="anonymous">
    <title>Friends</title>
</head>

<body>
    <header>
        <div class="header__top">
            <div class="header__column">
                <i class="fas fa-plane"></i>   <!-- plane icon -->
                <i class="fas fa-wifi"></i>    <!-- wifi icon -->
            </div>
            <div class="header__column">
                <span class="header__time">18:38</span>
            </div>
            <div class="header__column">
                <i class="fas fa-moon"></i>    <!-- moon icon -->
                <i class="fab fa-bluetooth-b"></i>    <!-- bluetooth icon -->
                <span class="header__battery">100%<i class="fas fa-battery-full"></i>
                </span>
            </div>
        </div>
        <div class="header__bottom">
            <div class="header__column">
                <span class="header__text">Manage</span>
            </div>
            <div class="header__column">
                <span class="header__text">Friends <span class="header__number">1</span></span>
            </div>
            <div class="header__column">
                <i class="fa fa-cog fa-lg"></i>
            </div>
        </div>
    </header>

    <main class="friends">
        <div class="search-bar">
            <i class="fa fa-search"></i>
            <input type="text" placeholder="Find friends, chats, Plus Friends">
        </div>

        <section class="friends__section">
            <header class="friend__section-header">
                <h6 class="friends__section-title">My profile</h6>
            </header>
            <div class="friends__section-rows">
                <div class="friends__section-row">
                    <img src="" art="">
                    <span class="friends__section-name">Nicolas</span>
                </div>
                <div class="friends__section-row">
                    <img src="" art="">
                    <span class="friend__section-name">Friends' Name Display</span>
                </div>
            </div>
        </section>

        <section class="friends__section">
            <header class="friend__section-header">
                <h6 class="friends__section-title">Friends</h6>
            </header>
            <div class="friends__section-rows">
                <div class="friends__section-row">
                    <div class="friends-section-column">
                        <img src="" art="">
                        <span class="friends__section-name">Lynn</span>
                    </div>
                    <span class="friends__section-tagline">
                        Life is short. So live your life.
                    </span>
                </div>
            </div>
        </section>

    </main>

    <nav class="tab-bar">
        <a href="index.html" class="tab-bar__tab tab-bar__tab--selected">
            <i class="fa fa-user"></i>
            <span class="tab-bar__title">Friends</span>
        </a>
        <a href="chats.html" class="tab-bar__tab">
            <i class="fa fa-comment"></i>
            <span class="tab-bar__title">Chats</span>
        </a>
        <a href="find.html" class="tab-bar__tab">
            <i class="fa fa-search"></i>
            <span class="tab-bar__title">Find</span>
        </a>
        <a href="more.html" class="tab-bar__tab">
            <i class="fa fa-ellipsis-h"></i>
            <span class="tab-bar__title">More</span>
        </a>
    </nav>
</body>
</html>
```

<br>

* **결과**

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/index_4.png" width="40%">

<br>

<br>

# 5. chats.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chats.png" width="40%">

상단에 검색창이 있고, 두개의 줄이 있다. 각 줄마다 두개의 컬럼이 있다. 첫번째 컬럼에는 1개의 div, 1개의 이미지가 있다. 

chats.html에서 header 다음에 클래스명이 chats인 main을 생성한다.  index.html에서 만들었던 검색창을 붙여넣기 한다.

클래스명이 chats__list인 ul을 만든다. 그 안에 아이템 리스트를 만드는데, 클래스명은 chats-chat 이라고 정한다. 이 리스트 안에 2개의 컬럼을 만든다. 첫번째 컬럼은 프로필 사진을 포함한 메시지 상태창이고, 두번째 컬럼은 시간이다. chat-content div와 chat-data-time span을 만든다.  

각 리스트와 리스트 아이템을 만들었다. (코드 참고)

```html
<!-- main code -->
<main class="chats">
    <div class="search-bar">
        <i class="fa fa-search"></i>
        <input type="text" placeholder="Find friends, chats, Plus Friends">
    </div>
    <ul class="chats__list">
        <li class="chats_chat">
            <div class="chat__content">
                <img src="http://pm1.narvii.com/6331/3cb83dea89204850888261c9252ba5dbb142af13_hq.jpg">
                <div class="chat__preview">
                    <h3 class="chat__user">Ryan</h3>
                    <span class="chat-last-message">I am king.</span>
                </div>
            </div>
            <span class="chat__date-tiem">
                15:55
            </span>
        </li>
    </ul>
    <ul class="chats__list">
            <li class="chats_chat">
                <div class="chat__content">
                    <img src="https://www.90daykorean.com/wp-content/uploads/2015/04/Groovy-Jay-G-300x293.png">
                    <div class="chat__preview">
                        <h3 class="chat__user">Jay-G</h3>
                        <span class="chat-last-message">Sooooooo....</span>
                    </div>
                </div>
                <span class="chat__date-tiem">
                    01:58
                </span>
            </li>
        </ul>
    <div class="chat-btn">
        <i class="fa fa-comment"></i>
    </div>
</main>
```

<br>

* 결과

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chats_main.png" width="50%">

<br>

<br>

# 6. find.html



(작성 중…..)
