---
title: Database 4. 관계형 데이터 모델 
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: 관계형 데이터 모델
tag : Database
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-19 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

관계형 데이터 모델
====================

## 데이터베이스 종류

### 1. 계층형 데이터베이스 

* 최조의 현대적 데이터베이스

### 2. 관계형 데이터 베이스 

* Relational Database (RDBMS)
* 2차원 표 형식으로 데이터 관리, 가장 널리 사용됨.
* 실생활에서 사용하는 모든 정보를 관계형 데이터베이스로 관리할 수 있음.

### 3. NOSQL 데이터베이스

* Not Only SQL 최근에 각광 받고 있음.

## 관계형 모델 ( Relational model )

* 집합론에 기반을 둔 일종의 데이터베이스 모델.
* 열(column) 과 행(row)을 이루는 하나 이상의 테이블이 존재하고 테이블에 데이터가 저장됨.

```
    - 열은 필드(Field) 혹은 속성 (Attribute)라고도 불림,
    - 행는 레코드 혹은 튜플(Tuple)로 불림.
```

* 각각의 테이블은 각각의 로우를 식별하는 기본 키(Primary Key)가 있음.

## 데이터 모델링 (data modeling)

* 현실 세계에 존재하는 데이터를 컴퓨터 세계의 데이터베이스로 옮기는 과정

```
    - 데이터베이스 설계의 핵심 과정
```

### 데이터 모델링 3단계

```
                     개념적 모델링
 현실세계 -------------------------------------> 개념적 데이터 모델
                                                     |
                                                     |  논리적 모델링
                                                     |
                     물리적 데이터 모델링             \|/
 데이터베이스 <--------------------------------- 논리적 데이터 모델   
 
```

#### 개념적 데이터 모델링

* 결과물로 개념적 데이터 모델 (E-R 모델)

![alt](/assets/images/post/Database/E-R.png)

#### 논리적 데이터 모델링

* 결과물로 관계 데이터 모델

## 관계 데이터 모델

* 개체(Entity)에 대한 데이터를 저장하는 논리적 구조

```
   - 릴레이션 (2차원 테이블 구조) 
```

![alt](/assets/images/post/Database/1.png)

* 집한론에 기반을 둔 일종의 데이터 베이스 모델
* 컬럼(열)과 로우(행)를 이루는 하나 이상의 테이블이 존재하고 이 테이블에 데이터가 저장됨.
* 각각의 테이블은 각각의 로우를 식별하는 기본키(Primary Key)가 있음.
* 컬럼은 필드(Field) 혹은 속성(Attribute)라고도 불린다.
* 로우는 레코드 혹은 튜플(Tuple)로 불림.



