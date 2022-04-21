---
title: Database 5. DDL (SQL)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: 데이터베이스 시스템 언어
tag : SQL
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

DDL
====

## SQL ( Structured Query Language )

* 관계형 데이터베이스 (RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적 프로그래밍 언어
* 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를  
  위해 고안됨.
* 많은 수의 데이터베이스 관련 프로그램들이 SQL을 표준으로 채택하고 있음.
* 데이터에 구조화된( = 사전에 지정된 ) 질문을 하는 언어
* 대소문자 구별하지 않음

## SQL의 용도

```
    사용자 <---> SQL 작성 및 명령 수행 <---> DBMS (시스템 소프트웨어) <---> 데이터베이스
```

## ORACLE 계정 생성

### 오라클 구 버전 방식으로 사용자 계정 생성을 위한 설정

```sql
  ALTER SESSION SET "_ORACLE_SCRIPT" = TRUE ; -- 사용자 계정 생성을 위한 설정

  CREATE USER EZEN IDENTIFIED BY 0824;		-- "ezen" 사용자 계정을 생성
  ALTER USER ezen account unlock;
  GRANT CONNECT, RESOURCE, DBA TO ezen;		-- "ezen" 사용자 계정에게 권한 줌
```

### 테이블 스페이스

```sql
    CREATE tablespace ezen_data
    datafile 'C:\app\ezen\product\18.0.0\oradata\XE\ezen_data.dbf' SIZE 2G
    autoextend ON NEXT 512M maxsize unlimited
    logging
    ONLINE 
    permanent
    extent management LOCAL autoallocate
    blocksize 8K
    segment SPACE management auto
    flashback ON;
```

### temp

```sql
    CREATE TEMPORARY tablespace ezen_temp
    tempfile 'C:\app\ezen\product\18.0.0\oradata\XE\ezen_temp.dbf' SIZE 500M
    autoextend ON NEXT 100M maxsize unlimited;
```

* 생성한 테이블 스페이스를 ezen 사용자 계정의 default 테이블 스페이스로 지정

```sql
    ALTER USER ezen DEFAULT tablespace ezen_data;
    ALTER USER ezen TEMPORARY tablespace ezen_temp;
```

## DDL (Data Definition Language)

### 데이터 정의어

* DB, 테이블의 스키마를 정의, 수정하는 기능
* 테이블 생성, 컬럼 추가, 타입 변경, 각종 제약조건 지정, 수정 등

### 1. CREATE TABLE
* 테이블 생성

```sql
    CREATE TABLE 테이블이름 (
        속성이름  데이터타입 [NOT NULL][DEFAULT 기본값]
        [PRIMARY KEY(속성)]
        [UNIQUE (속성)]
        [FOREIGN KEY(속성) REFERENCES 테이블이름(속성)]
        [ON DELETE 옵션]
        [CONSTRAINT 이름]
        [CHECK(조건)]
    );
```

#### NOT NULL
* 속성이 널 값을 허용하지 않음을 의미하는 키워드

#### DEFAULT
* 속성의 기본 값을 지정하는 키워드

#### PRIMARY KEY
* 기본키를 지정하는 키워드

#### FOREIGN KEY
* 참조 무결성 제약조건 유지를 위해 참조되는 테이블에서 투플(행) 변경 시 처리 방법을  
  지정 

- on update no action : 투플을 변경하지 못하게 함.
- on update cascade : 관련 투플에서 외래키 값을 함께 변경함.
- on update ser null : 관련 투플의 외래키 값을 null로 변경함.
- on update set default : 관련 투풀의 외래키 값을 미리 지정한 기본값으로 변경함.

#### CHECK
* 테이블에 정확하고 유효한 데이터를 유지하기 위해 특정 속성에 대한 제약조건을 지정


```sql
    CREATE TABLE customer (
	cusID varchar(20) NOT NULL,
	cusName varchar(10)NOT NULL, 
	cusAge int,
	grade varchar(10)NOT null,
	job   varchar(20),
	point int DEFAULT 0,
	PRIMARY key(cusID)
);
```

![alt](/assets/images/post/Database/sql/1.png)

### 2. DROP TABLE
* 테이블 삭제

```sql
    DROP TABLE CUSTOMER;
```

```sql
    ex) alter table customer drop constraint check_age;
```

#### 만약, 삭제할 테이블을 참조하는 테이블 있다면?

* 테이블 삭제가 수행되지 않음
* 관련된 외래키 제약조건을 먼저 삭제해야 함




### 3. ALTER TABLE
* 테이블 변경

#### 새로운 속성 추가

```sql
    alter table 테이블이름 add 속성이름 데이터타입 [not null] [default]
```

```sql
    ex)  alter table customer add createDate date;
```

#### 기존 속성 삭제

```sql
    alter table 테이블이름 drop column 속성이름;
```

```sql
    ex)  alter table customer drop column createDate;
```

##### 만약, 삭제할 속성과 관련된 제약조건이 존재하면 
* 속성 삭제가 수행되지 않음
* 관련된 제약조건을 먼저 삭제해야 함

#### 새로운 제약조건 추가

```sql
    alter table 테이블이름 add constraint 제약조건이름 제약조건내용;
```

```sql
    ex) alter table customer add constraint check_age check (cusage >= 20) ;
```

#### 기존 제약조건 삭제

```sql
    alter table 테이블이름 drop constraint 제약조건이름;
```

```sql
    ex) alter table customer drop constraint check_age;
```

### 속성의 데이터 타입

#### VARCHAR(n)
* 최대길이가 n인 가변길이의 문자열 

#### INT
* 정수

#### DATE
* 연,월,일로 표현되는 날짜

