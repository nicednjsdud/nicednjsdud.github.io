---
title: (Software) 데이터 타입, 추상 데이터 타입
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Software
description: Data Structures & Algorithm
tag: Data Structures
article_tag1: Data Structures
article_section: Data Structures
meta_keywords: Data Structures, Computer, Software
last_modified_at: "2022-11-08 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료구조 - 데이터 타입, 추상 데이터 타입

## 1. 데이터 타입 (data type)

- 데이터의 집합과 연산의 집합

```
                / 데이터 : {..,-2,-1,-,1,2,..}
  int 데이터 타입 -
                \ 연산 : +, -, /, *, %

```

## 2. 추상 데이터 타입 (ADT : Abstract Data Type)

- 데이터 타입을 추상적(수학적)으로 정의한 것
- 데이터나 연산이 **무엇(what)**인가는 정의되지만 데이터나 연산을 **어떻게(how)**  
  컴퓨터 상에서 구현할 것인지는 정의 되지 않는다.

## 3. 추상 데이터 타입의 정의

### 1) 객체

- 추상 데이터 타입에 속하는 객체가 정의된다.

### 2) 연산

- 이들 객체들 사이의 연산이 정의된다.
- 이 연산은 추상 데이터 타입과 외부를 연결하는 인터페이스의 역할을 한다.

![alt](/assets/images/post/software/10.png)

## 4. 추상 데이터 타입의 예

### 1) 자연수

- 객체 : 0에서 시작하여 INT_MAX까지의 순서화된 정수의 부분 범위
- 연산 :

```c
   zero() ::= return 0;

   is_zero() ::= if(x) return FALSE;
                else return true;

   add(x,y) ::= if( (x+y) <= INT_MAX) return x+y;
                else return INT_MAX;

   sub(x,y) ::= if(x<y) return 0;
                else return x-y;

   equal(x,y) ::= if(x=y) return TRUE;
                    else return FALSE;

   successor(x) ::= if( (x+1) <= INT_MAX) return x+1;

```

## 5. 추상 데이터 타입과 VCR

### 1) 추상 데이터 타입

![alt](/assets/images/post/software/11.png)

1. 사용자들은 추상 데이터 타입이 제공하는 연산만을 사용할 수 있다.
2. 사용자들은 추상 데이터 타입을 어떻게 사용하는지 알아야 한다.
3. 사용자들은 추상데이터 타입 내부의 데이터를 접근할 수 없다.
4. 사용자들은 어떻게 구현됬는지 몰라도 이용할 수 있다.
5. 만약 다른 사람이 추상 데이터 타입의 구현을 변경하더라도 인터페이스가 변경되지 않으면  
   사용할 수 있다.

### 2) VCR

![alt](/assets/images/post/software/12.png)

1. VCR의 인터페이스가 제공하는 특정한 작업만을 할 수 있다.
2. 사용자는 이러한 작업들을 이헤헤야 한다.  
   즉, 비디오를 시청하기 위해서는 무엇을 해야 하는지 알아야한다.
3. VCR의 내부를 볼 수는 없다.
4. VCR의 내부에서 무엇이 일어나고 있는지 몰라도 이용할 수 있다.
5. 누군가가 VCR의 내부의 기계장치를 교환한다고 하더라도 인터페이스만 바뀌지  
   않는 한 그대로 사용이 가능하다.
