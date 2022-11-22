---
title: (컴퓨터 개론) 4-2 운영체제의 구성
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 운영체제의 구성
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2022-11-22 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 운영체제의 구성

## 1. 운영체제의 시동

- 자동차를 운행할 때 시동을 거는 것과 같이 컴퓨터에 전원을 넣으면 운영체제가 시동 됨을 강조

### 1) 컴퓨터의 시동

#### (1) 부트 로더(Boot Loader)

- 운영체제를 컴퓨터 시스템 내부로 가져와 작동
- 부트 로더는 ROM 메모리에 저장
  - DRAM은 휘발성 기억장치, ROM은 비휘발성
  - ROM에 저장되어 있는 부트로더는 펌웨어(Firmware)

![alt](/assets/images/post/ComputerStudy/147.png)

### 2) 사용자 인터페이스와 커널

![alt](/assets/images/post/ComputerStudy/148.png)

- 컴퓨터 사용자가 컴퓨터 시스템에게 원하는 작업을 요청하기 위한 상호작용을 지원
- UNIX에서는 사용자 인터페이스를 쉘(Shell)
- GUI 방식의 쉘을 윈도우 관리자(Windows Manager)

#### (1) 사용자 인터페이스의 유형

- 명령어(Command Line) 방식
- 메뉴(Menu Driven) 방식
- 그래픽 사용자 인터페이스(GUI: Graphic User Interface)

![alt](/assets/images/post/ComputerStudy/149.png)

#### (2) 커널(Kernel)

- 프로세스 관리자(Process manager) : 프로세스 관리
- 메모리 관리자(Memory manager) : 기억장치 관리
- 파일 관리자(File manager) : 파일 저장, 검색 관리
- 장치 관리자(Device manager) : 컨트롤러 제어 관리

![alt](/assets/images/post/ComputerStudy/150.png)

### 3) 메모리와 파일 관리

#### (1) 가상 메모리

- 실행 중인 프로그램을 적당한 크기로 나우어 현재 실행에 **꼭 필요한 부분을 RAM에 배치하여**,  
  RAM의 용량이 훨씬 큰 것처럼 느끼도록 처리하는 방식

##### (1-1) 가상 메모리 기법

- 페이징(Paging) 기법 : 크기가 일정
- 세그멘테이션(Segmentation) 기법 : 크기가 가변
- 스와핑 : **프로그램 단위로** 주기억장치와 보조기억장치에 필요 시 적재하는 방식
- 하드디스트의 파일을 계층적 구조에 따라 디렉토리(Diretory)와 폴더(Folder)에 저장

![alt](/assets/images/post/ComputerStudy/151.png)

#### (2) 파일경로(Directory Path) : 계층적 디렉토리

- Unix의 예 : `C://Introduction to Computers/text/ch03_software.ppt`
- 파일 확장자의 예

![alt](/assets/images/post/ComputerStudy/152.png)

## 2. 컴퓨터 실행의 제어

- 컴퓨터는 모든 일을 몇개의 처리하는 **단위(Process)**로 나누고, 구성해서 일을 처리한다.

### 1) 프로세스의 개념

- 프로그램을 실행할 목적으로 생성된 동적 엔티티로 컴퓨터에서 작업을 하는 단위

#### (1) 프로세스의 처리단계

```c
  "준비(Ready)", "실행(Running)",
  "인터럽트(Interrupt)", "대기(Waiting", "종료(Terminated" 상태
```

![alt](/assets/images/post/ComputerStudy/153.png)

#### (2) 프로세스의 관리

- 대기 상태(Job Queue) : 처리할 작업들
- 준비 상태 (Ready Queue) : 프로세스 단위들

#### (3) 프로세스 처리 방식

- FCFS(First Come First Served) : 적재 순서대로 처리
- SPN(Shortest Process Next) : 처리시간이 작은 것
- 시분할(Time Sharing) : 타임슬롯을 “Round-Robin” 방식으로 배정하여 적재

![alt](/assets/images/post/ComputerStudy/154.png)

### 2) 컴퓨터 자원의 경쟁

#### (1) 세마포(Semaphore)

##### (1-1) 깃발(Flag)

- 깃발을 세마포라 함
- ex) 프린터의 사용

```c
  "Flag = 1"이면 프린터를 이용할 수 있는 상태
  "Flag = 0"이면 프린터를 사용할 수 없는 상태
```

##### (1-2) 크리티컬 리전(Critical Region)

- 프로그램의 어떤 부분이 시작되어 완료될 때까지 다른 프로세스가 **간섭하면 안되는** 프로그램의 부분
- 세마포를 이용하여 크리티컬 리전 표시는 잠금(Lock), 작업 완료시 해제(Unlcok)

##### (1-3) 세마포를 이용한 자원의 할당

![alt](/assets/images/post/ComputerStudy/155.png)

#### (2) 데드록(Deadlock)

- 프로세스 간에 자원을 차지하려고 경쟁하다 생기는 문제
- 더 이상 프로세스의 처리 작업을 진행할 수 없는 상태가 발생
- 병목 현상

![alt](/assets/images/post/ComputerStudy/156.png)

##### (2-1) 데드록 발생 조건

- 공유할 수 없는 자원의 경쟁이 존재하므로 발생한다.
- 필요한 자원을 한꺼번에 점유하지 않고 하나씩 점유하기 때문이다.
  - 일단 점유한 자원은 필요한 자원을 모두 차지할때까지 놓아주지 않기 때문이다.
- 자원이 프로세스에 의해 점유된 후에는 강제로 뺏을 수 없기 때문이다.

##### (2-2)

- 데드록 탐지(3가지 발생조건 탐지)와 데드록 회피(발생하지 말도록 운영체제가 통제)

#### (3) 스풀링(Spooling)

- 가상프린터에 출력 보낸 후 여유 있을 때 실제 출력하는 방식

#### (4) 프로세스 기아(Starvation)

- 데드록이 발생하지 않도록 해도 또 다른 문제가 프로세스의 **기아 문제**
- 영원히 자원을 차지하지 못하는 프로세스가 발생

![alt](/assets/images/post/ComputerStudy/157.png)
