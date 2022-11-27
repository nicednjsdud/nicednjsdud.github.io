---
title: (컴퓨터 개론) 5-1 프로그래밍 언어의 개념
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로그래밍 언어의 개념
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2022-11-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 프로그래밍 언어의 개념

## 1. 프로그래밍 언어의 번역기

- 소프트웨어는 프로그래밍 언어로 작성된 프로그램의 집단을 의미
- 과거의 프로그래밍 언어는 복잡하고 전문가만이 작성하였지만, 오늘날에는 비전문가도 쉽고 간단하게 작성할 수 있음

### 1) 프로그래밍 언어의 개념

- 컴퓨터에 사용하기 위해서 만든 인공 언어

#### (1) 프로그래밍 언어의 계층

![alt](/assets/images/post/ComputerStudy/240.png)

1. 컴퓨터가 이해할 수 있는 **유일한 언어**는 0과 1로 구성된 기계어뿐
2. 기계어와 자연어의 중간 형태로 개발된 **인공 언어**가 프로그래밍 언어(저급언어 + 고급언어)
3. 저급언어는 기계어와 어셈블리어로 구성 (기계어와 1:1로 대응시켜 기호화 한 언어가 어셈블리 언어)

![alt](/assets/images/post/ComputerStudy/241.png)

#### (2) 저급언어 (Low level Language)

- 기계어 중심 언어로 컴퓨터가 명령을 직접 인식하기 때문에 처리 속도는 빠르지만, **하드웨어에 의존적**

##### (2-1) 기계어

- 직접 실행하므로 처리 속도가 고속
- 컴퓨터 기종 간에 호환성이 없음

##### (2-2) 어셈블리어

- 기계어와 1:1로 대응시켜 사용자가 이해하기 쉽도록 이진 코드를 **기호화환 언어**
- 기계어보다 작성이 쉽지만, 컴퓨터 기종간에 호환성이 없어 전문 프로그래머만 사용

![alt](/assets/images/post/ComputerStudy/242.png)

#### (3) 고급언어 (High level Language)

- 일상생활에서 사용하는 자연어와 유사하기 때문에 배우기 쉽고, 쓰기 쉬운 언어로  
  **컴퓨터 기종과 관계없이** 활용할 수 있음

##### (3-1) 언어 번역 프로그램

![alt](/assets/images/post/ComputerStudy/243.png)

- 고급 언어는 기계어로 번역되기 위해서는 언어 번역 프로그램이 필요함
- 원시 프로그램을 목적 프로그램으로 번역하기 위해서는 **언어 번역 프로그램**(컴파일러, 인터프리터)이 필요
- 목적 프로그램을 실행 가능한 기계어로 번역해주기 위해서는 링커와 로더가 필요

##### (3-2) 컴파일러

- 고급언어(C,C++,C#,Java 등)로 작성한 원시 프로그램 전체를 목적 프로그램으로 번역해줌
- 효율성 강조

##### (3-3) 인터프리터

- 원시 명령문 단위로 하나씩 번역하여 즉시 실행
- 목적 프로그램을 생성하지 않음

![alt](/assets/images/post/ComputerStudy/244.png)

## 2. 프로그래밍 언어의 역사와 구조

- 프로그래밍 언어는 기계어 중심에서 인간이 사용하기 편리하게, **자연어**와 유사하게 발전할 것
- ex) 인공지능
- 프로그래밍 언어의 패러다임은 접근방법을 개념적으로 분류 P-O-D-F

![alt](/assets/images/post/ComputerStudy/245.png)

### 1) 프로그래밍 언어의 종류

#### (1) 절차적 언어 (Procedural Programming Language)

- 명령어 언어(Imperative Language)로, 기본적으로 알고리즘을 표현하기 위한 **명령어들의 집합으로** 구성
- 구조적 프로그래밍 개념 (순차, 선택, 반복)

#### (2) 객체지향 언어 (Object-Oriented Programming Language)

- 객체(Object)라는 엔티티에 데이터 구조와 메소드 (Method)가 포함
- 객체 내의 데이터를 접근하기 위하여 필히 객체의 메소드를 통해 가능

#### (3) 선언적 언어 (Declarrative Programming Language)

- 절차적 언어 : "문제를 어떻게 풀지 (How to solve the problem)"를 기술
- 선언적 언어 : "문제가 무엇인지 (What the problem is)"를 정의
- 시뮬레이션 언어 GPSS, 논리적 언어 Prolog, 데이터베이스 질의어 SQL등

#### (4) 함수형 언어 (Functional Programming Language)

- 블록 단위의 프로그램이 마치 수학의 함수와 같이 작용
- 인공지능 언어 LISP, Scheme 등

#### (5) 4세대 프로그래밍 언어

- 제 1세대 언어 : 기계어
- 제 2세대 언어 : 어셈블리어
- 제 3세대 언어 : 고수준 프로그래밍 언어

##### 제 4세대 언어

- 초고수준 언어로 선언적 언어의 특성을 가짐
- How to do(작업의 방법)에서 What to do(작업의 대상) 표현 방식의 변화
- Visual Studio(Visual Basic, Visual C++), Delphi, PowerBuilder, SQL, RPG 등
- 인공지능 언어 : LISP, Prolog
- 웹 문서 작성 : HTML, XML
- 사용자 인터랙션 : JavaScript, Perl, Ajax

![alt](/assets/images/post/ComputerStudy/246.png)

### 2) 프로그래밍 언어의 구조

#### (1) 프로그램은 세 가지 유형의 문장

- 선언문 : 변수의 자료형, 상수의 선언
- 명령문 : 프로그램의 알고리즘을 수행할 명령어
- 주석 : 프로그램을 이해하기 쉽게 설명한 문장

#### (2) 프로그램의 선언부와 명령부

![alt](/assets/images/post/ComputerStudy/247.png)

#### (3) 변수와 자료형 (Data Type)

- Integer,float(real), character, Boolean
- C, C++, Java에서 사용

#### (4) 행렬(Array)과 스트럭처(Structure)

- 행렬 : 같은 유형의 데이터가 모인 자료구조
- 레크드 또는 스트럭처 : 다른 유형의 데이터가 모인 자료구조

#### (5) 리터럴(Literal)과 상수(Constant)

![alt](/assets/images/post/ComputerStudy/248.png)

#### (6) 배정문 (Assignment statement)

```c
  A = X + Y; // C,C++,Java
  A <- X + Y // APL
```

#### (7) 제어문 - 조건문과 반복문

- 구조적 프로그래밍 (Structured Programming)
- 조건문 : if-then-else, switch
- 반복문 : while문, for문

#### (8) 프로시저(Procedure)와 함수(function)

- 모듈화 프로그래밍
- 프로시저(호출한 곳으로 분기)와 함수(함수값 만 전달)
- 전역변수와 지역변수

##### 프로그램과 프로시저의 실행 순서

![alt](/assets/images/post/ComputerStudy/249.png)

##### 사례

![alt](/assets/images/post/ComputerStudy/250.png)

#### (9) 매개변수(Parameter)의 값 전달 방식

- 형식 매개변수(Formal Parameter)와 실 매개변수(Actual Parameter) (=실제 데이터 값)
- 프로시저를 호출할 때 매개변수 값을 전달하는 방식

##### (9-1) 값에 의한 호출(Call by Value)

- 호출하는 프로그램에서 호출당하는 프로시저로 한번 실 매개변수 값을 전달하면 그것으로
  끝남

##### (9-2) 참조에 의한 호출(Call by Reference)

- 호출하는 프로그램에서 호출당하는 프로시저로 매개변수 값을 전달하는 것이 아니고 매개
  변수가 저장되어 있는 메모리 주소를 대신 전달

#### (10) 프로그램 언어의 번역 과정

- 렉시컬 분석 과정: 토큰(Token)의 생성
- 파싱(Parsing): 파스트리의 생성
- 코드 생성기: 목적 프로그램의 생성

![alt](/assets/images/post/ComputerStudy/251.png)

##### (10-1) 렉시컬 분석 (Lexical Analysis)

- 토큰의 생성
- 토큰은 변수 이름, 상수 이름, 리터럴, 예약어
- 더 이상 분리할 수 없는 프로그램에서 가장 작은 단위

##### (10-2) 구문 분석 (Syntax Analysis)

- 특정 명령문이 구문 다이어그램으로 표현
- 명령문을 구문 다이어그램에 맞게 분석하여 하나의 트리 형태로 생성하여 오류검사

![alt](/assets/images/post/ComputerStudy/252.png)

##### (10-3) 터미널(Terminal)과 논터미널(Nonterminal)

- 사례: 배정문에서 “=”의 오른쪽에 오는 표현식(Expression)
- Term과 factor는 논터미널
