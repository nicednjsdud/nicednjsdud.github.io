---
title: Database 7. DML, JOIN, SUBQUERY (SQL)
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

DML
======

## SELECT 문 : 데이터 검색

### 1. 정렬검색

* 사용자가 원하는 순서로 출력
* 오름차순(기본) : ASC / 내림차순 : DESC
* 널 값은 오름차순에서 맨 마지막에 출력됨, 내림차순에서는 맨 먼저 출력됨.

```sql
    SELECT [ALL | DISTINCT] 속성들
    FROM 테이블(들)
    [WHERE 조건]
    [ORDER BY 속성(들) [ASC | DESC]];
```

``` sql

    SELECT cusname 고객이름, grade 등급, cusage 나이
    FROM CUSTOMER 
    ORDER BY cusage DESC;
```
![alt](/assets/images/post/Database/sql/13.png)

### 2. 집계 함수(aggregate function) 검색

* = 열 함수 (column function)
* 개수, 합계, 평균, 최대값, 최소값의 계산 기능 제공
* Where 절에서는 사용할 수 없고, SELECT 절이나 having절에서만 사용 가능.
* COUNT, MAX, MIN, SUM, AVG

```sql
    SELECT sum(remain) AS "재고량 합계"
    FROM item
    WHERE FACTORY = '오뚜기';
```

![alt](/assets/images/post/Database/sql/15.png)

```sql

-- 정확한 개수를 계산하기 위해서는 보통 기본키 속성이나 *를 주로 이용.
    SELECT count(*) AS 고객수
    FROM CUSTOMER;
```

![alt](/assets/images/post/Database/sql/16.png)

### 3. 그룹별 검색

* 특정 속성의 값이 같은 투플을 모아 그룹을 만들고, 그룹별로 검색
* HAVING 키워드를 함께 이용해 그룸에 대한 조건을 작성
* 그룹을 나누는 기준 이 되는 속성을 SELECT절에도 작성하는것이 좋음

```sql
    SELECT [ALL | DISTINCT] 속성들
    FROM 테이블(들)
    [WHERE 조건]
    [GROUP BY 속성(들) [HAVING 조건]]
    [ORDER BY 속성(들) [ASC | DESC]];
```

```SQL
-- 주문 테이블에서 주문 제품별 수량의 합계를 검색하시오.
-- 동일 제품을 주문한 투풀을 모아 그룹으로 만들고, 그룹별로 수량의 합계를 계산
    SELECT ORDERNAME, SUM(COUNT) AS 총주문수량
    FROM ORDERSERVICE
    GROUP BY ORDERNAME;
```

![alt](/assets/images/post/Database/sql/17.png)

## JOIN

### 개념 

* 서로 다른 테이블을 공통 컬럼을 기준으로 합치는 (결합하는) 테이블 단위 연산.
    * 여러 테이블에 대한 조인 검색
    * 여러 개의 테이블을 연결하여 데이터를 검색하는 것
    * 조인 속성

```
    - 조인 검색을 위해 테이블을 연결해주는 속성
```

* 조인의 결과 테이블은 이전 테이블의 컬럼 수의 합과 같음.

```SQL
    SELECT * FROM 테이블1 JOIN 테이블2 ON 테이블1.컬럼명 = 테이블2.컬럼영 ....
```

* 조인시 서로 다른 테이블에 같은 컬럼명이 존재하면 구분을 위해 테이블명.컬러명  
  으로 사용해서 표시
    - 연결하려는 테이블 간에 조인 속성의 이름은 달라도 되지만 도메인은 같아야 함.
    - 일반적으로 외래키를 조인 속성으로 이용함.

* FROM 절에 검색에 필요한 모든 테이블을 나열.

### 종류

* 조인시 NULL값을 허용하지않는 내부조인,허용하는 외부조인으로 구분.

#### Inner Join

##### 조인 결과 

* 두 개 테이블에 모두 존재하는 행만 남음
* 조인시 null값을 허용하지 않음
* null값을 가진 레코드(투플)는 조인결과에서 빠짐

##### 필요 사항 

* 두개 테이블을에 조인 키가 빠짐없이 있을 때  

![alt](/assets/images/post/Database/sql/18.png)

#### Left Join

##### 조인 결과 

* 왼쪽 테이블을 기준으로 오른쪽 테이블을 붙힘

```
    만약, 오른쪽 테이블에 조인되는 값이 없는 경우 null로 표기됨
```

* 조인시 join의 왼쪽 테이블의 null값을 포함해서 표시

![alt](/assets/images/post/Database/sql/19.png)


```sql
    SELECT 제품.제품명 
    FROM 제품, 주문
    WHERE 주문.주문고객 = 'banana' AND 제품.제품번호 = 주문.주문제품; 
```

![alt](/assets/images/post/Database/sql/20.png)

## 부속 질의분을 이용한 검색


### SELECT문 안에 또 다른 SELECT문을 포함하는 질의



#### 상위 질의문 (주 질의문)

* 다른 SELECT문을 포함하는 SELECT문 


#### 부속 질의문 (서브 질의문)

* 다른 SELECT문 안에 들어 있는 SELECT문
    * 괄호로 묶어서 작성.
    * ORDER BY 절을 사용할 수 없다.

##### 결과 반환 종류

* 단일 행 : 하나의 행을 결과로 반환
* 다중 행 : 하나 이상의 행을 결과 반환

```sql
    -- 부속 질의문
    SELECT 제조업체
    FROM 제품
    WHERE 제품명 = '달콤비스킷';

    -- 상위 질의문
    SELECT 제품명, 단가
    FROM 제품
    WHERE 제조업체 = (SELECT 제조업체 FROM 제품 WHERE 제품명 = '달콤비스킷');
```


![alt](/assets/images/post/Database/sql/21.png)

### 부속질의문을 먼저수행하고, 그결과를 이용해 상위 질의문을 수행

### 부속 질의문과 상위 질의문을 연결하는 연산자가 필요.
* 단일 행 부속 질의문은 비교 연산자 (=, <>, >=, <, <=>)

* 다중 행 부속 질의문은 비교 연산자 사용 불가

#### 사용가능한 연산자(다중행 연산자)
* 결과값 중에 있는 것에서의 의미
* 존재하면 TRUE / 존재하지 않으면 fALSE
* IN : 부속 질의문 결과 값 중 일치하는 것이 있으면 검색 조건이 참

```
   IN은 전체 레코드를 스캔함, EXISTS는 존재여부만 확인하고 스캔하지 않음
```

* NOT IN : 부속 질의문의 결과 값 중 일치하는 것이 없으면 검색 조건이 참

```sql
    SELECT 주문제품
    FROM 주문 
    WHERE 주문고객 = 'banana';

    SELECT 제품명, 제조업체 
    FROM 제품
    WHERE 제품번호 IN (SELECT 주문제품 FROM 주문 WHERE 주문고객 = 'banana');
```

![alt](/assets/images/post/Database/sql/22.png)

* EXIST : 부속 질의문의 결과 값이 하나라도 존재하면 검색 조건이 참
* NOT EXISTS : 부속 질의문의 결과 값이 하나도 존재않으면 검색 조건이 참

```sql

-- 2019년 3월 15일에 제품을한 주문한 고객의 고객이름을 검색하시오.
SELECT 고객이름
FROM 고객
WHERE EXISTS (SELECT * FROM 주문 
 			  WHERE 주문일자 = '2019-03-15' AND 주문.주문고객 = 고객.고객아이디 );
```

![alt](/assets/images/post/Database/sql/24.png)

* ALL : 부속 질의문의 결과 값 모두와 비교한 결과가 참이면 검색 조건이 참
```
    여러 개의 레코드 AND효과
    (가장 큰 값보다 큰)
```

```sql
    
 --대한식품이 제조한 모든 제품의 단가보다 비싼 제품의 제품명, 단가,   
 --제조업체를 검색하시오.
SELECT 제품명, 단가, 제조업체
FROM 제품
WHERE 단가 > ALL(SELECT 단가 FROM 제품 WHERE 제조업체 = '대한식품');

```

![alt](/assets/images/post/Database/sql/23.png)

### 스칼라 서브 쿼리

* select절 내에 사용하는 서브 쿼리.

```sql
-- 스칼라 서브쿼리 
/*
    각 제품의 가격을 구하면서 해당 제품이 위치하고 있는 제품 카테고리의 평균
    가격도 같이 구하시오.
    PRODUCT_NAME        list_price                   avg_list_price  
*/

select a.product_name, a.list_price, round(
                                (select avg(k.list_price)
                                 from products K
                                where k.category_id = a.category_id
                                    ),2) as AVG_List_Price
from products A
order by a.product_name
```

![alt](/assets/images/post/Database/sql/44.png)

## SQL 함수

### DBMS가 제공하는 내장 함수(built-in function)

#### 단일행 함수

##### 특징

* SELECT, WHERE, ORDER BY 절에 사용 가능함.
* 각 행(ROW)들에 대해 개별적으로 작용함.
    * 각각의 행에 대한 조작 결과를 리턴함.
* 단 하나의 결과만 리턴함.
* 함수의 중첩이 가능함.

#### 문자 형 함수

* 문자를 입력하면 문자나 숫자값을 반환함.
* LOWER, UPPER, SUBSTR, LENGTH, TRIM..

```SQL
-- 단일행 문자형 함수

SELECT LOWER('Oracle Server, SQL Develper') AS "LOWER('소문자로 변환')",
	   UPPER('Oracle Server, SQL Develper') AS "UPPER('대문자로 변환')",
	   ASCII('A') AS "ASCII('아스키코드값 출력')",
	   CONCAT('SQL','Develper') AS "CONCAT('문자열 결합')",
	   SUBSTR('SQL Develper',1,3) AS "SUBSTR('문자열 잘라내기')" 
FROM DUAL;
```

![alt](/assets/images/post/Database/sql/98.png)

#### 날짜, 시간 함수 
#### 변환 형 함수

##### TO_DATE(char , datetime)
* 문자형(CHAR) 데이터를 DATE형으로 변환

##### TO_CHAR(date , datetime)
* DATE형 데이터를 문자열(VARCAHR2)로 변환
* datetime의 주요인자

```sql
    - d     : 요일 순서 ( 1 ~ 7 , 월 = 1 )
    - dd    : 1달 중 날짜 ( 1 ~ 31 )
    - ddd   : 1년 중 날짜 ( 1 ~ 365 )
    - mm    : 월 순서 ( 01 ~ 12 , January = 1 )
    - momth : 월 이름 ( January ~ December )
    - yyyy  : 4자리 연도  
```
##### 숫자 함수
* 숫자를 입력하면 숫자값을 반환함.
* ABS (숫자) : 절대값
* ROUND (숫자, m) : m 자리를 기준으로 숫자 반올림

```SQL
SELECT ABS(-15) AS "ABS('절대값을 반환')",
	   SIGN(10) AS "SIGN('양수일 경우 1 음수일 경우 -1, 0일 경우 0 반환')",
	   MOD(8,3) AS "MOD('나머지 반환')",
	   CEIL(38.678) AS "CEIL('무조건 올림')",
	   FLOOR(38.678) AS "FLOOR('무조건 버림')",
	   ROUND(38.678,2) AS "ROUND('소수점 2번째 자리까지 반올림')",
	   TRUNC(38.678) AS "TRUNC('0의 자리에서 무조건 자름')",
	   TRUNC(38.678,1) AS "TRUNC('1의 자리에서 무조건 자름')"
FROM DUAL;
```

![alt](/assets/images/post/Database/sql/100.png)
![alt](/assets/images/post/Database/sql/101.png)

##### 문자 함수 (문자 변환)

* REPLACE(s1, s2, s3)

```
    - 대상 문자열(s1)의 지정된 문자(s2)를 원하는 문자(3)로 변경
```

```sql
    -- 공백이 들어간 것을 알수 있음.
SELECT REPLACE(CHAR_COMPARE_4,' ','_') AS CHAR_COMPARE_4 
		, REPLACE(CHAR_COMPARE_6,' ','_') AS CHAR_COMPARE_6 
FROM EZEN.CHAR_COMPARE cc ;

```

![alt](/assets/images/post/Database/sql/90.png)

##### NULL 관련 함수

* NULL을 처리하기 위한 함수
* NVL, NULLIF, COALESCE

#### 집계 함수
#### 분석 함수