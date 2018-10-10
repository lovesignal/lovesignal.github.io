---
title: Python & Django Day20 Django 프로젝트 파일 구조, MTV
key: 20180505
tags: [django, python]
categories: programming
comments: true
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>



## Django 프로젝트 만들기

```
$ python3 -m venv django-venv
$ source django-venv/bin/activate
$ pip install django
$ django-admin startproject firstproject
```

<br>

아래 구조의 프로젝트가 생성된다.

<br>

## Django 프로젝트 디렉토리 형태

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_project.png" width="90%">

<br>

### manage.py

다양한 명령어를 수행시켜주는 매개체 역할을 한다.

<br>

### ______init______.py

파이썬 모듈로써 동작을 할 수 있다.

<br>

### settings.py

여러 설정들을 기억해 두는 파일.

<br>

### wigs.py

웹서버에 배포를 할때 설정파일들을 연결시켜주는 파이썬 파일.

<br><br>

## Django 앱 추가해보기

```
source ../django-env/bin/activate    # 가상환경 실행
python3 manage.py startapp myapp     # myapp 자리에 앱 이름 넣으면 됨
```

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_myapp.png" width="90%">

<br><br>

## Django MTV

### Model

데이터 베이스 관리

### Template

사용자가 보는 화면(HTML, CSS 등)

### View

화면을 구성 통제. 데이터베이스와 템플릿을 연결

