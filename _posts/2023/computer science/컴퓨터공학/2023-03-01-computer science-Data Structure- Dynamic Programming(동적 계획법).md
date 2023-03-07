---
title: (10분 테크톡) Process vs Thread
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: Process vs Thread
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-03-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Process vs Thread

## 키워드

### 1) 실행 단위

- cpu core에서 실행하는 하나의 단위로 프로세스와 스레드를 포괄하는 개념

### 2) (부연 설명이 없는) 프로세스

- 하나의 스레드만 가지고 있는 단일 스레드 프로세스

### 3) 동시성

- 한 순간에 여러가지 일이 아니라, 짧은 전환으로 여러가지 일을 동시에 처리하는 것 처럼 보이는 것

## 순서

1. Process & Thread
2. Multi-process vs. Multi-thread
3. Muilti-core
4. 요약

## 1. 프로그램과 프로세스, 프로세서

- 피자레시피가 적힌 종이 - 프로그램
- 프로세스 - 피자

### 1) 프로그램 (Program)

- 어떤 작업을 위해 운영체제 위에서 **실행할 수 있는 파일**
- 예를 들어 웹 브라우저, 워드 프로세서, 카카오톡 등

### 2) 프로세스 (Process)

- 운영 체제 위에서 **실행중인** 프로그램
- 프로그램 명령어와 데이터들이 메모리에 올라오고 실행 중 또는 실행 대기중인 상태

#### 2-1) 프로세스의 구조

##### Stack

- 호출된 함수, 지역변수 등 임시 데이터

##### Heap

- 동적으로 생긴 데이터
- 예) new Object(), malloc()

##### Data

- 전역변수
- 예) static 변수, global 변수

##### Code

- 프로그램의 코드

### 3) 프로세서 (Processor)

- 프로세스가 **동작**될 수 있도록 하는 하드웨어 (= cpu)

#### 3-1) 동작

- 프로그램의 자원들이 메모리에 올라오고, 실행 되어야 할 코드의 메모리 주소를 CPU의 레지스터로 올리는 것

![alt](/assets/images/post/ComputerStudy/812.png)

## 2. Thread

### 1) 스레드

- 프로세스 내에서 실행되는 작업 흐름의 단위
- Code, Data, Heap 영역 공유

![alt](/assets/images/post/ComputerStudy/816.png)

## 3. Multi-process & Multi-thread

![alt](/assets/images/post/ComputerStudy/813.png)

### 1) Multi-process

- 각 프로세스는 독립적
- IPC를 사용한 통신
- 자원 소모적, 개별 메모리 차지
- Context Switching 비용이 큼
- 동기화 작업이 필요하지 않음

### 2) Multi-thread

- Thread끼리 긴밀하게 연결되어 있음
- 공유된 자원으로 통신 비용 절감
- 공유된 자원으로 메모리가 효율적임
- Context Switching 비용이 적음
- 공유 자원 관리를 해야함

#### 2-1) 주의점

- 디버깅이 까다로움
- 한 프로세스안의 스레드에 문제가 생기면 같은 프로세스안의 스레드도 같이 문제가 생김
- 같은 데이터를 공유하기에, 데이터 동기화에 신경 써야함

## 4. Multi - core

![alt](/assets/images/post/ComputerStudy/814.png)

- 멀티프로세스랑 멀티쓰레드는 `처리방식`의 일종 -> 소프트웨어 분야의 가까움
- 멀티코어 -> 하드웨어의 측면에 가까움
- 멀티코어는 벙렬 처리
  - 물리적으로 여러 코어를 사용해서 다수의 실행 단위를 한순간에 처리할 수 있게 해줌

![alt](/assets/images/post/ComputerStudy/815.png)

### 1) 동시성 Concurrency

- 하나의 코어에서 하나 이상의 프로세스(혹은 쓰레드)가 번갈아가면서 진행되지만 동시에 진행되는 것 처럼 보이는 것

### 2) 병렬 처리 Parallelism

- 둘 이상의 코어에서 동시에 하나 이상의 프로세스( 혹은 스레드)가 한꺼번에 진행되는 것

## 5. 리눅스에서 Process와 Thread

- 리눅스 **커널**에서는 프로세스와 스레드를 동일하게 봄
  - 스레드는 사용자 스레드와 커널 스레드로 나뉜다.
  - 리눅스 커널 스레드는 일대일 모델
  - 사용자 스레드당 커널 스레드 하나가 매칭되어있다.
  - 그래서 `각각의 쓰레드가 하나의 프로세스다`라고 표현

## 6. 요약

- 프로세스는 프로그램이 실행 된 것이다.
- 스레드는 한 프로세스 내에서 나뉘어진 하나 이상의 실행 단위이다.
- 한 어플리케이션에 대한 작업을 동시에 하기 위해서는 2가지 처리 방식(멀티 프로세스, 멀티 스레드)이 있다.
- 동시에 실행되는 것처럼 보이기 위해 실행 단위는 시분할로 cpu를 점유하며 context switching을 한다.
- 멀티 프로세스는 독립적인 메모리를 가지고 있지만 멀티스레드는 자원을 공유한다. 그것에 따른 각각의 장단점이 있다.
- 멀티 코어는 하드웨어 측면에서 실행 단위를 병렬적으로 처리할 수 있도록 여러 프로세서가 있는 것이다.

## 출처

<a href="https://www.youtube.com/watch?v=1grtWKqTn50">코다의 Process vs Thread</a>
<a href="https://www.youtube.com/watch?v=DmZnOg5Ced8">쪼밀리와 오구의 Process vs Thread</a>
