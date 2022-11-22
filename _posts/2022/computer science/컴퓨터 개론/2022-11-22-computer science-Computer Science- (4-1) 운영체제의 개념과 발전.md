---
title: (컴퓨터 개론) 4-1 운영체제의 개념과 발전
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 운영체제의 개념과 발전
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2022-11-22 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 운영체제의 개념과 발전

## 1. 운영체제의 목적과 발전

### 1) 운영체제의 시동

- 운영체제에 가장 중요한 것
  - **스케줄링**과 이를 효율적으로 **운영하는 것**을 강조

### 2) 소프트웨어의 개념

- 소프트웨어의 위상

![alt](/assets/images/post/ComputerStudy/138.png)

- 소프트웨어의 기능

![alt](/assets/images/post/ComputerStudy/139.png)

### 3) 소프트웨어의 계층

![alt](/assets/images/post/ComputerStudy/141.png)

#### (1) 시스템 소프트웨어 (System Software)

- 하드웨어를 운영하고 관리, 운영하는 소프트웨어

#### (2) 미들 웨어 (Middleware)

- 서로 다른 통신 규약, 시스템구조, 운영체제, DB간에 다양한 서비스를 지원하는 소프트웨어

#### (3) 응용 소프트웨어 (Application Software)

- 어떤 일을 처리할 수 있도록 프로그램을 **미리 만들어 놓은 소프트웨어**
- 업무 처리 별로 별도의 SW가 있다.

### 4) 운영체제의 개념

- 컴퓨터 5대 장치 자원을 제어하여 명령을 처리하는 프로그램의 집합체로  
  공항에서 항공기의 관제탑 역할
- 사용자가 컴퓨터 전문지식이 없어도 컴퓨터 각종 자원을 효과적으로 사용할 수 있도록 지원
- 컴퓨터에 운영체제가 없으면 자동차에 엔진이 없고, 오케스트라의 지휘자가 없는 것과 동일

#### (1) 운영체제의 처리 과정

1. 사용자가 문서 작성 응용 소프트웨어에 문서를 출력하도록 지시함.
2. 워드 프로세싱 응용 소프트웨어는 '문서가 프린터에 보내져야 한다'고 운영 체제에 신호를 보냄
3. 운영 체제는 그 문서를 프린터에 보냄

### 5) 운영체제의 발전

#### (1) 배치 처리 (Batch Processing)

- 처리할 프로그램을 원칙적으로 도착 순서에 따라 하나씩 실행 하는 것으로  
  **일괄처리**(데이터를 모아서 한꺼번에 일괄처리)라고도 부름
- FIFO (First-In First-Out) **선입 선출**
- 처리할 프로그램이나 명령어를 작업 또는 잡(Job)

##### (1-1) 배치 프로세싱의 개념

![alt](/assets/images/post/ComputerStudy/140.png)

#### (2) 상호대화식 처리 (Interactive Processing)

- 이용자와 컴퓨터 간에 상호대화 방식
- 모니터를 통해 프로그램의 실행 도중에 데이터를 제공하거나 프로그램을 제어, 경우에 따라서  
  중간 결과 확인
- 인터프리터

![alt](/assets/images/post/ComputerStudy/142.png)

#### (3) 시분할 시스템(다중프로그래밍, 다중작업)

- 다중 프로그래밍 : **다수의 사용자가** 여러개의 프로그램을 동시에 실행
- 다중작업(Multitasking) : **여러개의 서로 다른** 프로그램이 동시에 실행
  - ex) PC에서 음악을 들으면서 문서작업 작성
- CPU가 하나인 경우, **CPU 시간을 분할**(Time Slice)하여 순서대로 돌아가면서 실행하는 방식이  
  시분할(Time Sharing)기법

![alt](/assets/images/post/ComputerStudy/143.png)

#### (4) 실시간 처리 (Real Time Processing)

- 컴퓨터로 하여금 정해진 짧은 시간(거의 실시간) 내에 작업을 완료(데이터 입력시 즉시 처리)

#### (5) 병렬처리와 다중처리

##### (5-1) 병렬처리

- Parallel Processing
- **하나의 프로그램**A를 여러개의 작업{A1,A2,...,A6}로 분할하여 **몇개의 CPU**에 할당하여 빠른 실행 결과

##### (5-2) 다중처리

- Multiprocessing
- **여러개의 프로그램**을 **여러개이 CPU**가 실행하여 전체적인 성능 향상

![alt](/assets/images/post/ComputerStudy/144.png)

#### (6) 모바일 운영체제

- 컴퓨터에 비해 장치 규모가 작기 때문에 각 기기의 특수한 상황에 따라 기능을 주로 요구하므로  
  운영체제의 핵심 기능만 삽입
- 임베디드 장치에 필요한 시스템 소프트웨어를 **임베디드 운영체제**라고 하며,  
  고사양의 임베디드 운영체제로는 Windows CE와 임베디드 Linux

### 6) 운영체제의 역사

#### (1) 초창기의 운영체제

- 컴퓨터 시스템마다 **자체 운영체제**
- 예) IBM OS/360, CDC SCOPE

#### (2) 유닉스(Unix) 운영체제

- 1969년 AT&T사 벨 연구소의 토마스 리치등이 어셈블리어로 개발, 1971년 C언어로 다시 작성하여  
  운영체제 오픈
- UNIX 개발자들에게 **무상으로 제공**, 다양한 컴퓨터에서 구현

#### (3) 리눅스(Linux)

- UNIX 계열의 운영체제 중 대표적인 **공개 소프트웨어**
- 1991년 리눅스 토발즈가 개발
- 공개 소프트웨어 운동은 원래 MIT 리차드 스톨만 교수가 UNIX와 유사한 운영체제 GNU를  
  개발하면서 시작, '오픈 소스(Open Source)'용어 탄생

#### (4) 데스크탑 운영체제

- DOS, MS Windows, Mac OS, UNIX, Linux 등
- GUI방식 : 1984년 Mac OS, 1980년대 후반 MS Windows

#### (5) 운영체제의 주요 역할

- 펌웨어(Firmware) 형태의 시스템 소프트웨어로 GUI를 통해 사용자와 각 장치, 그리고  
  소프트웨어에게 명령을 내려 일을 처리

![alt](/assets/images/post/ComputerStudy/145.png)
