---
layout: post
title: Python & Django Day21 Django view
tags: [django, python]
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>



## url

`www.mydomain.com/ part / ? name=sol&like=python#tag`

<br><br>

## view

화면 구성을 통제

<br>

### urls.py

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/urlpatterns.png" width="80%">

모든 서버 url로 접속하는 요청들은 항상 urlpatterns을 먼저 인식한 후 일치하는 경로로 이동하게 된다.

(ex) 127.0.0.1:9000**/admin**

<br><br>

### Url 추가하기

```python
# urls.py 파일 수정
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('app/', include("myapp.urls"))
]
```

<br>

```python
# myapp 폴더 아래 urls.py 파일 생성
from django.urls import path

urlpatterns =[
    path("")
]
```

```python
# 터미널에서 서버 실행
python manage.py runserver 127.0.0.1:9000

# 아래와 같은 에러가 발생한다
TypeError: _path() missing 1 required positional argument: 'view'
```

<br><br>

### views.py

화면 구성을 통제하는 파일

```python
# myapp 폴더 아래 views.py 수정
from django.shortcuts import render, HttpResponse
import datetime

def say_hi(request):
    now_time = str(datetime.datetime.now())
    return HttpResponse(
        "<h1> Hi </h1>" 
        + '<br>' 
        + now_time
        )
```

<br>

그 다음 urls.py로 views.py를 가져온다.

두 파일이 같은 폴더에 있기 때문에 import로 불러올 수 있다.

```python
# urls.py
from django.urls import path
from . import views

urlpatterns =[
    path("", views.say_hi)
]
```

<br>

* 실행 : 

```python
> python manage.py runserve127.0.0.1:9000
# http://127.0.0.1:9000/app/ 로 접속
```

<br><br>

#### 경로를 통한 인자전달

경로에 <u>?name=value</u> 를 입력하면 값을 전달할 수 있다.

(ex) http://127.0.0.1:9000/app/?name=jane

<br>

위의 예에서는 **def say_hi()** 에 있는 **request**라는 매개변수에 값이 들어가게 된다.

```python
def say_hi(request):
    now_time = str(datetime.datetime.now())
    print(request)    # print를 해서 값 확인
    print(request.GET)
    return HttpResponse(
        "<h1> Hi </h1>" 
        + '<br>' 
        + now_time
        )
```

브라우저에 http://127.0.0.1:9000/app/?name=jane 를 입력 후 새로고침 해 보면 아래와 같이 GET parameter가 출력된다.

<br>

<WSGIRequest: GET '/app/?name=jane'>

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/GETparameter.png" width="80%">

<br><br>

#### Request 값을 꺼내는 방법

먼저 print(request.GET) 로 출력해 보면 

```python
def say_hi(request):
    now_time = str(datetime.datetime.now())
    print(request)    
    print(request.GET)
    return HttpResponse(
        "<h1> Hi </h1>" 
        + '<br>' 
        + now_time
        )
```

> <QueryDict:{'name': ['Signal']}>

이 출력되는 것을 확인할 수 있다.

<br><br>

Get의 값을 추출해서 사용해보면 아래와 같이 가능하다.

```python
def say_hi(request):
    now_time = str(datetime.datetime.now())    
    name = request.GET['name']  
    return HttpResponse(
        "<h1> Hi {}</h1>".format(name) 
        + '<br>' 
        + now_time
        )
```

> System check identified no issues (0 silenced).
> May 09, 2018 - 15:34:12
> Django version 2.0.4, using settings 'firstproject.settings'
> Starting development server at http://127.0.0.1:9000/
> Quit the server with CONTROL-C.
> [09/May/2018 15:34:21] "GET /app/?name=Signal HTTP/1.1" 200 47

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/GetSignal.png" width="80%">

<br>

입력값이 없을 경우 에러가 발생하므로 if문을 이용하여 아래와 같이 예외처리 해 줄 수 있다.

```python
def say_hi(request):
    now_time = str(datetime.datetime.now())    
    name = request.GET('name')
    if not name:
        name = 'Guest'  
    return HttpResponse(
        "<h1> Hi {}</h1>".format(name) 
        + '<br>' 
        + now_time
        )
```