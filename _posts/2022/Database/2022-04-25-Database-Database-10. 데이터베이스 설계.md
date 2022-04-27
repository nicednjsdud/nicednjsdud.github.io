---
title: Database 9. 데이터베이스설계
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: Database
tag : Database
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Datebase
============

## RDBMS의 대표적인 설계 방법 

* 프로젝트 생명주기

### 1) E-R 모델을 이용한 설계

#### 1 단계 : 요구사항 분석

* 결과물 : 요구 사항 명세서

#### 2 단계 : 개념적 설계 

* 결과물 : 개념적 스키마 ( E - R 다이어그램 )

#### 3 단계 : 논리적 설계

* 결과물 : 논리적 스키마 ( 릴레이션 스키마 ) 

#### 4 단계 : 물리적 설계

* 결과물 : 물리적 스키마

#### 5 단계 : 구현 (개발)

* SQL 문 작성한 후 이를 DBMS에서 실행하여 DB 생성

### 2) 정규화를 이용한 설계

## 설계 1 단계 

### 요구사항 분석

* 요구 사항을 수집하고 분석하여 업무에 필요한 데이터가 무엇인지, 그 데이터에  
  어떤 처리가 필요한지 등을 고려.

```
    - 주요 사용자의 범위 결정
    - 수행하는 업무 분석
    - 인터뷰, 설문조사, 관련 문서 분석 등 방법을 이용해 요구 사항 수집.
```

## 설계 2 단계

### 개념적 설계

* DBMS에 독립적인 개념적 스키마 설계
* 요구 사항 분석 결과물을 개념적 데이터 구조로 표현

```
    - E-R 모델을 많이 사용 ( E-R 다이어그램 )
```

#### 주요 작업
* 중요한 개체 추출 

```
    - ex) 병원 DB 개발에 필요한 개체 (명사)
        - 병원 운영에 필요한 사람 : 환자, 의사, 간호사 등
        - 병원 운영에 필요한 사물 : 병실, 수술실, 의료 장비 등

    - 찾아낸 명사를 개체와 속성으로 분류
      ex) 싸다 마트에 회원으로 가입하려면 회원아이디, 비밀번호, 이름,
          --------   ----              ---------- -------- -----
          나이, 직업을 입력해야 한다.
          ---   --- 

          가입한 회원에게는 등급과 적립금이 부여된다.
                           ----   -----    
```

##### 개체 간의 관계

* 개체 간의 의미는 연관성
* 요구 사항 문제에서 개체 간의 연관성을 의미 있게 표현한 동사를 찾는다.

```
    - 일대일(1:1), 일대다(1:n), 다대다(n:m)
    - 필수적 / 선택적
```







## 데이터 모델링(Modeling)

* 단순화 시켜 표현하는 것
* 명확하게 하는 것
* 추상화된 반영

## 데이터 모델링의 세가지 관점

### 데이터 관점 ( Data, What )

* 업무가 어떤 데이터와 관련이 있는지, 데이터간의 관계는 무엇인지 

### 프로세스 관점 ( Process, How )

* 업무가 실제하고 있는 일은 무엇인지, 무엇을 해야하는지

### Data vs Process 관점

* 업무가 처리하는 일의 방법에 따라 데이터는 어떻게 영향을 받고 있느냐

## 데이터 모델링의 3가지 요소

* 업무가 어떤 것 (Things)
* 어떤 것이 가지는 성격 (Attributes)
* 업무가 관여하는 어떤 것간의 관계 (Relationship)

## 데이터 모델링 용어

### 1) 어떤 것 (Things)

* 엔티티 (Entity) , 인스턴스 (instance)

### 2) 어떤 것 간의 성격

* 속성 (Attributes) , 속성값 (Attributes Value)

### 3) 어떤 것간의 관계 

* 관계(Relationship), 페어링 (Pairing)

## 데이터 모델링 작업 순서

### 1) 엔티티를 그린다.

![alt](/assets/images/post/Database/sql/48.png)


### 2) 엔티티를 적절하게 배치한다.

### 3) 엔티니간 관계를 설정한다.

![alt](/assets/images/post/Database/sql/49.png)

### 4) 관계명을 기술한다.
### 5) 관계의 참여도, 필수 여부를 기술한다.

![alt](/assets/images/post/Database/sql/50.png)
![alt](/assets/images/post/Database/sql/51.png)


