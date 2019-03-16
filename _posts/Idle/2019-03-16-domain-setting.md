---
key: 20190316
title: "Godaddy와 Github page 도메인 연동하기"
excerpt: "Godaddy에서 구입한 도메인을 Github 블로그와 연결한다."
comments: true
tags: [idle, daily, blog, domain]
categories: idle
---

## Github 블로그 설정

1. 블로그 repository 밑에  `CNAME` 파일을 만들고 사용할 도메인을 입력하여 저장한다.

<br>

![](https://raw.githubusercontent.com/lifeisgouda/img/master/etc/domain-CNAME.png)

<br>

<br>

2. Github setting에 들어가서 GitHub Pages 항목 아래 Custom domain 란에 사용할 도메인을 입력한다.
3. Enforce HTTPS 가 체크 되어 있는지 확인하고, 체크 되어 있지 않다면 체크 해둔다.

<br>

![](https://raw.githubusercontent.com/lifeisgouda/img/master/etc/domain-setting.png)

<br>

<br>

## Godaddy Setting

1. Godaddy에 접속하여 DNS Management 메뉴로 들어간다.

   (` https://dcc.godaddy.com/manage/{자기도메인}/dns` )

2. Add 버튼을 눌러서 아래 이미지의 빨간 박스 내용을 똑같이 입력한다.

<br>

![](https://raw.githubusercontent.com/lifeisgouda/img/master/etc/domian-DNS_management.png)

<br>

적용 되는데 약간 시간이 걸리므로 기다린다.



