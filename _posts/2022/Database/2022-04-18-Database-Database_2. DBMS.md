---
title: 2.DBMS 
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: DBMS
tag : Database
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

DBMS
========

## 데이터베이스 관리 시스템 (DBMS)

* 응용프로그램은 데이터베이스 통해서 파일 시스템의 파일에  
  저장한 데이터에 접근한 것.

```
    - 응용프로그램과 데이터 파일 분리
```

### DBMS

![alt](/assets/images/post/Database/DBMS1.png)


* 응용프로그램과 데이터 연결을 도와주며 데이터 관리와 데이터에 대한  
  기본 처리를 담당하는 추가적인 소프트웨어
* 데이터베이스와 일름 관리하는 소프트웨어인 DBMS와 응용프로그램 모두들 칭하는 용어

```
    - 데이터 베이스 시스템
```

* 파일시스템의 데이터중복과 데이터 종속 문제를 해결하기 위해 제시된 소프트웨어
* 데이터베이스의 생성과 관리를 담당 
* 모든 응용 프로그램은 데이터베이스 공유 가능, DBMS 통해서 데이터 삽입, 수정, 검색.
* **OS와 함께 중요한 시스템 소프트웨어 패키지.**

### 대표적인 DBMS
* Oracle, MySQL, MS-SQL Server, PostgreSQL, SAP HANA

### 주요 기능

* 정의 기능 : 데이터베이스 구조 정의 및 수행
* 조작 기능 : 데이터를 삽입, 삭제, 수정, 검색하는 연산 수행
* 제어 기능 : 데이터를 항상 정확하고 안전하게 유지하는 기능

### DBMS 장점

* 파일시스템의 데이터 중복문제를 해결
* 데이터 독립성 확보 
* 데이터 동시 공유 (Concurrency control)
* 데이터 보안 향상 

```
    - 사용자 별 접근 가능한 데이터베이스 영역 제한 가능
```

* 데이터 무결성 유지
* 표준화 방식으로 데이터에 접근 (with DB 언어 - SQL)
* 장애 발생 후 회복시 데이터 일관성과 무결성 유지 - **트랜잭션 기능**

### DBMS 단점

* DBMS 구매 비용
* 응용 프로그래머가 DBMS가 어떻게 동작하는지와 SQL에 대한 지식 필요
* DBMS 장애가 발생할 때 모든 응용프로그램 장애가 발생함

## 용어

### Data Dictionary (System Catalog)

* DBMS는 database와 함께 metadata(data about data)을 저장함.
* 데이터 정의어(DDL)에 의해 생성됨.

### Metadata

* 각 데이터에 접근할 수 있는 데이터의 이름(테이블, 컬럼 이름)
* 스토리지에 데이터가 저장된 위치 
* 보안을 위한 제약 ( Sercurity Constraint )

```
    - 누가 어떤 데이터를 접근할 수 있나
```

* 무결성을 위한 제약 (intergrity constraint)

```
    - 어떤값이 데이터에 유효하느냐
```

### 스키마 (Schema)

* 데이터베이스에 저장되는 데이터의 논리적인구조와 제약 조건을 정의하는 것
* ex) 고객 schema

```
    - 고객번호      이름             나이       주소
        int       varchar(10)       int       varchar(100)
```

### 인스턴스 (instance)

* 정의된 스키마에 따라 데이터베이스에 실제로 저장된 값


## 데이터베이스 구조

### 3단계 데이터베이스 구조 
* **3 level database architecture**
* 미국 기관 ANSI/SPARC에서 일반 사용자가 데이터베이스를 쉽게 이용하고  
  사용할 수 있게 하는 구조 제안

```
                    End Users

External Schema    : External level    (외부 스키마)

Conceptural Schema : Conceptural level (개념 스키마)

Internal Schema    : Physical level    (내부 스키마)

                    DATABASE

```

![alt](https://mblogthumb-phinf.pstatic.net/MjAxNzEyMjNfNjgg/MDAxNTEzOTk4OTI2MzE0.v86gcDb5SegrLC4xNS0eU_0FNf43dUgn-UW83u5QxLAg.E_JpjpxkVH0F1bNKTiH8jqSSYmT3RzvGlJRAfOCBkiog.PNG.qbxlvnf11/20171223_121515.png?type=w800)

