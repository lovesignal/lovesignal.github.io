---
layout : post
date: 2018-03-01
title: "[Hadoop] Hadoop 완전분산모드 설치"
excerpt: "VirtualBox를 이용하여 Hadoop을 완전분산모드로 설치하는 방법 정리"
categories: programming
comments: true
tag : [hadoop, data engineering]
---



## [Progamming] Hadoop 완전분산모드 설치

VirtualBox 에 4개의 Ubuntu 를 만든다.

설치 시 사용자명은 hadoop 으로 한다.

4개를 따로 설치하거나 1개를 만들어서 3개를 복제한다.

각각 아래처럼 이름과 IP 주소를 사용할 예정. 
IP 주소는 각 VirtualBox에서 자동으로 생성되고 뒤에 2자리만 순서대로 변경해서 넣어주면된다.

192.168.30.101 hadoop01  

192.168.30.102 hadoop02   

192.168.30.103 hadoop03 

192.168.30.104 hadoop04 

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/hadoop_copy.png?raw=true)
<br>


#### 복제 전에 할 일

hadoop01에 아래와 같이 먼저 설치한 후 복제해서 hadoop02 ~ hadoop04를 만든다.

```
// vim 설치
$ sudo apt-get install vim

// 각각 Ubuntu 에 JDK 8 설치
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```


```
// 자바 환경설정. 아래 내용 입력 후 저장
$ vim .bashrc
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/java_path.png?raw=true)
<br>
<br>



### VirtualBox 호스트 전용 어댑터 설정

#### 1. 전체 설정

VirtualBox > 전역 도구(G) > 호스트 네트워크 관리자 > 만들기 > vboxnet0 > 192.168.57.1 > 어댑터 > o 수동으로 어댑터 설정 > IPv4 주소: 192.168.30.1 > IPv4 서브넷 마스크: 255.255.255.0



#### 2. 각 VM이 종료된 상태에서 어댑터 추가

VM > 우클릭 > 설정 > 네트워크 > 어댑터 2 > v 네트워크 어댑터 사용하기 > 다음에 연결됨: 호스트 전용 어댑터 > 이름: vboxnet1 > 확인



#### hadoop 복제

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/host1.png?raw=true)
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/host2.png?raw=true)
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/host3.png?raw=true)
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/host4.png?raw=true)
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/host6.png?raw=true)
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/hadoop_copy.png?raw=true) 
<br><br>





#### 3.  게스트 OS 네트워크 설정

```
// ifconfig 로 체크한 이름 중 enp0s8 을 기준으로 수정하면 됨
$ ifconfig
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/ifconfig.png?raw=true) <br><br>





```
// cat 으로 현재 정보 확인
$ sudo cat /etc/network/interfaces

// hadoop01 에서 vi 로 아래 내용 추가
$ sudo vi /etc/network/interfaces

auto enp0s8
iface enp0s8 inet static
address 192.168.56.101
netmask 255.255.255.0
network 192.168.56.1
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/interfaces.png?raw=true)<br><br>





```
// hostname 수정
$ sudo vi /etc/hostname
hadoop01
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/hostname.png?raw=true)<br><br>





```
$ sudo reboot
// 리부팅
```



#### 4. 호스트 OS 에서 ping 으로 체크하면 응답 OK

```
$ ping 192.168.56.101

// hadoop02 에서 vi 로 아래 내용 추가
$ sudo vi /etc/network/interfaces

auto enp0s8
iface enp0s8 inet static
address 192.168.56.102
netmask 255.255.255.0
network 192.168.56.1

// hostname 수정
$ sudo vi /etc/hostname
hadoop02

// 리부팅
$ sudo reboot


// hadoop03 에서 vi 로 아래 내용 추가
$ sudo vi /etc/network/interfaces

auto enp0s8
iface enp0s8 inet static
address 192.168.56.103
netmask 255.255.255.0
network 192.168.56.1

// hostname 수정
$ sudo vi /etc/hostname
hadoop03

// 리부팅
$ sudo reboot


// hadoop04 에서 vi 로 아래 내용 추가
$ sudo vi /etc/network/interfaces

auto enp0s8
iface enp0s8 inet static
address 192.168.56.104
netmask 255.255.255.0
network 192.168.56.1

// hostname 수정
$ sudo vi /etc/hostname

hadoop04
// 리부팅


$ sudo vi /etc/hosts
127.0.0.1     localhost
192.168.56.101  hadoop01
192.168.56.102  hadoop02
192.168.56.103  hadoop03
192.168.56.104  hadoop04
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/hostsetting.png?raw=true)
<br><br>

hadoop02, hadoop03, hadoop04 에도 모두 같은 내용으로 hosts 파일 수정

hadoop01, hadoop02, hadoop03, hadoop04 모두 openssh-server 설치한다.

```
$ sudo apt-get install openssh-server
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/openssh_install.png?raw=true)
<br><br>


```
// 아래 부분은 hadoop01 에서만 실행
$ ssh-keygen -t rsa 

# 엔터 3번
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

$ ssh localhost 
# 처음 한번만 yes, 두번째 접속시 부터는 안 물어봄.

$ exit 
# exit 로 꼭 나와야 함

// hadoop02, hadoop03, hadoop04 에 키 복사
$ ssh-copy-id -i /home/hadoop/.ssh/id_rsa.pub hadoop@hadoop02
$ ssh-copy-id -i /home/hadoop/.ssh/id_rsa.pub hadoop@hadoop03
$ ssh-copy-id -i /home/hadoop/.ssh/id_rsa.pub hadoop@hadoop04

```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/ssh_keys.png?raw=true)
<br><br>


```
// 접속 잘 되는지 확인
$ ssh hadoop@hadoop02

//hadoop 1.2.1 다운로드
$ wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz

// 압축 해제
$ tar zxvf hadoop-1.2.1.tar.gz

$ cd hadoop-1.2.1/
$ cd conf
$ vi hadoop-env.sh

// 맨아래에 내용 추가
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export HADOOP_HOME=/home/hadoop/hadoop-1.2.1
export HADOOP_HOME_WARN_SUPPRESS="TRUE"

export HADOOP_HEAPSIZE=1024     // 메모리 설정
export HADOOP_PID_DIR=/home/hadoop/hadoop-1.2.1/pids

```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/path.png?raw=true)
<br><br>




```

$ vi core-site.xml

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->
<configuration>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://hadoop01:9000</value>
    </property>

    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/hadoop/hadoop-data</value>
    </property>
</configuration>

```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/conf.png?raw=true)
<br><br>


```
$ vi hdfs-site.xml

// dfs.replication : 복제갯수
 

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>3</value>    
    </property>

    <property>
        <name>dfs.http.address</name>
        <value>hadoop01:50070</value>
    </property>
    
    <property>
        <name>dfs.secondary.http.address</name>
        <value>hadoop02:50090</value>
    </property>
</configuration>
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/hdfs-site.png?raw=true)
<br><br>





```
// 맵리듀스 설정
$ vi mapred-site.xml

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->

<configuration>
    <property>
        <name>mapred.job.tracker</name>
        <value>hadoop01:9001</value>
    </property>
</configuration>
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/mapred-site.png?raw=true)
<br><br>




```
$ cd hadoop-1.2.1/conf
$ ls
// secondary namenode: hadoop02
// slaves : datanode. hadoop02, hadoop03, hadoop04

$ vi masters 
hadoop02
```
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/masters.png?raw=true)

```
$ vi slaves
hadoop02
hadoop03
hadoop04
```
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/slaves.png?raw=true)
<br><br>


```
// 맨 상위로 이동
$ cd ~

// hadoop-1.2.1 통째로 압축
$ tar zcvf hadoop.tar.gz hadoop-1.2.1 

// hadoop02, hadoop03, hadoop04로 복사
$ scp hadoop.tar.gz hadoop@hadoop02:/home/hadoop
$ scp hadoop.tar.gz hadoop@hadoop03:/home/hadoop
$ scp hadoop.tar.gz hadoop@hadoop04:/home/hadoop

// 압축풀기
$ ssh hadoop@hadoop02
$ tar zxvf hadoop.tar.gz
$ exit

$ ssh hadoop@hadoop03
$ tar zxvf hadoop.tar.gz
$ exit
$ ssh hadoop@hadoop04
$ tar zxvf hadoop.tar.gz
$ exit

// 하둡 경로 설정 
$ vim .bashrc
export HADOOP_INSTALL=/home/hadoop/hadoop-1.2.1
exprot PATH=$PATH:$HADOOP_INSTALL/bin
```

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/path_setting.png?raw=true)
<br><br>

```
$ exit


// 리부트
$ sudo reboot
// hadoop 실행
$ hadoop

// 반드시 hadoop01 에서 실행
$ hadoop namenode -format
$ start-all.sh

$ jps
JobTracker
Jps
NameNode 
// 3가지 떠있는 것 확인 가능
// 나머지 hadoop2,3,4에서도 동일 명령어로 확인 가능

// hadoop01, hadoop02, hadoop03, hadoop04 에서 jps 실행해서 확인
// hadoop01은 NameNode, JobTracker
// hadoop02은 SecondaryNameNode, DataNode, TaskTracker
// hadoop03은 DataNode, TaskTracker
// hadoop04은 DataNode, TaskTracker 가 보이면 OK

// 반드시 종료 시켜야 함
$ stop-all.sh 
```







브라우저로 http://hadoop01:50070 으로 접속해서 HDFS 확인

브라우저로  http://hadoop01:50030 으로 접속해서 MapReduce 확인

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/check1.png?raw=true)
<br><br>
![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/Hadoop/check2.png?raw=true)



