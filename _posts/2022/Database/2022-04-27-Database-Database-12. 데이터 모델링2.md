---
title: Database 11. 데이터모델링 - 관계
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
last_modified_at: '2022-04-27 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

데이터 모델링 - 관계
===========

## 관계(Relationship)

* 상호 연관성이 있는 상태
* 엔터티 간 논리적인 연관성을 의미함
* 존재에 의한 관계와 행위에 의한 관계로 구분됨.

![alt](/assets/images/post/Database/sql/58.png)

## 관계의 페어링

* 관계는 엔터티 안에 인스턴스가 개별적으로 관계를 가지는 것 **(페어링)**  
  이것의 집합을 관계로 표현한다는 것임.
* 각각의 엔터티의 인스턴스들은 자신이 관련된 인스턴스들과 관계의 발생으로  
  참여하는 형태를 **관계 페어링(Relationship Paring)**이라고 함.

## 관계의 분류 

### 존재에 의한 관계

![alt](/assets/images/post/Database/sql/59.png)

* 사원은 부서에 항상 속해 있다.

```
 "소속된다"의미는 행위에 따른 이벤트에 의해 발생되는 의미가 아니고  
  그냥 사원이 부서에 소속되어 있기 때문에 나타나는 즉 존재의 형태에 의해  
  관계가 형성되어 있는 것임
```

### 행위에 의한 관계

![alt](/assets/images/post/Database/sql/60.png)

* 주문은 고객이 주문을 할 때 발생한다.

```
  주문 엔터티의 주문번호는 고객이 "주문한다"라는 행위에 의해 발생되었기  
  때문에 두 엔터티 사이의 관계는 행위에 의한 관계가 되는 것임.
```

## 관계의 표기법

* **관계명(Membership)** : 관계의 이름
* **관계차수(Cardinality)** : 1:1, 1:M, M:M
* **관계선택사양(Optionality)** : 필수관계, 선택관계

### 1) 관계명

* 엔터티가 관계에 참여하는 형태를 지칭함.
* 각각의 관계는 두개의 관계명을 가질 수 있음.
    * 즉 각각의 관게명에 의해 두 가지의 관점으로 표현될 수 있다.

* **관계 시작점 (The Beginning)**과 **끝점 (The End)** 모두 관계이름을 가져야 하며,   
참여자의 관점에 따라 관계이름이 **능동적(Active)** 이거나 **수동적(Passive)**으로 명명됨

#### 명명 규칙

* 애매한 동사는 피한다.
* 현재형으로 표현한다.

### 2) 관계 차수

* 두 개의 엔터티 간 관계에서 참여자의 수를 표현한 것을 **관계차수(Cardinality)**라고 함.
* 가장 일반적인 관계 차수 표현방법은 **1:1, 1:M, M:M** 임.

#### 1:1

![alt](/assets/images/post/Database/sql/61.png)

* 각각의 엔터티는 관계를 맺는 다른 엔터티에 대해 단지 하나의 관계만을 가지고 있음.

#### 1:M

![alt](/assets/images/post/Database/sql/62.png)

* 한명의 사원은 한 부서에 소속되고 한 부서에는 여러 사원을 포함함.

#### M:M

![alt](/assets/images/post/Database/sql/63.png)

* 하나 혹은 그 이상의 수와 관계를 가지고 있음.

### 3) 관계 선택사양 (Optionality)

* 지하철출발과 지하철문닫힘은 **필수(Mandatory)적**으로 연결 관계가 있는 것임 

```
    이와 같은 것이 데이터 모델의 관게에서는 필수참여관계(Mandatory)가 됨.
```

* 안내방송과 지하철 출발과 상관없이 방송해도 아무런 문제가 발행하지 않은 것임.

```
    지하철 출발과 지하철방송과는 정보로서 관련은 있지만 서로 선택적인 관계
    (Optional)가 되는 것임.
```

#### 선택적 관계 

* 고객은 여러개의 주문을 할 수도 있고 한개의 주문도 하지않을 수 있다.

#### 필수적 관계

* 주문은 반드시 고객을 가짐.


