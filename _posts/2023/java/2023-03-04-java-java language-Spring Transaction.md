---
published: true
title: (Spring) 스프링 트랜잭션 @Transactional
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Visitor Pattern (Design Pattern - 18)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-03-04 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# @Transactional 이란?

## 1. AOP (Aspect-Oriented Programming)

- 애플리케이션 기능은 크게 핵심기능과 부과 기능으로 나눌 수 있다.
  - 핵심 기능 : 해당 객체가 제공하는 고유한 기능 (ex : CustomerService - 구매로직)
  - 부가 기능 : 핵심 기능을 보조하는 기능 (ex : 로그 추적, 트랜잭션 처리)
- 하나의 부가 기능은 여러 곳에서 동일하게 사용되는 경우가 많다.
- 이 부가 기능을 분리하고 이 기능을 어디에 적용할지 선택하는 기능을 합쳐 하나의 모듈로 만든 것이 **Aspect**이다.

- **우리 말로는 `관점`이라는 뜻인데 애플리케이션을 바라볼 때 핵심 기능만 바라볼 수 있도록 도와준다.**
- `@Transactional`은 **트랜잭션 AOP**를 위해 Spring에서 **지원해주는 어노테이션**이다.

## 2. @Transactional 예제

- UserDao의 loseMoeny 또는 SellerDao의 gainMoney 둘 중 하나라도 실패하면 전체 작업을 취소
- 모든 작업이 성공할 경우 DB에 해당 변경 내역이 반영
- **CheckedException**이 발생하는 경우는 트랜잭션이 롤백되지 않는다.

```java
    @Transactional
    public void buy(Long money){
        userDao.loseMoney(money);
        sellerDao.gainMoney(money);
    }
```

## 3. @Transactional의 동작 구조

- 스프링 트랜잭션 AOP는 `@Transactional`을 인식하여 트랜잭션 프록시를 적용
- 프록시는 `대리인`이라는 뜻인데 `Aspect`와 `@Transcational`을 적용한 클래스 or 메서드인 Target을  
  연결해주는 역할을 한다.

1. Clinet가 API 호출
2. 프록시 실행
3. 트랜잭션 코드 실행
4. 비즈니스 로직 실행
5. 트랜잭션 코드 실행 (commit / rollback)

![alt](/assets/images/post/ComputerStudy/811.png)

## 4. 테스트와 @Transcational

* 테스트 환경에서는 `@Transactional`이 약간 다르게 동작한다.
* 성공/실패 결과와는 다르게 테스트 메서드가 종료되면 무조건 롤백

