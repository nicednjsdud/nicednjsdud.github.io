---
title: (Spring) 2. Spring Framework
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Spring
description: Spring Framework description
tag : Spring Basic
article_tag1: Spring Basic
article_section: Spring Basic
meta_keywords: Spring, backend ,framework
last_modified_at: '2022-06-24 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Spring Framework description
============================

![alt](/assets/images/post/spring/2.png)

## 1. Framework 정의

* 어떤 것을 구성하는 구조 또는 뼈대
* 기능을 미리 클래스나 인터페이스 등으로 만들어 제공하는 반제품 **(Semi Complete)**

## 2. Framework 장점

### 1) 일정한 기준에 따라 개발이 이루어짐
    
* 개발 생산성과 품질 보장된 애플리케이션 개발

### 2) 개발 후 유지보수 및 확장성에서도 품질 보장

## 3. Enterprise Applictaions

* 다수의 사용자가 접근하며, 기업내 분산된 다른 엔터프라이즈 애플리케이션과  
  통합됨

### 1) 예

* 배송추적, 환자기록, 외환거래, 보험, 회계, 인사, 공급망, 고객서비스

## 4. Java Enterprise Edition : Java EE

* Enterprise Applications에 필요한 확장성, 신뢰성, 보안성 등 제공하는 자바  
  플랫폼 프레임워크임.

![alt](/assets/images/post/spring/1.png)


### 1) 2018년 Java EE가 오라클에서 이클립스 재단으로 이관

* Jakarta EE 새이름을 받음

## 5. 스프링 프레임워크

### 1) 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크

#### 1. 제어의 역전과 의존관계 주입 **(Inversion of Control / Dependency Injection)**
* 설정 파일이나 어노테이션을 통해서 객체 간의 의존관계 설정

#### 2. 관점지향 프로그래밍 **(Asepect Oriented Programming)**
* 트랜잭션이나 로깅, 보안과 같이 공통적으로 필요로 하는 모듈들을 실제 핵심   
  모듈에서 분리해서 적용  
       
#### 3. 이식 가능한 서비스 추상화 **(Portable Service Abstraction)**

#### 4. 설정정보

#### 5. 핵심은 엔터프라이즈 서비스 기능을 POJO (순수 객체)에 제공하는 것임

### 2) 자바 웹 애플리케이션 개발을 위한 오픈 소스 프레임 워크

* EJB(Enterprise Java Bean) 보다 가벼운 경량 프레임워크
* 엔터프라이즈 개발 용이

### 3) 컨테이너 (Container)

#### 톰캣은 서블릿 컨테이너라고 부름
* 톰캣을 실행하면 톰캣은 서블릿의 생성, 초기화, 서비스 실행, 소멸에 관한   
  모든 권한을 가지고 서블릿을 관리
* 스프링은 애플리케이션에서 사용되는 여러가지 빈 (클래스)을 개발자가 아닌  
  스프링이 권한을 가지고 Java 객체의 LifeCycle을 직접 관리. 

### 4) 스프링 IoC 컨테이너(Spring IoC Container)와 빈 (Beans)

* 컨테이너는 제어의 역전(IoC) 원리가 적용된 스프링 핵심 컴포넌트.
* 컨테이너에 의해 생성 및 조립된 후 관리(초기화,소멸 등)되는 객체를 빈(Beans)  
  이라고 부름.
* 빈 생성 시 의존관계 주입(Dependency Injection)이 일어남
* 빈 구성정보를 바탕으로 비즈니스 오브젝트를 이용해 애플리케이션 구성하고   
  생애를 관리

####  POJO (Plian Old Java Object) 기반 비즈니스 오브젝트 지원
* POJO 는 객체지향 원리에 충실
* 특정 환경이나 규약에 종속되지 않고 필요에따라 재활용 될 수 잇는 방식으로  
  설계된 객체임
* Java 객체는 특정한 인터페이스를 구현하거나, 특정 클래스를 상속받지 않음

## 6. Spring Framework 구성하는 기능 요소

### 1) Spring Core Container 

* Spring 프레임워크의 기본 기능 제공
* 이 모듈에 있는 BeanFactory는 Spring의 기본 컨테이너이면서 스프링 DI의 기반임

### 2) AOP

* AOP 모듈을 통해 Aspect 지향 프로그래밍 지원

### 3) ORM

* MyBatis, Hibernate, JPA 등 널리 사용되는 ORM 프레임워크의 연결고리 제공