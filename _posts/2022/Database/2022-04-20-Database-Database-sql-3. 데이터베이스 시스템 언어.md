---
title: Database 3. 데이터베이스 시스템 언어
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: 데이터베이스 시스템 언어
tag : Database
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Database System Language
===========================

## 데이터베이스 사용자

### 데이터베이스 관리자 (DBA)

* 데이터베이스 시스템을 운영하고 관리
* 데이터베이스를 설계 및 구축, 제어
* DBMS 자체는 물론 데이터 베이스 구축, 관리에 해박한 지식과 많은 경험이 요구됨.

### 응용 프로그래머

* 데이터베이스 언어를 이용하여 응용프로그램을 작성

### 최종 사용자 (End User)

* 데이터베이스에 접근하여 데이터를 조작

![alt](/assets/images/post/Database/DBMS2.png)

## 데이터 언어

* 사용자가 데이터베이스를 구축하고 이에 접근하기 위해 데이터베이스   
  관리 시스템과 통신하는 수단

### 데이터 언어 종류
#### 1. 데이터 정의어 (DDL)
* 스키마 구조와 제약조건 등을 정의, 수정, 삭제

```SQL
  create table employ (
            ID char(5),
            name varvhar(20),
            department varchar(20),
            salary numberic(8,2),
            primary key(ID)
    );
```

#### 2. 데이터 조작어 (DML)
* 데이터의 삽입, 삭제, 수정, 검색

#### 3. 데이터 제어어 (DCL)
* Data Control Language
* 내부적으로 필요한 규칙 (보안, 무결성 체크) 등을 정의하는 데이터 언어
* DB나 테이블의 접근권한이나 CRUD 권한을 정의하는 기능
* 특정 사용자에게 테이블의 조회권한 허가/ 금지 등

```
  - GRANT : 데이터베이스 객체에 권한을 부여
  - REVOKE : 이미 부여된 데이터베이스 객체 권한을 취소한다.
```
