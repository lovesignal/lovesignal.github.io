---
layout: post
date: 2018-05-25
title: "[Clone Coding] KAKAO Talk on HTML"
excerpt: "nomadcoders 강의를 듣고 정리한 카카오톡 클론 코딩 - HTML"
categories: programming
comments: true
tags: [clonecoding, html]
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

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/find_top_bottom.png">

<br>

header 아래 main을 만들고 클래스명은 find라고 정한다. 2개의 섹션을 만드는데, top과 bottom이다. 상단에 있는 섹션을 find-option이라고 정한다. 그 안에 div를 만들고 다시 그 안에 아이콘, span이 있다.

```javascript
// 단축 코드
div.find__option>i.fa+span.find__option-title   

// 아래 구조가 생성 된다. 아이콘이 4개가 있으므로 아래 구조가 4개 필요하다. 각각 아이콘도 입력해준다.
<div class="find__option">
    <i class="fa fa-address-book fa-lg"></i>
    <span class="find__option-title">Find</span>
</div>
<div class="find__option">
        <i class="fa fa-qrcode fa-lg"></i>
        <span class="find__option-title">QR Code</span>
</div>
<div class="find__option">
        <i class="fa fa-mobile fa-2x"></i>
        <span class="find__option-title">Shake</span>
</div>
<div class="find__option">
        <i class="fa fa-envelope fa-lg"></i>
        <span class="find__option-title">Invite via SMS</span>
</div>
```

<br>

두번째 섹션 클래스명은 find-recommended 로 정한다. 

타이틀을 생성해야 하므로 헤더를 만든다.  `h6.find__title`

div로 영역 나누고 span 이용해서 문구를 입력한다.

```html
<section class="find__recommended">
    <header>
        <h6 class="recommended__title">Recommended Friends</h6>
    </header>
    <div class="recommended__none">
        <span class="recommended__text">You have no recommended friends.</span>
    </div>
</section>
```

<br>

* 결과 

  <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/find_header2.png">



<br><br>

# 7. more.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/more_main.png">



<br>

### more-header 

```html
<!-- more-header 코드 -->
<header class="more__header">
    <div class="more-header__column">
        <img src="http://pm1.narvii.com/6331/3cb83dea89204850888261c9252ba5dbb142af13_hq.jpg" alt="">
        <div class="more-header__info">
            <h3 class="more-header__title">
                Ryon
            </h3>
            <span class="more-header__subtitle">
                ryon@gmail.com
            </span>
        </div>
    </div>
    <i class="far fa-comment-alt fa-2x"></i>
</header>
```

<br><br>

### option-bar

```html
<!-- 단축 생성 코드 -->
div.more__option*4>i.fa+span.more__option-title 
```



이전에 만든 내비게이션 생성 원리와 동일하다.

```html
<section class="more__options">
    <div class="more__option">
        <i class="far fa-smile fa-2x"></i>
        <span class="more__option-title">Emoticons</span>
    </div>
    <div class="more__option">
        <i class="fas fa-paint-brush fa-2x"></i>
        <span class="more__option-title">Themes</span>
    </div>
    <div class="more__option">
        <i class="fas fa-user-friends fa-2x"></i>
        <span class="more__option-title">Plus Friend</span>
    </div>
    <div class="more__option">
        <i class="fas fa-code-branch fa-2x"></i>
        <span class="more__option-title">Account</span>
    </div>
</section>
```

<br><br>

### more-plus-freinds

```html
<!-- 단축생성코드 참고 -->
div.plus-friends__item*8>i.fa+span.plus-friends__item-title
```

```html
<section class="more__plus-friends">
    <header class="plus-friend__header">
        <h2 class="plus-friends__title">Plus Friends</h2>
        <span class="plus-friend__learn-more">
            <i class="fas fa-info-circle"></i>
            Learn More
        </span>
    </header>

    <div class="plus-friends__item">
        <div class="plus-friends__item">
            <i class="fas fa-utensils"></i>
            <span class="plus-friends__item-title">Order</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-store"></i>
            <span class="plus-friends__item-title">Store</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-tv"></i>
            <span class="plus-friends__item-title">TV Channel/Raido</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-pencil-alt"></i>
            <span class="plus-friends__item-title">Creation</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-graduation-cap"></i>
            <span class="plus-friends__item-title">Education</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-university"></i>
            <span class="plus-friends__item-title">Politics/Society</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-dollar-sign"></i>
            <span class="plus-friends__item-title">Finance</span>
        </div>
        <div class="plus-friends__item">
            <i class="fas fa-video"></i>
            <span class="plus-friends__item-title">Movies/Music</span>
        </div>
    </div>
</section>
```



### more-options

```html
<section class="more__options">
    <div class="more__option">
        <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/kakaoStory.png" alt="" class="more__options-image">
        <span class="more__options-title">Kakao Story</span>
    </div>
    <div class="more__option">
        <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/path.png" alt="" class="more__options-image">
        <span class="more__options-title">Path</span>
    </div>
    <div class="more__option">
        <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/kakaoFriends.png" alt="" class="more__options-image">
        <span class="more__options-title">Kakao Friends</span>
    </div>
</section>
```



### 전체코드

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

    <main class="more">
        <header class="more__header">
            <div class="more-header__column">
                <img src="http://pm1.narvii.com/6331/3cb83dea89204850888261c9252ba5dbb142af13_hq.jpg" alt="">
                <div class="more-header__info">
                    <h3 class="more-header__title">
                        Ryon
                    </h3>
                    <span class="more-header__subtitle">
                        ryon@gmail.com
                    </span>
                </div>
            </div>
            <i class="far fa-comment-alt fa-2x"></i>
        </header>

        <section class="more__options">
            <div class="more__option">
                <i class="far fa-smile fa-2x"></i>
                <span class="more__option-title">Emoticons</span>
            </div>
            <div class="more__option">
                <i class="fas fa-paint-brush fa-2x"></i>
                <span class="more__option-title">Themes</span>
            </div>
            <div class="more__option">
                <i class="fas fa-user-friends fa-2x"></i>
                <span class="more__option-title">Plus Friend</span>
            </div>
            <div class="more__option">
                <i class="fas fa-code-branch fa-2x"></i>
                <span class="more__option-title">Account</span>
            </div>
        </section>

        <section class="more__plus-friends">
            <header class="plus-friend__header">
                <h2 class="plus-friends__title">Plus Friends</h2>
                <span class="plus-friend__learn-more">
                    <i class="fas fa-info-circle"></i>
                    Learn More
                </span>
            </header>

            <div class="plus-friends__item">
                <div class="plus-friends__item">
                    <i class="fas fa-utensils"></i>
                    <span class="plus-friends__item-title">Order</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-store"></i>
                    <span class="plus-friends__item-title">Store</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-tv"></i>
                    <span class="plus-friends__item-title">TV Channel/Raido</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-pencil-alt"></i>
                    <span class="plus-friends__item-title">Creation</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-graduation-cap"></i>
                    <span class="plus-friends__item-title">Education</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-university"></i>
                    <span class="plus-friends__item-title">Politics/Society</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-dollar-sign"></i>
                    <span class="plus-friends__item-title">Finance</span>
                </div>
                <div class="plus-friends__item">
                    <i class="fas fa-video"></i>
                    <span class="plus-friends__item-title">Movies/Music</span>
                </div>
            </div>
        </section>

        <section class="more__options">
            <div class="more__option">
                <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/kakaoStory.png" alt="" class="more__options-image">
                <span class="more__options-title">Kakao Story</span>
            </div>
            <div class="more__option">
                <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/path.png" alt="" class="more__options-image">
                <span class="more__options-title">Path</span>
            </div>
            <div class="more__option">
                <img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/kakaoFriends.png" alt="" class="more__options-image">
                <span class="more__options-title">Kakao Friends</span>
            </div>
        </section>
    </main>

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
        <a href="more.html" class="tab-bar__tab tab-bar__tab--selected">
            <i class="fa fa-ellipsis-h"></i>
            <span class="tab-bar__title">More</span>
        </a>
    </nav>
</body>
</html>
```

<br><br>

# 8. chat.html

## chats.html과 chat.html연결하기

chat.html로 이동하는 방법은 index.html에서 채팅창 리스트를 클릭해서 chats.html로 이동한다. 그리고 chats.html에서 채팅창 리스트를 클릭해서 chat.html로 이동할 수 있어야 한다.



chats.html에 **chats_chat 클래스 li 리스트** 안에 링크를 만든 후 chat.hmtl로 연결시킨다. 동일한 작업을 모든 리스트에 한다.

```html
<ul class="chats__list">
    <li class="chats_chat">
        <a href="chat.html">  <!-- 리스트를 chat.html에 연결 시킴 -->
            <div class="chat__content">
               ....... code 생략
            </span>
        </a>
    </li>
</ul>
```



아래와 같이 연결 된 것을 확인할 수 있다.

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chat_li_chats.gif">

<br>

마찬가지 방법으로  화살표 아이콘에도 링크를 걸어준다.

```html
<div class="header__bottom">
    <div class="header__column">
        <a href="chats.html">              <!-- 링크 연결해주기 -->
            <i class="fa fa-chevron-left fa-lg"></i>
        </a>
    </div>
		..... 생략 .....
</div>
```

<br>

## chat.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chat_html.png">

```html
<main class="chat">
    <div class="date-divider">
        <span class="date-divider__text">Wednesday, August 2, 2018</span>
    </div>
    <div class="chat__message chat__message--from-me">
        <span class="chat__message-time">17:55</span>
        <span class="chat__message-body">
            Hello! This is a test.message.
        </span>
    </div>
    <div class="chat__message chat__message--to-me">
        <img src="https://www.90daykorean.com/wp-content/uploads/2015/04/Groovy-Jay-G-300x293.png" class="chat-message-avatar">
        <div class="chat__message-center">
            <h3 class="chat__message-username">Jay-G</h3>
            <span class="chat__message-body">
                And this is an answer.
            </span>
        </div>
        <span class="chat__message-time">18:55</span>
    </div>
</main>
<div class="type-message">
    <i class="fa fa-plus fa-2x"></i>
    <div class="type-message__input">
        <input type="text">
        <i class="far fa-smile"></i>
        <span class="record-message">
            <i class="fas fa-microphone"></i>
        </span>
    </div>
</div>
```

<br>

* 결과

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/chat_html_2.png">

<br>

<br>

# 9. profile.html

## index.html과 profile.html 연결

index.html에서 프로필을 클릭하면 profile.html로 이동해야 한다.

```html
<div class="friends__section-rows">
    <div class="friends__section-row">
        <a href="profile.html">       <!-- profile.html과 연결 -->
            ..... 생략.....
        </a>
    </div>
</div>
```

<br>

<br>

## profile.html

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/profile_html.png">

<br>

header 아래에 main을 생성한다.

```html
<main class="profile">
    <header class="profile__header">
        <img src="http://pm1.narvii.com/6331/3cb83dea89204850888261c9252ba5dbb142af13_hq.jpg">
        <h3 class="profile__header-title">Ryan</h3>
    </header>
    <input type="text" placeholder="ryan@gmail.com">
    <div class="profile__actions">
        <div class="profile__action">
            <span class="profile__action-circle">
                <i class="fas fa-comment fa-2x"></i>
            </span>
            <span class="profile__action-title">My Chatroom</span>
        </div>
        <div class="profile__action">
            <span class="profile__action-circle">
                <i class="fas fa-edit fa-2x"></i>
            </span>
            <span class="profile__action-title">Edit Profile</span>
        </div>
    </div>
</main>
```



profile.html에서는 상단의 x를 누르면 index.html로 돌아가야 한다. 

```html
<div class="header__bottom">
    <div class="header__column">
        <a href="index.html">           <!-- 아이콘에 링크를 걸어준다. -->
            <i class="fa fa-times fa-lg"></i>
        </a>     
        .... 생략 .....
</div>
```



* 결과

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/kakao-clone/profile_html_2.png">









