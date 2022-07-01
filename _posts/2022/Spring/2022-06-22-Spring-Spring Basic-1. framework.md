---
title: (Spring) 1. FrameWork 란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Spring
description: What is the FrameWork?
tag : Spring Basic
article_tag1: Spring Basic
article_section: Spring Basic
meta_keywords: Spring, backend ,frame work
last_modified_at: '2022-06-22 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

What is the FrameWork?
=======================

## 0. Intro

### 1) 엔터프라이즈 애플리케이션 개발의 복잡함

* 복잡한 현대 사회 문제를 해결하려 하는데서 오는 비즈니스 로직의 복잡함
* 수 많은 사용자와 데이터를 대응하기 위한 기술적인 제약조건과 요구사항

### 2) 복잡함을 다루기 위한 해결책 (스프링)

* 객체지향 설계
* PSA + IOC + AOP

## 1. SW 재사용 방안

### 1) Copy & Paste

### 2) 메서드 호출

* 자주사용되고, 유사한 기능을 모아 메서드로 정의하여 재사용함.

### 3) 클래스 재사용 (상속)

### 4) AOP (Aspect Oriented Programming)

* 관심사의 분리 (Sesperation Of Concerns)

## 2. 디자인 패턴

* 프로그램 개발에서 자주 나타나는 이슈를 해결하기 위한 방법
* 개발과정에서 발견된 Know-How를 축적하여 이름을 붙여 재사용하기 위한 좋은  
  형태로 패턴, 규약을 묶어서 정리한 것.
    * Design Patterns : Elements of Reusable Object - Oriented Software

### 1) 사용하는 이유

* 요구사항은 수시로 변경 -> 소스코드 변경을 최소화 
* 팀 프로젝트진행 -> 범용적인 코딩 스타일 적용
* 인수인계하는 경우 -> 직관적인 코드 사용 

## 3. 프레임워크

* 비기능적 요구사항 (성능,보안,확장성,안정성 등)을 만족하는 구조와 구현된  
  을 안정적으로 실행하도록 제어해주는 잘 말들어진 구조의 라이브러리 덩어리
* 애플리케이션들의 최소한의 공통점을 찾아 하부 구조를 제공함으로써 개발자들로  
  하여금 시스템의 하부 구조를 구현하는데 들어가는 노력을 절감.
* 개발자는 프레임워크의 기반 코드를 확장하여 사용하면서 자연스럽게 그   
  프레임워크에서 사용된 패턴을 적용할수 있게 됨.
* 프레임워크는 디자인 패턴과 그것이 적용된 기반 라이브러리의 결합으로 이해할 수  
  있음.

### 1) 사용하는 이유

* 비기능적인 요소들 초기 개발 단계마다 구현해야 하는 것을 극복해줌
* 기능적인(Funcotional) 요구사항에 집중할 수 있도록 해줌
* 반복적으로 발견되는 이슈를 해결하기 위한 solution 제공함.

## 4. 프레임워크의 구성요소

### 1) IoC (Inversion of Control)

* 제어의 역전
* 인스턴스 생성부터 소멸까지의 생명주기 관리를 개발자가 아닌 컨테이너  
  (Spring IoC Container)가 대신 해준다는 의미임.
* 컨테이너 역할을 해주는 프레임워크에게 제어(Control)하는 권한을 넘겨서   
  개발자의코드가 신경써야 할 것을 줄이는 전략임.
* 일반적인 프로그램 흐름과 반대로 동작하므로 IoC라고 함.
* Spring Container 는 IoC를 지원함.
* 메타데이터(XML,annotation 설정)를 통해 beans 관리 (애플리케이션의 중요부분)  
* Spring Container는 관리되는 bean들을 의존정 주입 (Dependenecy Injection)을  
  통해 IoC를 지원함.

### 2) 클래스 라이브러리 (Class Library)

* 특정 부분의 기술적인 구현을 라이브러리 형태로 제공


| cf. | 특징          | 프레임워크  |   라이브러리 |
|-----|--------------|-------------|-------------|
|..|유저코드 작성|프레임워크 클래스를 서브클래싱해서 작성 제공 |독립적으로 작성 |
|..| 호출 흐름 | 프레임워크코드가 유저코드를 호출 | 유저코드가 라이브러리를 호출|
|..| 실행 흐름 | 프레임워크가제어 | 유저코드가 제어 |
|..| 객체의 연동 | 프레임워크가 정의 | 독자적으로 정의 |


