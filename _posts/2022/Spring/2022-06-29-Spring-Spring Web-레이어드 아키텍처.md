---
title: (Web) Spring-Layered Architecture
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Layered Architecture
tag: Spring Web
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-06-29 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Layered Architecture

![alt](https://cphinf.pstatic.net/mooc/20180219_283/1519009121486u3LkD_PNG/2.png?type=w760)

## Controller에서 중복되는 부분을 처리하려면?

- 별도의 객체로 분리한다.
- 별도의 메소드로 분리한다.

```
예를 들어 쇼핑몰에서 게시판에서도 회원 정보를 보여주고, 상품 목록 보기에서도
회원 정보를 보여줘야 한다면 회원 정보를 읽어오는 코드는 어떻게 해야할까?
```

## 컨트롤러와 서비스

- 비지니스 메소드를 별도의 Service객체에서 구현하도록 하고 컨트롤러는  
  Service객체를 사용하도록 한다.

![alt](https://cphinf.pstatic.net/mooc/20180219_85/1519008848012uvMNx_PNG/1.png?type=w760)

## 서비스(Service) 객체란?

- 비지니스 로직(Business logic)을 수행하는 메소드를 가지고 있는 객체
- 보통 하나의 비즈니스 로직은 하나의 트랜잭션으로 동작한다.

## 트랜잭션(Transaction)이란?

- 트랜잭션은 하나의 논리적인 작업을 의미한다.
- 트랜잭션의 특징은 크게 4가지로 구분된다.
  - 원자성 (Atomicity)
  - 일관성 (Consistency)
  - 독립성 (Isolation)
  - 지속성 (Durability)

### 1) 원자성 (Atomicity)

- 전체가 성공하거나 전체가 실패하는 것을 의미한다.
- 하나의 작업이라도 오류가 발생했다면, 앞의 작업들을 모두 원래대로 복원을  
  시켜야한다.
  - 이를 rollback이라고한다.
- 모두 성공했을때만 정보를 모두 반영해야한다.
  - 이를 commit이라고한다.
- 이렇게 rollback하거나 commit을 하게되면 하나의 트랜잭션 처리가 완료된다.

### 2) 일관성 (Consistency)

- 일관선은 트랜잭션의 작업처리 결과가 항상 일관성이 있어야 한다는 것이다.
- 트랜잭션이 진행되는 동안에 데이터가 변경 되더라도 업데이트된 데이터로  
  트랜잭션이 진행되는 것이 아니라, 처음에 트랜잭션을 진행하기 위해 참조한  
  데이터로 진행된다.
  - 이렇게 함으로써 각 사용자는 일관성있는 데이터를 볼 수 있다.

### 3) 독립성 (Isolation)

- 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 경우에 어느 하나의 트랜잭션  
  이라도 다른 트랜잭션의 연산을 끼어들 수 없다.
- 하나의 특정 트랜잭션이 완료될때까지, 다른 트랜잭션이 특정 트랜잭션의 결과를  
  참조할 수 없다.

### 4) 지속성 (Durability)

- 트랜잭션이 성공적으로 완료되었을 경우, 결과는 영구적으로 반영되어야 한다.

## JDBC 프로그래밍에서 트랜잭션 처리 방법

- DB에 연결된 후 Connection객체의 setAutoCommit메소드에 false를 파라미터로  
  지정한다.
- 입력,수정,삭제 SQL이 실행을 한 후 모두 성공했을 경우 Connection이 가지고  
  있는 commit()메서드를 호출한다.

## 스프링에서 트랜잭션 처리방법

### @EnableTransactionManagement

- Spring Java Config 파일에서 트랜잭션을 활성화 할때 사용하는 애노테이션
- Java Config를 사용하게 되면 PlatformTransactionManager 구현체를 모두  
  찾아서 그 중에 하나를 매핑해 사용한다.
- 특정 트랜잭션 메니저를 사용하고자 한다면 TransactionManageMentConfigurer  
  를 Java Config파일에서 구현하고 원하는 트랜잭션 메니저를 리턴하도록 한다.
- 아니면, 특정 트랜잭션 메니저 객체를 생성이 @Primary 애노테이션을 지정한다.

## 서비스 객체에서 중복으로 호출되는 코드의 처리

- 데이터 엑세스 메소드를 별도의 Repository(Dao) 객체에서 구현하도록 하고  
  서비스는 Repository객체를 사용하도록 한다.

출처 :<a href="https://www.boostcourse.org/web326/lecture/58982?isDesc=false">boostcourse 1) 레이어드 아키텍처(Layered Architecture) 란?</a>
