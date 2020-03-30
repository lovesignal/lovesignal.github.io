---
key: 20200331
title: "[MySQL] Stored Procedure 알아보기 (in MySQL)"
excerpt: "Stored Procedure in MySQL"
comments: true
tags: [MySQL]
categories: sql
---

## 1. 사전에 알아야할 용어

### 1.1 PL/SQL

**정의**

- Procedural Language extension to SQL
- PL/SQL은 상용 관계형 데이터베이스 시스템인 오라클 DBMS에서 SQL 언어를 확장하기 위해 사용하는 컴퓨터 프로그래밍 언어 중 하나이다.
- SQL의 확장된 개념으로 PL/SQL Block 내에서 SQLdml DML(데이터 조작어)문과 Query(검색어)문, 절차형 언어(IF, LOOP) 등을 하용하여 절차적 프로그래밍을 가능하게 한 트랜잭션 언어



### 1.2 PL/SQL BLOCK

> **정의**
>
> PL/SQL 소스 프로그램의 기본 단위를 **블록**(Block)이라고 하는데, 블록은 선언부, 실행부, 예외 처리부로 구성된다. 이 블록은 다시 이름이 없는 블록과 이름이 있는 블록으로 구분할 수 있는데 전자에 속하는 것이 익명 블록이며, 함수, 프로시저, 패키지 등이 후자에 속한다. PL/SQL의 블록 구조는 다음과 같다.
>
> ```
> 이름부
> IS(AS)
> 선언부
> BEGIN
> 실행부
> EXCEPTION
> 예외 처리부
> END;
> ```
>
> [출처]: https://thebook.io/006696/part02/ch08/01/01/	"오라클 SQL과 PL/SQL을 다루는 기술"



### 1.3 Procedure

- 정의: 특정 작업을 수행 하는, 이름이 있는 PL/SQL BLOCK 이다.



## 2. Stored Procedure

앞의 용어에 기반하여 설명하면,

- DB 내부에 저장된 일련의 SQL 명령문들을 하나의 함수처럼 실행하기 위한 쿼리의 집합이 Stored Procedure이다.
- 나중에 Query를 실행하기 위하여 DB Server에 Query를 저장할 때 stored procedure를 사용할 수 있다.



### 2.1 CREATE PROCEDURE

- `CREATE PROCEDURE` statement는 Query를 감싸는 새로운 stored procedure를 만든다.

```mysql
DELIMITER $$
 
CREATE PROCEDURE GetCustomers()
BEGIN
    SELECT 
        customerName, 
        city, 
        state, 
        postalCode, 
        country
    FROM
        customers
    ORDER BY customerName;    
END$$
DELIMITER ;
```

위 예시에서 `GetCustomers()` 라는 stored procedure를 MySQL 서버에 만들었다



### 2.2 CALL

- `CALL` 을 사용하여 저장된 stored procedure를 호출할 수 있다.
- 아래와 같이 호출하게 되면 작성해둔 query와 동일한 결과가 반환된다.

```mysql
CALL GetCustomers();
```

- Stored procedure를 처음 호출하면 MySQL은 DB의 catalog에서 이름을 찾아서 stored procedure의 코드를 compile하여 메모리 영역에 캐시로 저장한 후 stored procedure를 실행한다.
- 동일한 session에서 같은 stored procedure를 재호출 하면 MySQL은 기존에 있는 캐시로 실행한다. (컴파일을 다시 거치지 않음)
- Stored procedure에서 매개 변수가 있을 경우 값을 전달하고 결과를 다시 반환 받을 수 있다. 
  - e.g., 국가, 도시별 고객을 반환하는 stored procedure가 있다고 가정. 이 경우 국가, 도시는 stored procedure의 매개 변수이다.
- Stored procedure에는 IF, CASE, LOOP 등 control flow statements가 포함될 수 있다. 
- Stored procedure는  다른 stored procedure 또는 stored function을 호출하여 코드를 만들(modulize) 수 있다.



### 2.3 MySQL stored procedures advantages

#### Reduce network traffic

- Application과 MySQL Server 사이에 Network traffic을 줄이는데 도움이 된다. 
- 긴 SQL문을 여러 개 전송하지 않아도,  application이 stored procedure의 이름과 매개 변수만 보내면 된다.

#### Centralize business logic in the database

- 여러 application에서 재사용 가능한 비즈니스 로직을 만들 수 있기 때문에 동일한 로직을 복제하져는 노력을 줄일 수 있고 DB의 일관성을 향상시킬 수 있다.

#### Make database more secure

- 특정 stored procedure에 접근할 수 있는 권한만을 부여하여 기본 table을 더욱 안전하게 관리할 수 있다. 

### 2.4 MySQL stored procedures disadvantages

### Resource usages

- Stored procedure를 많이 사용할 경우 메모리 사용량이 증가할 수 있다.
- 또한, MySQL이 logical operations을 잘 할 수 있게 설계되지 않았기 때문에, stored procedure에서 과도하게 많은 연산을 할 경우 CPU 사용량이 증가할 수 있다.

#### Troubleshooting

- Stored procedure를 디버깅 하기 어렵다.
- MySQL은 stored procedure 디버깅 기능을 제공하지 않는다. (Oracle 같은 Enterprise DB는 제공)

#### Maintenances

- Stored procedure를 개발하고 유지, 관리하는데 개발 resource가 많이 필요하다. 그렇기 때문에 유지보수의 문제가 발생할 수 있다.

---

- 출처: https://www.mysqltutorial.org/introduction-to-sql-stored-procedures.aspx