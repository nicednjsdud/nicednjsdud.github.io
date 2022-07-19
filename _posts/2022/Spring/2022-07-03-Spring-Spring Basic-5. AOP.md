---
title: (Spring) 5. AOP 이란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: AOP
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-03 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# AOP

## 1. AOP 개요와 용어

### 1) 핵심기능과 부가기능

- 업무(Biz) 로직을 포함하는 기능 : 핵심 기능(Core Concerns)
- 핵심기능을 도와주는 부가적인 기능(로깅, 보안 등) : 보안기능 (Cross-cutting Concerns)

### 2) AOP (Aspect Oriented Programming)

- 애플리케이션에서 관심사의 분리(기능의 분리)

```
    즉, 핵심기능에서 부가적인 기능을 분리함.
```

- 분리한 부가기능을 애스펙트라는 모듈형태로 만들어서 설계,개발하는 방법
- **AOP**는 부가기능을 애스팩트로 정의하여 핵심기능에서 부가기능을 분리함.
- 관점 지향 프로그래밍(AOP)을 이용해서 주기능과 보조기능을 분리해서 메서드에 적용

## 2. AOP 용어

### 1) 애스펙트(Aspect)

- 부가기능을 정의한 코드인 **어드바이스(Advice)**와 어드바이스를 어디에  
  적용할지를 결정하는 **포인트 컷(PointCut)**
- Aspect = Advice + PointCut

### 2) 타켓(Target)

- 핵심기능을 담고 있는 모듈
- 타겟은 부가기능을 부여할 대상이 됨.

### 3) 어드바이스(Advice)

- **(타겟에 제공할)**부가기능을 담고 있는 모듈

### 4) 포인트 컷(PointCut)

- 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식임.
- 포인트컷 표현식은 execution으로 시작함.

### 5) 위빙(Weaving)

- 포인트컷에 의해서 결정된 타겟의 조인 포인트에 부가기능(어드바이스)을 삽입하는  
  과정을 뜻함
- 핵심기능(타겟)의 코드에 영향을 주지 않으면서 필요한 부가기능(어드바이스)을 추가  
  할수 있도록 해주는 핵심적인 처리과정

![alt](/assets/images/post/spring/28.png)

### 6) 조인 포인트(Join Point)

- 어드바이스가 적용될 수 있는 위치
- 타겟 객체가 구현한 인터페이스의 모든 메서드는 조인 포인트가 됨.
- AOP가 적용되는 지점

## 3. AOP 기능을 구현하는 방법

### 1) 제공하는 API을 이용하는 방법

### 2) @Aspect 애너테이션을 이용한 AOP 구현 방법

- 부가기능 제공하는 Aspect 클래스를 작성함
- Aspect 클래스는 어드바이스를 구현하는 메서드와 포인트컷을 포함함
- XML 설정 파일에 `<aop:aspectj-autoproxy />`를 설정함.

## 4. Spring AOP 특징

![alt](/assets/images/post/spring/29.png)

- Spring은 타겟(Target) 객체에 대한 프록시를 만들어 제공함
- 타겟을 감싸는 프록시는 실행시간(Runtime)에 생성됨
- 프록시(Proxy)는 어드바이스를 타겟 객체에 적용하면서 생성되는 객체임.
- 프록시가 호출을 가로챔 (Intercept)
  - 전처리 어드바이스
  - 후처리 어드바이스
- Spring AOP는 메서드 조인 포인트만 지원함

## 5. 포인트컷 관련 용어

### 1) 지시자 (exection, within, bean)

#### 1-1 execution

### 2) 어드바이스 동작 시점

#### 1-1 Before 어드바이스

- 타겟의 메서드가 실행되기 이전(before) 시점에 처리해야 할 필요가 있는 부가기능을 정의함
- **JoinPoint 앞에서 실행되는 Advice**

#### 1-2 After 어드바이스

#### 1-3 After-returning 어드바이스

#### 1-4 After-throwing 어드바이스

#### 1-5 Around 어드바이스

- 타겟의 메서드가 호출되기 이전(before) 시점과 이후(after) 시점에 모두 처리해야 할  
  필요가 있는 부가기능을 정의함.
- **JoinPoint 앞과 뒤에서 실행되는 Advice**

## 6. JoinPoint Interface

- AspectJ에서 AOP가 적용되는 지점을 뜻함
- getArgs() : 메서드 아규먼트를 반환함
- toString() : 어드바이즈 되는 메서드의 설명 출력함.
- getSignature() : 어드바이즈 되는 메서드의 설명 출력함.
- **Around 어드바이스는 ProceedingJoinPoint 타입의 파라미터를 필수적으로 선언해야 함.**

## 7. PointCut 표현식

- AspectJ 포인트컷 표현식은 포인트컷 지시자를 이용해 작성함.
- 포인트컷 지시자 중에서 가장 대표적으로 사용되는 것은 **execution()**임.

### 1) 문법 구조

```java
  [] = 생략가능              (패키지와 클래스 이름에 대한 패턴)
                            ------
  execution([접근제한자] 타입패턴 타입패턴 이름패턴(타입패턴) [throws 예외패턴])
                                    ------
                                    파라미터의 타입 패턴을 순서대로 넣음
                                    와일드카드를 이용해 파라미터 개수에 상관없는
                                    패턴 작성
```

#### ex)

```java
              (package)  (class)
               ----------- -   -- (any type and number of arguments)
  "execution(* kr.co.tiles.*.*(..))"
            --               -
           (any return type) (method)
```

```java
  "execution(* hello(..))"
```

- hello라는 이름을 가진 메서드를 선정하는 것
- 파라미터는 모든 종류를 다 허용함.

```java
  "execution(* hello())"
```

- 파라미터 패턴이 ()로 되어 있으니 hello 메서드 중 파라미터가 없는 것만 선택함.

```java
  "execution(* kr.co.tiles.member.controller.MemberControllerImpl.*(..)"
```

- kr.co.tiles.member.controller.MemberControllerImpl 클래스를 직접 지정하여  
  이 클래스가 가진 모든 메서드를 선택함.

```java
  "execution(* kr.co.tiles.member.*.*(..))"
```

- kr.co.tiles.member 패키지의 모든 클래스에 적용됨
- 하지만 서브패키지의 클래스는 포함되지 않음.

```java
  "execution(* kr.co.tiles.member..*.*(..))"
```

- kr.co.tiles.member 패키지의 도든 클래스가 적용됨
- ..를 사용해서 서브패키지의 모든 클래스까지 포함됨.
