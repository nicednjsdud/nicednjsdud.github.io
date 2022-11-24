---
title: (시스템 프로그래밍) 5-2 프로세스 식별
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로세스 식별
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-24 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 프로세스 식별

## 1. PID(ProcessID) 개념

### 1) 프로세스란?

- **실행중인 프로그램을 프로세스(process)라고 부름**
- 각 프로세스는 유일한 프로세스 번호 PID를 가짐
- 각 프로세스는 부모 프로세스에 의해 생성됨

### 2) 프로세스 식별

#### (1) PID 검색 : getpid(2)

- 이 함수를 호출한 프로세스의 PID를 리턴

```c
  #include <unistd.h>
  pid_t getpid(void);
```

#### (2) PPID 검색 : getppid(2)

- 호출한 프로세스의 부모 프로세스 PID 리턴

```c
  #include <unistd.h>
  pid_t getppid(void);
```

### 3) 프로세스 그룹

- 관련 있는 프로세스를 묶은 것으로 프로세스 그룹 ID(PGID)가 부여됨
- 작업제어 기능을 제공하는 C쉘이나 콘쉘은 명령을 파이프로 연결하여 프로세스 그룹 생성 가능

#### (1) 프로세스 그룹 리더

- 프로세스 그룹을 구성하는 프로세스 중 하나가 그룹 리더가 됨
- 프로세스 그룹 리더의 PID 가 PGID
- 프로세스 그룹 리더는 변경 가능

#### (2) PGID 검색 : getpgrp(2), getpgid(2)

```c
  #include <unistd.h>

  pid_t getpgrp(void);
  pid_t getpgid(pid_t pid);
```

- pid : PGID를 구하려는 프로세스의 ID

#### (3) PGID 변경 : setpgid(2)

```c
  #include <sys/types.h>
  #include <unistd.h>

  int setpgid(pid_t pid, pid_t pgid);
```

- pid : 프로세스 그룹에 속한 프로세스의 ID
- pgid : 새로 지정할 PGID

## 2. PID 관련 함수

### 1) 프로세스 목록 보기

- 현재 실행중인 프로세스 목록을 보려면 ps 명령 사용

![alt](/assets/images/post/ComputerStudy/191.png)

#### (1) ps aux

![alt](/assets/images/post/ComputerStudy/192.png)

#### (2) 전체 프로세스를 보려면 -ef 옵션 사용

![alt](/assets/images/post/ComputerStudy/193.png)

### 2) 세션

- POSIX 표준에서 제안한 개념
- 사용자가 로그인해 작업하고 있는 **터미널** 단위로 프로세스 그룹을 묶은 것

![alt](/assets/images/post/ComputerStudy/194.png)

#### (1) 세션 검색 : getsid(2)

- 세션 ID는 SVR4에서 정의한 개념
- 새로운 세션을 생성하면 해당 프로세스는 세션 리더가 되면 세션 리더의 PID가 세션 ID

```c
  #include <unistd.h>

  pid_t getsid(pid_t pid);
```

- pid : 자신이 속한 세션의 ID 구하려는 프로세스의 ID
