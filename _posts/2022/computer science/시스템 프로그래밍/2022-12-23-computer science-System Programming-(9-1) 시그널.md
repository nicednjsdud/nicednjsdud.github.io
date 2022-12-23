---
title: (시스템 프로그래밍) 9-1 시그널
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 시그널
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-12-23 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 시그널

## 1. 시그널

### 1) 시그널의 개념

- 소프트웨어 인터럽트
- 프로세스에 뭔가 발생했음을 알리는 간단한 메세지를 비동기적으로 보내는 것
- 무엇이 발생했는지를 표시하는 미리 정의된 상수 함수

### 2) 발생사유

- 0으로 나누기처럼 프로그램에서 예외적인 상황이 일어나는 경우
- kill 함수처럼 시그널을 보낼 수 있는 함수를 사용해서 다른 프로세스에 시그널을 보내는 경우
- 사용자가 Ctrl + C 와 같이 인터럽트 키를 입력한 경우

### 3) 시그널 처리방법

- 각 시그널에 지정된 기본 동작 수행.
- 대부분의 기본 동작은 **프로세스 종료**
- 시그널을 무시
- 시그널 처리를 위한 함수(시그널 핸들러)를 지정해놓고 시그널을 받으면 해당 함수 호출
- 시그널이 발생하지 않도록 블록처리

![alt](/assets/images/post/ComputerStudy/452.png)

![alt](/assets/images/post/ComputerStudy/453.png)

## 2. 시그널 발생 및 처리

### 1) 시그널 보내기 함수

- 프로그램에서 시그널 보낼 때 사용하는 함수
- 프로세스 종료시 kill 함수 사용

![alt](/assets/images/post/ComputerStudy/454.png)

### 2) 시그널 핸들러 지정 함수

#### (1) 시그널 핸들러

- 시그널을 받았을 때 이를 처리하기 위해 지정된 함수
- 프로세스를 종료하기 전에 처리할 것이 있거나, 특정 시그널에 대해 종료하고 싶지 않을 경우 지정

![alt](/assets/images/post/ComputerStudy/455.png)

### 3) 시그널 집합 관련 함수

- 시그널 집합 : 여러개의 시그널 처리 (POSIX 표준)

![alt](/assets/images/post/ComputerStudy/456.png)

### 4) 시그널 처리 제어 함수

- sigaction()
- 시그널을 받아 처리할 시그널 지정 및 플래그를 성정해 시그널 처리 과정 제어 가능
- 시그널 핸들러가 수행되는 동안 다른 시그널 블록할 수 있음

![alt](/assets/images/post/ComputerStudy/457.png)

### 5) 알람 시그널 관련 함수

![alt](/assets/images/post/ComputerStudy/458.png)

### 6) 기타 시그널 관련 함수

- 일정한 시간이 지난 후에 자동으로 시그널 발생
- 한번 혹은 일정 시간 간격의 주기적 발생

![alt](/assets/images/post/ComputerStudy/459.png)
