---
title: (컴퓨터 개론) 5-2 프로그래밍 언어의 종류
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로그래밍 언어의 종류
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2022-11-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 프로그래밍 언어의 종류

## 1. 절차적 프로그래밍 언어

- 프로그램을 어떤 순서와 절차인 명령어에 따라 작성하는 기법

### 1) 절차적 프로그래밍의 개념

#### (1) 구조적 프로그래밍

- 순차, 반복 및 제어 구조의 표현을 체계적으로 할 수 있는 특징
- 반복 구조 : for, while
- 선택 구조 : if-then-else, switch-case

### 2) 절차적 프로그래밍 언어의 유형

#### (1) FORTRAN

- 1954년 과학 및 공학 계산을 위한 최초의 고급 프로그래밍 언어

#### (2) COBOL

- 1960년대 초반 **데이터 처리**를 주목적으로 개발된 상업용 언어

#### (3) C, BASIC, PASCAL

##### (3-1) C

- 1970년대 초반 벨 연구소에서 UNIX 운영체제를 작성하기 위하여 개발
- 고급수준 프로그램뿐만 아니라 저급수준 하드웨도 제어

##### (3-2) BASIC

- 간단한 계산을 위한 초보자용
- 배우기 쉽고 작성이 용이한 교육용 언어

## 2. 객체지향언어

- 감기약처럼 몇 가지 기능을 캡슐에 담아서 시판하는 것처럼
- 처리 단위 별로 묶어서 프로그래밍 하는 방식임

### 1) 객체지향언어의 개념

#### (1) 클래스, 객체 및 메소드의 개념

- 인간이 이해하기 쉬운 사물이나 개념을 객체(Object)로 표현

##### (1-1) 클래스(Class)

- 객체의 형식을 의미, 객체의 속성값(자료구조)과 처리 방법(메소드)을 한 묶음으로

##### (1-2) 객체(Object)

- 사물이나 개념을 의미
- 클래스의 인스턴스(Instance)
- 밴, 아우디, 스포츠카는 자동차 클래스의 인스턴스

![alt](/assets/images/post/ComputerStudy/253.png)

#### (2) 추상화, 캡슐화, 상속성 및 다형성 개념

![alt](/assets/images/post/ComputerStudy/254.png)

##### (2-1) 추상화(Abstraction)

- 클래스 또는 객체를 어떤 속성과 메소드를 통하여 나타내는지를 의미
- 애플리케이션 프로그램이 꼭 필요로 하는 **속성과 메소드만**을 추려서 클래스나 객체로 표기

##### (2-2) 캡슐화(Encapsualtion)

- 객체 안에 속성과 메소드가 존재하고, 이들의 접근이 외부로부터 통제 되므로 객체 내부의 행위가 내부에 그치고,  
  다른 객체에 영향을 미치지 않는다는 개념
- 객체 간에 서로 독립적으로 존재하기 때문에, 전체 프로그램의 구조를 이해하기 용이

##### (2-3) 상속성(Inheritance)

- 하나의 클래스는 상위 클래스의 모든 속성 및 메소드를 상속

##### (2-4) 다형성(Polymorphism)

- 기본 클래스(Shape)와 가족으로 가지는 클래스(Line, Triangle, Circle)
- 기본 클래스(Shape)를 위한 메소드로 Draw, Area, Boundary를 실행하는 방법이 다른 메소드가 존재
- 실제 호출되어 실행되는 객체는 상황에 따라 기본 클래스(Shape)의 메소드(Draw,Area,Boundary)가 아니고,  
  가족 중 한 객체 (Line,Triangle,Circle)일 수 있음

![alt](/assets/images/post/ComputerStudy/255.png)

#### (3) 절차적 언어와 객체지향 언어의 차이점

- 절차적 언어는 다른 프로시저를 호출할 때 매개변수 이용
- 객체지향 언어에서는 한 객체가 다른 객체에 **메세지(Message)**를 보냄

![alt](/assets/images/post/ComputerStudy/256.png)

### 2) 객체지향 언어의 종류

#### (1) C++ 언어

- 1980년대 벨 연구소에서 C언어를 확장하여 객체지향 개념을 적용

#### (2) Java

- 1995년 Sun Microsystems사가 차세대 프로그래밍 언어로 개발
- 일반 애플리케이션과 웹 애플리케이션 및 소형 가전기기에도 적요
- Java 컴파일러는 일종의 중간 형태의 기계어인 바이트 코드(Byte Code)로 번역, 실행시에는 자바 가상머신  
  (JVM)에서 실행

#### (3) Python

- 1991년도 반 로섬이 발표, 비영리 단체에서 관리
- Java와 유사하게 바이트 코드로 번역해 놓고, 인터프리터 방식으로 플랫폼에 독립적인 **대화식** 객체지향 언어
- 실행 시 데이터 형을 검사하는 동적 타이핑, 작성하기 용이, 라이브러리가 풍부
