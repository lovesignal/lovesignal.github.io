---
layout: post
date: 2018-05-01
title: Python & Django Day18 Python 가상환경 세팅 & Django 설치
tags: [django, python]
categories: programming
comments: true
---

 Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

## Python Virtual Environment

* 가상환경의 필요성
  1. 버전의 분리 : 버전별로 또는 필요에 따라 패키지 등을 다르게 설치할 수 있다.
  2. 서버와의 통일

<br>

### 가상환경 만들기

```
$ python3 -m venv first-env    # python3 -m venv 가상환경이름
$ ls	# 설치된 것 확인
first env

$ cd first-env	# 폴더로 들어가기
$ source first-env/bin/activate		# 적용

# pip list를 입력해보면 여태까지 설치된 패키지가 나오지 않고, 기본 패키지만 나오는 것을 볼 수 있다.
$ pip list

# Django 설치
$ pip install django
```

```
// 가상환경 python 실행
$ python

// django 불러오기
>>> import django
>>> django

// 가상환경 종료
$ deactivate
```

<br>

#### Django 프로젝트 생성

```
// 장고 프로젝트 생성
$ django-admin startproject 프로젝트이름
```

<br>

#### Django 서버 실행

프로젝트폴더로 이동 후(manage.py가 있는 디렉토리)

```
$ python manage.py runserver
```

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_server1.png" width="90%">

<br>

http://127.0.0.1:8000/ 으로 접속하면 아래와 같은 화면이 뜬다.

<img src="https://raw.githubusercontent.com/lovesignal/img/master/programming/django/django_server2.png" width="80%">

