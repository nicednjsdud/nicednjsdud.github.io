---
title: (컴퓨터 개론) 10-2 DBMS와 관계형 DB
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: DBMS와 관계형 DB
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2023-01-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - DBMS와 관계형 DB

## 1. DBMS

- 기업이나 기관에서 필요한 데이터들을 **통합적**으로 구성하여 저장, 관리해주는 소프트웨어 **패키지**

### 1) DMBS의 개념

#### (1) 데이터 베이스 사용 환경 : DBMS

- 기업이나 기관이 요구하는 모든 데이터를 **통합적**으로 구성하여 저장, 관리해주는 소프트웨어 시스템
- 물리적 데이터베이스와 논리적(개념적 구성) 데이터베이스를 관리
- DBMS, 데이터베이스, 일반 사용자 및 응용 프로그램간의 관계를 연계 및 **통합적** 관리

![alt](/assets/images/post/ComputerStudy/508.png)

#### (2) 데이터 독립성 (Date Independence)

- 데이터베이스의 논리적 구조(또는 개념적 구조)와 물리적 구조가 변경되더라도 응용 프로그램은 영향을 받지 않음

![alt](/assets/images/post/ComputerStudy/509.png)

#### (3) 데이터의 독립성과 데이터 구조 간의 사상 개념

![alt](/assets/images/post/ComputerStudy/510.png)

### 2) DBMS의 3대 기능

#### (1) 데이터베이스의 정의 - DDL

- 응용 프로그램이 데이터베이스를 인터페이스 할 수 있도록 하기 위해 데이터 **정의어**  
  (DDL : Data Definition Language)를 이용
- 데이터베이스의 논리적 구조를 정의
- 데이터베이스의 물리적 구조 명세를 정의

#### (2) 데이터베이스의 조작 기능 - DML

- 데이터의 검색, 갱신, 삽입, 삭제를 용이하고 효율적으로 수행할 수 있는 데이터 **조작어**
- 데이터 조작언어(DML: Data Manipulation Language)는 응용 프로그래머가 사용

#### (3) 데이터베이스의 제어 기능 - DCL

- **데이터베이스를 정확하고 안전하게 유지하기 위한 데이터 제어언어(DCL: Data Control Language)이용**

##### (3-1) 데이터 일관성 (Data Consistency)

- 불일치 현상 방지

##### (3-2) 데이터 무결성 (Data Itegrity)

- 데이터의 정확성 또는 유효성 유지
- 접근 권한을 검사하여 보안지원
- DBMS의 구조

![alt](/assets/images/post/ComputerStudy/511.png)

#### (4) DMBS의 장점 - 데이터베이스를 통합적으로 관리

- 데이터의 공유와 데이터베이스의 효율적 관리
- 데이터 중복의 배제
- 데이터의 일관성 유지
- 데이터의 무결성
- 데이터 보안의 유지

### 3) 데이터 모델

#### (1) 데이터 모델의 개념

1. 데이터베이스는 지속적으로 변화하는 **현실 세계를** 데이터로 표현
2. 개념적 모델링(Conceptual Modeling)

- (2.1) 인간은 현실 세계에 존재하는 다양한 개체들과 **객체 간의 관계**를 개념적으로 명확히 이해 하기 위하여  
  추상적으로 표현

3. 논리적 구조(**논리적 스키마**)를 형성하는 데이터 모델이 DBMS모델에 따라 다름
4. 데이터베이스의 개념적 구조와 물리적 구조 간에 사상

![alt](/assets/images/post/ComputerStudy/512.png)

#### (2) DBMS의 발전

##### (2-1) 제 1세대 DBMS

- 최초이 DBMS : 1960대 초 GE사의 IDS, 네트워크 모델의 기초
- 1960년대 후반, IBM사의 **IMS** : 계층적 데이터 모델 개념

##### (2-2) 제 2세대 DBMS

- 1970년 IBM San Jose 연구소의 E.F. Codd : **관계형** 데이터 모델
- 관계형 데이터 모델은 DBMS 발전에 획기적인 전환점
- 1980년 이후 **대부분**의 DBMS는 관계형 데이터 모델
- 표준 데이터베이스 **질의 언어 SQL**

##### (2-3) 1990년대, 다양한 멀티미디어 응용 분야

- 객체지향 데이터베이스 (OODBMS) : Object-Oriented DBMS
- 객체-관계 데이터베이스 (ORDMBS) : Oject-Relational DBMS

### 4) 데이터 모델의 종류

#### (1) 계층형 데이터 모델

- **트리 구조를** 기반으로 함
- 상위 레코드와 하위 레크드 간에 부모-자식 관계 존재

![alt](/assets/images/post/ComputerStudy/513.png)

#### (2) 네트워크 데이터 모델

- 레코드들 간에 그래프를 기반으로 구성
- 레코드들이 링크에 의해 상호 연결, 데이터 구조의 변경이 어렵고 새로운 프로그램의 목적을 만족시키기 어려운 한계성

![alt](/assets/images/post/ComputerStudy/514.png)

#### (3) 관계형 데이터 모델

- 1970년 IBM사의 에드가 카드(E.F. Codd)가 제안
- 관계(Relation): 테이블(Table) 개념과 대수에 기반

![alt](/assets/images/post/ComputerStudy/515.png)

#### (4) 객체지향 데이터 모델

- 1980년대 후반, 객체지향 모델 등장

##### (4-1) 객체지향 프로그래밍 패러다임에 기반

- 객체(Object), 속성(Attribute), 메소드(Method), 클래스(Class), 클래스 계층 및 상속 개념
- 객체의 캡슐화

![alt](/assets/images/post/ComputerStudy/516.png)

## 2. 관계형 DB

- 현재 널리 활용되는 데이터 모델은 관계형 DB

### 1) 관계형 DB의 구조

#### (1) 테이블의 열(Column)과 행(Row)

- 관계(Relation), 속성(Attribute), 튜플(Tuple) 개념
- 수학적 관계 및 **집합 이론에** 근거

![alt](/assets/images/post/ComputerStudy/517.png)

#### (2) 관계 데이터베이스의 구성 예

![alt](/assets/images/post/ComputerStudy/518.png)

#### (3) 정규화 관계(Normalized Relation)의 특성

- 한 관계에 포함된 튜플은 모두 상이함 (**튜플의 유일성**)
- 한 관계에 포함된 튜플 사이에는 순서가 없음 (**튜플의 무순서성**)
- 한 관계를 구성하는 속성 사이에 순서가 없음 (**속성의 무순서성**)
- 모든 속성값은 더 이상 분해할 수 없는 **원자값**을 가짐

#### (4) 후보 키(Candidate Key): K

- 관계의 키(Key) : 튜플을 유일하게 **식별**할 수 있는 속성의 집합

##### (4-1) 유일성

- 관계 R의 모든 튜플에 대해 **K의 값은** 상이하고 유일함

##### (4-2) 최소성

- 후보 키는 모든 튜플을 유일하게 식별하기 위한 **최소의 속성을** 가짐

### 2) 관계 대수

![alt](/assets/images/post/ComputerStudy/523.png)

#### (1) 집합 연산

- 합집합 연산(Union)
- 교집합 연산(Intersection)
- 차집합 연산(Difference)
- 카디션 프로덕트 연산 (Cartesian Product)

##### (1-1) 합집합 연산 (UNOIN: U)

```sql
  B U C
```

##### (1-2) 교집합 연산 (INTERSECTION)

```c
  B n C
```

![alt](/assets/images/post/ComputerStudy/524.png)

##### (1-3) 차집합 연산(DIFFERENCE)

```c
  B - C
```

![alt](/assets/images/post/ComputerStudy/525.png)

#### (2) 순수한 관계 연산

- 선택 연산 (Select)
- 추출 연산 (Project)
- 조인 연산 (Join)

##### (2-1) 선택 연산 (SELECT)

```sql
  select from a where a.n = 7;
```

![alt](/assets/images/post/ComputerStudy/519.png)

##### (2-2) 추출 연산 (PROJECT)

```sql
  project m, n from A;
```

![alt](/assets/images/post/ComputerStudy/520.png)

##### (2-3) 조인 연산 (JOIN)

```sql
  JOIN A and B where A.L = B.P;
```

![alt](/assets/images/post/ComputerStudy/521.png)

### 3) 질의어 (SQL)

#### (1) SQL (Structured Query Language)

- 비절차적 언어로 사용자는 자신이 **원하는 데이터**("what")을 선언함으로써 정보를 검색 즉,  
  **원하는 정보를 어떻게**("how") 찾아오는지를 명시하지 않음
- SQL은 **관계해석**(Relational Calculus)개념에 기반
- **데이터 베이스 정의 기능** : DDL (Data Definition Language)
- **데이터 베이스 조작 기능** : DML (Data Manipulation Language)
- **데이터 베이스 제어 기능** : DCL (Data Control Language)

#### (2) 데이터 정의어 (DDL)

- 사용자가 데이터 정의어를 이용하여 관계를 생성하고 제거하며 새로운 속성을 추가하고 삭제하면 관계의 기본키를 정의

```sql
  create table department
      (deptno number not null,
       deptname char(12),
       building char(20),
       primary key (deptno),
      );
```

#### (3) 데이터 조작어 (DML)

- 데이터베이스로부터 데이터를 검색하고 데이터를 수정, 추가, 삭제하는 관리기능

```sql
  SELECT st_id, name
  from student
  where dno = 3, year = 4;
```

#### (4) 데이터 제어어 (DCL)

- 관계에 대한 접근 권한을 부여하거나 취소하는 기능
- 사용자 트랜잭션 시작, 철호, 완료 기능도 지원
