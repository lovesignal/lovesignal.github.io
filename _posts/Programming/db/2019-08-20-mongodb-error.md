---
key: 20190820
title: "[MongoDB] MongoDB 에러 해결 메모 (업데이트 중...)"
excerpt: "mongod.lock 관련 에러, SocketException: Address already in use MONGODB 에러 해결 메모"
categories: programming
comments: true
tags: [MongoDB]
---

### mongod.lock 관련 에러

```shell
# 기존 데이터 보호
$ sudo -u mongodb mongod --dbpath /var/lib/mongodb --repair --repairpath /var/lib/mongodb0
# 새롭게 띄우기
$ sudo -u mongodb mongod --dbpath /var/lib/mongodb --repair

# permission 문제
$ sudo chown -R mongodb:mongodb "/var/lib/mongodb"
```

<https://stackoverflow.com/questions/13700261/mongodb-wont-start-after-server-crash>



**에러**

```shell
● mongodb.service - High-performance, schema-free document-oriented 
 
database
   Loaded: loaded (/etc/systemd/system/mongodb.service; enabled; vendor preset: 
   Active: failed (Result: exit-code) 
  Process: 2331 ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf (cod
 Main PID: 2331 (code=exited, status=2)
```



**해결**

```shell
$ sudo vim mongodb.service
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target
 
[Service]
User=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf
  
[Install]
WantedBy=multi-user.target
```



### SocketException: Address already in use MONGODB 해결 방법

kill the previous mongod instance and start the new one

```
# To kill the previous mongod instance, first search for a list of tasks running on machin
$ sudo lsof -iTCP -sTCP:LISTEN -n -P

# search for mongod COMMAND and its PID and type
$ sudo kill <mongo_command_pid>

# start mongod instance
$ mongod
```



## 외부접속 설정

```
$ sudo vim /etc/mongod.conf

# network interfaces
net:
  port: 27017
  bindIp: ::,0.0.0.0
```