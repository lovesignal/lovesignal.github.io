---
key: 20180224
title: "[Hadoop] Hadoop 설치 및 WordCount 예제 실습"
excerpt: "Hadoop 설치부터 WordCount 예제까지 실습"
categories: programming
comments: true
tag : [hadoop, data engineering]
---


## Hadoop

Hadoop = HDFS + MapReduce



### Mode 3가지

#### HDFS 설치방식

- Stand alone (독립실행모드) : 기본 실행모드. 분산저장 안함. 코딩은 가능.
- Pseudo-distributed (가상분산모드) : 하나의 컴퓨터에 설치
- Fully distributed (완전분산모드) : 여러 대의 컴퓨터에 설치



### 순서

1. VirtualBox 설치 
2. Ubuntu 14.04.2 설치 // 이후에는 VirtualBox 내의 Ubuntu 에서 진행
3. JDK 설치
4. 하둡 다운로드
5. 하둡 Stand-alone 모드 구성
6. 하둡 가상 분산 모드 구성
7. 이클립스 다운로드, 설정
8. WordCount 예제 코딩
9. 테스트



### Ubuntu에 JDK 8 설치

```

$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer

```



### 하둡 다운로드 후 압축 해제

URL : <https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz> 에서 다운로드



아래 명령어로 압축해제 및 설정.

참고 : 앞으로 나오는 /home/유저명/ 에서 "유저명" 부분은 "여러분 자신의 유저명"으로 수정하여 입력하면 된다. 



#### vim 설정

```
$ vi .vimrc

# 아래 내용 입력 후 저장
filetype plugin on
syntax on

set number
set paste

set ruler
set laststatus=2

$ cat .vimrc     # 확인
```





```
$ cd Downloads
$ cp hadoop-1.2.1.tar.gz ~       # ~ : home folder
$ cd ~
$ tar zxvf hadoop-1.2.1.tar.gz
$ sudo apt-get install vim

$ vim .bashrc # 맨 끝에 아래 3줄 추가

export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export HADOOP_INSTALL=/home/유저명/hadoop-1.2.1
export PATH=PATH:HADOOP_INSTALL/bin

$ source .bashrc # 변경 내용 적용
$ hadoop # 메시지가 정상 출력되면 OK
```



#### 하둡 Stand-alone 모드 구성 및 예제 테스트

아래 명령어로 테스트.

폴더명 중복 안되게 해야 한다.

```
$ cd /home/유저명/hadoop-1.2.1
$ mkdir input
$ cp README.txt input
$ hadoop jar hadoop-examples-1.2.1.jar wordcount input output
# cat output/part-r-00000 # 결과 확인

```

* jar : 파일을 실행하는 명령어

* hadoop-examples-1.2.1.jar 파일이 하둡 예제파일

* `$ hadoop jar hadoop-examples-1.2.1.jar wordcount input output` : hadoop / 파일실행 / 파일명 / 할일 /입력폴더 / 출력폴더

  ```
  # 출력 결과

  18/02/24 14:10:18 INFO util.NativeCodeLoader: Loaded the native-hadoop library
  18/02/24 14:10:18 INFO input.FileInputFormat: Total input paths to process : 1
  18/02/24 14:10:18 WARN snappy.LoadSnappy: Snappy native library not loaded
  18/02/24 14:10:18 INFO mapred.JobClient: Running job: job_local1707454656_0001
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: Waiting for map tasks
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: Starting task: attempt_local1707454656_0001_m_000000_0
  18/02/24 14:10:19 INFO util.ProcessTree: setsid exited with exit code 0
  18/02/24 14:10:19 INFO mapred.Task:  Using ResourceCalculatorPlugin : org.apache.hadoop.util.LinuxResourceCalculatorPlugin@415eb82d
  18/02/24 14:10:19 INFO mapred.MapTask: Processing split: file:/home/jane/hadoop-1.2.1/input:0+1366
  18/02/24 14:10:19 INFO mapred.MapTask: io.sort.mb = 100
  18/02/24 14:10:19 INFO mapred.MapTask: data buffer = 79691776/99614720
  18/02/24 14:10:19 INFO mapred.MapTask: record buffer = 262144/327680
  18/02/24 14:10:19 INFO mapred.MapTask: Starting flush of map output
  18/02/24 14:10:19 INFO mapred.MapTask: Finished spill 0
  18/02/24 14:10:19 INFO mapred.Task: Task:attempt_local1707454656_0001_m_000000_0 is done. And is in the process of commiting
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: 
  18/02/24 14:10:19 INFO mapred.Task: Task 'attempt_local1707454656_0001_m_000000_0' done.
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: Finishing task: attempt_local1707454656_0001_m_000000_0
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: Map task executor complete.
  18/02/24 14:10:19 INFO mapred.Task:  Using ResourceCalculatorPlugin : org.apache.hadoop.util.LinuxResourceCalculatorPlugin@2f017655
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: 
  18/02/24 14:10:19 INFO mapred.Merger: Merging 1 sorted segments
  18/02/24 14:10:19 INFO mapred.Merger: Down to the last merge-pass, with 1 segments left of total size: 1832 bytes
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: 
  18/02/24 14:10:19 INFO mapred.Task: Task:attempt_local1707454656_0001_r_000000_0 is done. And is in the process of commiting
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: 
  18/02/24 14:10:19 INFO mapred.Task: Task attempt_local1707454656_0001_r_000000_0 is allowed to commit now
  18/02/24 14:10:19 INFO output.FileOutputCommitter: Saved output of task 'attempt_local1707454656_0001_r_000000_0' to output
  18/02/24 14:10:19 INFO mapred.LocalJobRunner: reduce > reduce
  18/02/24 14:10:19 INFO mapred.Task: Task 'attempt_local1707454656_0001_r_000000_0' done.
  18/02/24 14:10:19 INFO mapred.JobClient:  map 100% reduce 100%
  18/02/24 14:10:19 INFO mapred.JobClient: Job complete: job_local1707454656_0001
  18/02/24 14:10:19 INFO mapred.JobClient: Counters: 20
  18/02/24 14:10:19 INFO mapred.JobClient:   Map-Reduce Framework
  18/02/24 14:10:19 INFO mapred.JobClient:     Spilled Records=262
  18/02/24 14:10:19 INFO mapred.JobClient:     Map output materialized bytes=1836
  18/02/24 14:10:19 INFO mapred.JobClient:     Reduce input records=131
  18/02/24 14:10:19 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=0
  18/02/24 14:10:19 INFO mapred.JobClient:     Map input records=31
  18/02/24 14:10:19 INFO mapred.JobClient:     SPLIT_RAW_BYTES=99
  18/02/24 14:10:19 INFO mapred.JobClient:     Map output bytes=2055
  18/02/24 14:10:19 INFO mapred.JobClient:     Reduce shuffle bytes=0
  18/02/24 14:10:19 INFO mapred.JobClient:     Physical memory (bytes) snapshot=0
  18/02/24 14:10:19 INFO mapred.JobClient:     Reduce input groups=131
  18/02/24 14:10:19 INFO mapred.JobClient:     Combine output records=131
  18/02/24 14:10:19 INFO mapred.JobClient:     Reduce output records=131
  18/02/24 14:10:19 INFO mapred.JobClient:     Map output records=179
  18/02/24 14:10:19 INFO mapred.JobClient:     Combine input records=179
  18/02/24 14:10:19 INFO mapred.JobClient:     CPU time spent (ms)=0
  18/02/24 14:10:19 INFO mapred.JobClient:     Total committed heap usage (bytes)=357564416
  18/02/24 14:10:19 INFO mapred.JobClient:   File Input Format Counters 
  18/02/24 14:10:19 INFO mapred.JobClient:     Bytes Read=1366
  18/02/24 14:10:19 INFO mapred.JobClient:   FileSystemCounters
  18/02/24 14:10:19 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=395714
  18/02/24 14:10:19 INFO mapred.JobClient:     FILE_BYTES_READ=290330
  18/02/24 14:10:19 INFO mapred.JobClient:   File Output Format Counters 
  18/02/24 14:10:19 INFO mapred.JobClient:     Bytes Written=1326


  ```

  ​



#### 하둡 가상분산 모드 구성

**5개의 프로세스** : Name node, Secondary Namenode, Data node, Job tracker, Tast tracker 

아래 순서로 네개 파일 수정해 준다.

 *  hadoop-env.sh : 환경변수 설정

 * core-site.xml : HDFS와 MapReduce에서 공통적으로 사용할 환경정보 설정

 * hdfs-site.xml : HDFS에서 사용할 환경정보 설정

 * mapred-site.xml : MapReduce에서 사용할 환경정보 설정





#### hadoop-env.sh 수정
JAVA_HOME 파라미터를 실제 JDK가 설치된 경로로 수정하는 작업
```
$ vim /home/유저명/hadoop-1.2.1/conf/hadoop-env.sh # 맨 끝에 3줄 추가

export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export HADOOP_HOME=/home/유저명/hadoop-1.2.1
export HADOOP_HOME_WARN_SUPPRESS="TRUE"  # Warning: $HADOOP_HOME is deprecated.

```



#### 보안 인증 관련 명령 실행

```
# 컴퓨터끼리 연결해서 접속할 수 있게 ssh 설정

$ sudo apt-get install openssh-server
$ sudo /etc/init.d/ssh restart # ssh 재실행
$ netstat -ntl # 0:::22 있으면 OK


# 접속할 때마다 비밀번호 묻지 않게 public key 공유(리눅스의 기능)

$ ssh-keygen -t rsa # 엔터 3번
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ ssh localhost # 처음 한번만 yes, 두번째 접속시 부터는 안 물어봄.
$ exit # exit 로 꼭 나와야 함
```



#### core-site.xml (하둡의 핵심 설정 파일) 편집

```
$ vim /home/유저명/hadoop-1.2.1/conf/core-site.xml

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/유저명/hadoop-1.2.1/hadoop-${user.name}</value>
    </property>
</configuration>
```
* fs.default.name : HDFS의 기본 이름을 의미. URI 형태로 사용.
* hadoop.tmp.dir : 하둡에서 발생하는 임시 데이터를 저장하기 위한 공간


#### hdfs-site.xml (하둡 분산 파일 관련 설정) 편집

```
$ vim /home/유저명/hadoop-1.2.1/conf/hdfs-site.xml

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration>
    <property>
        <name>dfs.name.dir</name>
        <value>/home/유저명/hadoop-1.2.1/dfs/name</value>
    </property>
    <property>
        <name>dfs.name.edits.dir</name>
        <value>${dfs.name.dir}</value>
    </property>
    <property>
        <name>dfs.data.dir</name>
        <value>/home/유저명/hadoop-1.2.1/dfs/data</value>
    </property>
</configuration>
```
* dfs.replication : HDFS의 저장될 데이터의 복제본 갯수를 의미. <br>
가상분산모드 : 1 <br>
완전분산모드 : 3

* dfs.http.address : 네임노드용 웹서버의 주소값. <br> 
기본값 : 0.0.0.0:50070
* dfs.secondary.http.address : 보조네임노드용 웹서버 주소값. <br> 
기본값 : 0.0.0.0:50090

#### mapred-site.xml (하둡 맵리듀스 관련 설정) 편집

```
$ vim /home/유저명/hadoop-1.2.1/conf/mapred-site.xml

<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration>
    <property>
        <name>mapred.job.tracker</name>
        <value>localhost:9001</value>
    </property>
    <property>
        <name>mapred.local.dir</name>
        <value>${hadoop.tmp.dir}/mapred/local</value>
    </property>
    <property>
        <name>mapred.system.dir</name>
        <value>${hadoop.tmp.dir}/mapred/system</value>
    </property>
</configuration>
```
* mapred.job.tracker : JobTracker 데몬의 주소를 의미. 데이터 노드에서 이 주소로 맵리듀스 작업을 요청.


#### namenode 포맷 ( namenode 는 처음에 꼭 한번 만 포맷해야 한다.)

```
$ hadoop namenode -format
```



#### 하둡 시작 및 확인

```
$ cd /home/유저명/hadoop-1.2.1
$ bin/start-all.sh
```



#### 하둡 프로세스 확인

```
$ jps # 5개의 프로세스 출력되면 OK : namenode, secondarynamenode, datanode, jobtracker, tasktracker

# 브라우저에서 접속해서 확인

URL : http://localhost:50070/dfshealth.jsp   // HDFS 확인
URL : http://localhost:50030/jobtracker.jsp // MapReduce 확인
```





### 이클립스 다운로드, 설정

#### 이클립스 다운로드

URL : <http://www.eclipse.org/downloads/> 로 접속

Eclipse IDE for Java Developers 를 다운로드



#### 압축해제

```
$ cd Downloads
$ tar zxvf eclipse-java-luna-SR2-linux-gtk-x86_64.tar.gz
```



#### 이클립스를 사용하여 Maven 프로젝트 생성

##### Maven에 대한 이해

https://www.slideshare.net/sunnykwak90/ss-43767933



##### 이클립스 실행

파일 (탐색기)를 이용해서 eclipse 폴더의 eclipse 파일을 더블 클릭해서 실행



##### Maven Project 생성

File -> New -> Project -> Maven -> Maven Project 선택

-> [Next] -> [Next] -> [Next] ->

Group Id : kr.co.mycompant.hd

Artifact Id : wcount

-> [Finish]



##### pom.xml 수정해서 하둡 jar 파일 설정

pom.xml 을 열어서 <dependencies> 와 </dependencies> 사이에 아래 내용을 입력

의미 : 하둡 1.2.1 관련된 jar 파일들을 자동으로 다운로드해서 환경 설정

```
<dependency>
  <groupId>org.apache.hadoop</groupId>
  <artifactId>hadoop-core</artifactId>
  <version>1.2.1</version>
</dependency>
```

![Hadoop_pom_xml](https://github.com/lovesignal/lovesignal.github.io/blob/master/_site/img/post/2018/Programming/Hadoop_pom_xml.png?raw=true)





### WordCount 예제 코딩

#### WordCount 클래스 생성

![Hadoop_class](https://github.com/lovesignal/lovesignal.github.io/blob/master/_site/img/post/2018/Programming/Hadoop_wordcount_class.png?raw=true)

sr/main/java 밑의 kr.co.mycompany.hd.wcount 에서

우클릭해서 -> New -> Class : WordCount -> [Finish]

아래 소스를 입력

```Java
package kr.co.mycompany.hd.wcount;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

public class WordCount {
  public static class MyMapper
    extends Mapper<LongWritable, Text, Text, LongWritable> {
    private final static LongWritable one = new LongWritable(1);
    private Text word = new Text();
    @Override
    public void map(LongWritable key, Text value, Context context)
        throws IOException, InterruptedException {
      String line = value.toString();
      StringTokenizer tokenizer =
        new StringTokenizer(line, "\t\r\n\f|,.()<> ");
      while(tokenizer.hasMoreTokens()) {
        word.set(tokenizer.nextToken().toLowerCase());
        context.write(word, one);
      }
    }// map
  }// MyMapper
  public static class MyReducer
    extends Reducer<Text, LongWritable, Text, LongWritable> {
    private LongWritable sumWritable = new LongWritable();
    @Override
    protected void reduce(Text key, Iterable<LongWritable> values,
        Context context)
        throws IOException, InterruptedException {
      long sum = 0;
      for(LongWritable val : values) {
        sum += val.get();
      }
      sumWritable.set(sum);
      context.write(key, sumWritable);
    }// reduce
  }// MyReducer
  public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    Job job = new Job(conf, "WordCount");

    job.setJarByClass(WordCount.class);
    job.setMapperClass(MyMapper.class);
    job.setReducerClass(MyReducer.class);

    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(LongWritable.class);

    job.setInputFormatClass(TextInputFormat.class);
    job.setOutputFormatClass(TextOutputFormat.class);

    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));

    job.waitForCompletion(true);
  }// main
}// end
```



##### 코드 설명

![WordcountExample](https://github.com/lovesignal/lovesignal.github.io/blob/master/_site/img/post/2018/Programming/WordcountExample.png?raw=true)



```Java
package kr.co.mycompany.hd.wcount;

public class WordCount {
  public static class MyMapper
    extends Mapper<LongWritable, Text, Text, LongWritable> {
    // Mapper를 상속받음 <KEYIN, VALUEIN, KEYOUT, VALUEOUT>
    
    private final static LongWritable one = new LongWritable(1);
    // final로 정의(상수). 공유하기 위해 static. 1을 담음. 어떤 단어가 한 번 나올 때 1이 들어가는 용도
    
    private Text word = new Text();
    // 단어 담는 용도. 이 위치에서 생성하는 게 성능 향상에 도움이 됨. 
    // Map에 생성되면 갯수만큼 호출되므로 매번 객체생성. Map에서는 객체 생성 안함. Map 들어가기 전에 생성.
    
    @Override  
    public void map(LongWritable key, Text value, Context context)
    // Text value : 텍스트가 한 줄씩 들어옴
    // Context : 나와 하둡의 연결고리
    
        throws IOException, InterruptedException {
      String line = value.toString();
      // String으로 바꿔야 자바에서 자료 관리가 가능하므로 변경
      // toStirng : String으로 바꿔줌
      
      StringTokenizer tokenizer = new StringTokenizer(line, "\t\r\n\f|,.()<> ");
      // StringTokenizer<String, 구분자>, 구분자 맨 뒤에 공백 있음.
      // Dear Bear River
      
      while(tokenizer.hasMoreTokens()) {
        word.set(tokenizer.nextToken().toLowerCase());
        context.write(word, one);
      // hasMoreTokens() : 반복문 돌면서 'hello hadoop world'
      // -> 3개로 끊어짐. 'hello', 'hadoo', 'world'
          
      // word.set : 하나씩 담음
      // nextToken : 다음 토큰 가져옴
      // toLowerCase : 대소문자 구분 안하기 위해 모두 소문자로 변경
      
      // context.write(word, one) : 단어 기록. (ex) 'hello'가 1번 나왔다 : ('hello', 1)
          // 첫번째 루프 : Deer, 1 / 두번째 루프 : Bear, 1 / 세번째 루프 : River 1
      }
    }// map
  }// MyMapper
  
  
  // Reducer
  public static class MyReducer
    extends Reducer<Text, LongWritable, Text, LongWritable> {
    // Reducer <KEYIN, VALUEIN, KEYOUT, VALUEOUT>  
      
    private LongWritable sumWritable = new LongWritable();
    
    @Override
    protected void reduce(Text key, Iterable<LongWritable> values,
        Context context)
    // Iterable : 반복자
        
        throws IOException, InterruptedException {
      long sum = 0;
      for(LongWritable val : values) {
        sum += val.get();
      }
      // 반복문 돌면서 LongWritable로 하나씩 가져온다.
      // 배열로 두개가 들어온다고 생각(그림의 Shuffling 부분 참고). (ex) Bear[1, 1]
      
      sumWritable.set(sum);
      // 더해 줌
        
      context.write(key, sumWritable);       
    }// reduce
  }// MyReducer
    
 
  // Main method
  public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    // Configuration : 환경설정
   
    Job job = new Job(conf, "WordCount");
    // Job : MapReduce의 Job

    job.setJarByClass(WordCount.class);
    job.setMapperClass(MyMapper.class);
    job.setReducerClass(MyReducer.class);

    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(LongWritable.class);

    job.setInputFormatClass(TextInputFormat.class);
    job.setOutputFormatClass(TextOutputFormat.class);

    FileInputFormat.addInputPath(job, new Path(args[0]));  // 입력폴더
    FileOutputFormat.setOutputPath(job, new Path(args[1]));  // 출력폴더

    job.waitForCompletion(true);
  }
}// end
```



#### 예제를 Maven Install 로 ~.jar 파일로 패키징한다.

프로젝트 우클릭 -> Run As -> 8 Maven install

target 폴더에 wcount-0.0.1-SNAPSHOT.jar 이 생성된다.



### 하둡 가상 분산 모드에서 생성된 jar 을 사용하여 WordCount 실행, 테스트

* wcount-0.0.1-SNAPSHOT.jar 파일을 /home/유저명/hadoop-1.2.1 폴더에 복사한다.
* hadoop fs 명령을 사용하여 테스트할 파일을 복사한다.

```
$ hadoop fs -put READEME.txt .
```



#### hadoop jar 명령을 사용하여 예제를 실행/테스트한다.

```
$ hadoop jar wcount-0.0.1-SNAPSHOT.jar kr.co.mycompany.hd.wcount.WordCount README.txt output1
```



#### 결과가 output1 폴더에 part-r-00000 이라는 파일로 저장된다.

hadoop fs -cat 명령어를 통해서 학인 할 수 있다.

```
$ hadoop fs -cat output1/part-r-00000
```







#### wc : wordcount 명령어 

단어수 31,  줄 179, 크기 1366 

![linux](https://github.com/lovesignal/lovesignal.github.io/blob/master/_site/img/post/2018/Programming/linux.png?raw=true)





[참고문헌]

https://blog.naver.com/sungback/220381870733

https://www.slideshare.net/sunnykwak90/ss-43767933

http://naver.me/IDMfcGl3

https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html