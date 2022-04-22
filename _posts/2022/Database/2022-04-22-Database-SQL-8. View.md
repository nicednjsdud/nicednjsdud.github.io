---
title: Database 8. View (SQL)
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
last_modified_at: '2022-04-22 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

View
======

## 뷰(View)

* 테이블을 들여다 볼 수 있는 창의 역할을 담당.
* SQL 쿼리의 결과값을 임시테이블로 저장해서 사용 할 수 있음.
* 다른 테이블을 기반으로 만들어진 가상 테이블
* 데이터를 실제로 저장하지 않고 논리적으로만 존재하는 테이블이지만,  
  일반 테이블과 동일한 방법으로 사용함.
* 뷰를 통해 기본 테이블의 내용을 쉽게 검색할 수는 있지만,  
  기본 테이블의 내용을 변화시키는 작업은 제한적으로 이루어짐.

### 뷰 생성

```sql
    CREATE VIEW 뷰이름[속성들]
    AS SELECT문 
    [WITH CHECK OPTION];
```

* CREATE VIEW에서 속성들을 생략하면 SELECT절에 나열된 속성의 이름을 그대로 사용
* AS 키워드와 함께 기본 테이블에 대한 SELECT문을 작성

#### WITH CHECK OPTION
* 뷰에 삽입이나 수정 연산을 할때 SELECT문에서 제시한 뷰의 정의 조건을 위반하면  
  수행되지 않도록 하는 제약조건을 지정

```sql
/* 
 * 고객 테이블에서 등급이 VIP인 고객의 고객아이디, 고객이름, 나이로 구성된 뷰를
 * 우수고객이라는 이름으로 생성하시오.
 * 그런 다음 우수고객 뷰의 모든 내용을 검색하시오
 */ 

    CREATE VIEW 우수고객 (고객아이디, 고객이름, 나이)
    AS SELECT 고객아이디,고객이름,나이
    FROM 고객
    WHERE 등급 = 'vip'
    WITH CHECK OPTION;

    SELECT *
    FROM 우수고객;
```

![alt](/assets/images/post/Database/sql/25.png)

### 뷰 활용

#### SELECT 문

* 뷰는 일반 테이블과 같은 방법으로 원하는 데이터를 검색할 수 있음.
* 검색 연산은 모든 뷰에 수행 가능

```sql
    SELECT *
    FROM 우수고객
    WHERE 나이 >= 25;
```

![alt](/assets/images/post/Database/sql/26.png)

#### INSERT, UPDATE, DELETE 문

* 뷰에 대한 삽입, 수정, 삭제 연산은 실제로 기본 테이블에 수행되므로 결과적으로  
  기본 테이블이 변경됨.
* 뷰에 대한 삽입,삭제 등 제한적을 수행됨

```sql
--primary key o
    CREATE VIEW 제품1
    AS SELECT 제품번호, 재고량, 제조업체 
    FROM 제품
    WITH CHECK OPTION;

--insert
    INSERT INTO 제품1 VALUES ('p08',1000,'신선식품');
```
![alt](/assets/images/post/Database/sql/27.png)

* 실제 제품 테이블 반영 (뷰 테이블 x)

![alt](/assets/images/post/Database/sql/28.png)


##### 변경 불가능한 뷰
* 기본 테이블의 기본키를 구성하는 속성이 포함되어 있지 않은 뷰

```sql
--primary key x
    CREATE VIEW 제품2
    AS SELECT 제품명, 재고량, 제조업체 
    FROM 제품
    WITH CHECK OPTION;

--insert
    INSERT INTO 제품2 VALUES ('시원냉면',1000,'신선식품');
```

![alt](/assets/images/post/Database/sql/29.png)

### 뷰의 장점

* 데이터의 보안 유지에 도움이 됨
* 데이터를 좀 더 편리하게 관리할 수 있음.



