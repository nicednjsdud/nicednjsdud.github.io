---
title: Database 6. DML 1 (SQL)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: SQL
tag : SQL
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-21 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

DML (Data Maniplation Language)
=================================

## DML
* 테이블의 데이터를 조작하는 기능
* 테이블의 레코드를 **CRUD(Create, Retrieve, Update, Delete)**

```
    - ABCD( add, browse, change, delete) 이라고도 함.
```

* **INSERT, DELETE, UPDATE, SELECT (SQL)**


### 데이터 직접 삽입

```sql
    INSERT INTO 테이블이름 [(속성들)] VALUES (속성값들)
```

```sql
INSERT INTO CUSTOMER VALUES ('strawberry','최유경',30,'vip','공무원',100);
```

![alt](/assets/images/post/Database/sql/2.png)

```sql
INSERT INTO CUSTOMER (cusid,cusName,grade) 
VALUES ('watermelon','이순신','vvip');
COMMIT;
```

* not null의 값만 채어 넣을 수 있다.

![alt](/assets/images/post/Database/sql/4.png)

* INSERT INTO 테이블이름 [(속성용)]
* VALUES (속성값들)

### 데이터 수정

```SQL
    UPDATE 테이블이름 SET 속성이름 1 = 값1, 속성이름 2 = 값2,
    [WHERE 조건]
```

```sql
    UPDATE ORDERSERVICE  SET count =5 WHERE ORDERID  IN   
    (SELECT cusid FROM CUSTOMER WHERE cusname ='정소화');
```

![alt](/assets/images/post/Database/sql/5.png)

### 데이터 삭제

```sql
    delete from 테이블이름 where [조건];
```

```sql
    DELETE FROM ORDERSERVICE 
    WHERE ORDERid IN (SELECT cusid FROM CUSTOMER WHERE cusname ='정소화');
```

## SELECT  

### 기본 검색 

```SQL
    SELECT [ALL | DISTINCT] 속성들
    FROM 테이블(들);
```

* ALL : 투플의 중복을 허용하도록 지정
* DISTINCT : 투플의 중복을 허용하지 않도록 지정

```sql
    select cusid, cusName,grade from customer;
```

![alt](/assets/images/post/Database/sql/6.png)

* AS 키워드를 이용해 결과 테이블에서 속성의 이름을 바꾸어서 출력 가능
    * AS 키워드 생략 가능

```sql
    select itemname, price as(생략 가능) 가격
    from item;
```

![alt](/assets/images/post/Database/sql/7.png)

#### 산술식을 이용해 검색
* 속성의 이름과 +,-,*,/ 등의 산술 연산자와 상수로 구성
* 속성의 값이 실제로 변경되는 것은 아님

```sql
    select itemname, price + 500 as 조정단가
    from item;
```

![alt](/assets/images/post/Database/sql/8.png)


### 조건 검색

```sql
    SELECT [ALL | DISTINCT] 속성들
    FROM 테이블(들)
    [WHERE 조건];
```

```sql
    select itemname as 제품명, remain as 재고량, price as 단가 
    from item
    where factory = '오뚜기';
```

![alt](/assets/images/post/Database/sql/9.png)


* WHERE 절에 비교 연산자, 논리 연산자를 이용한 검색 조건 제시

#### 비교연산자
* = , <> , < , > , <= , >=

#### 논리연산자
* AND , OR , NOT

#### LIKE 를 이용한 검색
* 부분적으로 일치하는 데이터를 검색
* 문자열을 이용하는 조건에만 LIKE 키워드 사용 가능
* 함께 사용할수 있는 기호
    * % : 0개이상의 문자( 문자의 내용과 개수는 상관 없음) 
    * _ : 1개의 문자 (문자의 내용은 상관 없음)

```SQL
    LIKE '이젠%' : '이젠'으로 시작하는 문자열 ('이젠'으로 시작하기만   
                하면 길이는 상관 없음) 
    LIKE '%이젠' : '이젠'으로 끝나는 문자열 ('이젠'으로 끝나기만 하면 길이는    
               상관 없음) 
    LIKE '%이젠%' : '이젠'이 포함된 문자열

    LIKE '이젠___'(3칸) : '이젠'으로 시작하는 5자 길이의 문자열

    LIKE '__이%'(2칸) : 3번째 글자가 '이'인 문자열
```

```sql
    SELECT cusname 고객이름, cusage 나이, grade 등급, point 적립금
    FROM CUSTOMER
    where cusname like '김%';
```

![alt](/assets/images/post/Database/sql/10.png)

#### NULL을 이용한 검색
* null은 empty가 아닌 unknown 
* is null 키워드를 이용해 특정 속성의 값이 널 값인지를 비교
* is not null 키워드를 이용해 특정 속의 값이 널 값이 아닌지를 비교
* 검색 조건에서 널 값은 다른 값과 크기를 비교하면 결과가 모두 거짓이 됨.

```sql
    select cusname 고객이름
    from customer
    where cusage is null;
```

![alt](/assets/images/post/Database/sql/11.png)

```sql
    select cusname 고객이름
    from customer
    where cusage is not null;
```

![alt](/assets/images/post/Database/sql/12.png)

* null값과 산술 연산 및 비교연산 결과는 null

```
     5 + null   returns null
    null > 5    returns null
    null = null returns null
```

##### null과 논리 연산 결과

```
- OR : ( null OR true ) = true
       ( null OR false) = null
       ( null OR null ) = null

- AND :(null AND true ) = null
       (null AND false) = false
       (null AND null ) = null

- NOT :(NOT null)       = null    
```