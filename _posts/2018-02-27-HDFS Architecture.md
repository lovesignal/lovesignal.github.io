---
key: 20180227
title: "[Hadoop] HDFS Architecture"
excerpt: "HDFS의 기본 구조에 대해 정리"
categories: programming
comments: true
tag : [hadoop, data engineering]
---






## [Programming] HDFS Architecture

![](https://github.com/lovesignal/lovesignal.github.io/blob/master/img/post/Programming/HDFS%20Architecture.png?raw=true)



1. 파일 저장, 읽기 : 어플리케이션에서 클라이언트로 파일 저장 또는 읽기 요청
2. Client : application 요청에 의해 client가 NameNode에 데이터 블록의 위치를 조회 
3. NameNode에게 받은 Data block 위치를 통해 Client가 데이터를 직접 조회
4. Heart beat : DataNode가 상태를 주기적으로 보고(일종의 출석체크).



* Secondary NameNode

  NameNode가 망가지면 데이터가 어디에 저장되어 있는지 알 수 없기때문에 읽어들일 수 없으므로, NameNode를 백업해 두었다가 NameNode가 망가지면 다시 복구해 주는 역할

  ​

* HDFS와 MapReduce는 둘다 Master/Slave 구조

  **HDFS**

  - Master : Name node(메타정보관리)
  - Slave : Data node(실제 데이터)

  **MapReduce**

  - Master : JobTracker(TaskTracker의 상태 및 전체 작업의 진행 상황등을 지속적으로 감시하며 일 시적인 장애에 대해 자동 복구 기능 제공)

  - Slave : TaskTracker

  - Map Task

    레코드 단위로 처리해야 하는 작업을 담당

  - Reduce Task

    관련된 데이터 끼리 묶어서 처리해야 하는 작업 담당

  MapReduce만 코딩. 나머지는 자동.



- Node : 컴퓨터 한 대라고 생각하면 됨.
- Name Node, Data Node : HDFS 컨트롤 
- Job tracker, task tracker : MapReduce 컨트롤





