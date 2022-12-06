---
title: (시스템 프로그래밍) 6-1 프로세스 실행
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로세스 실행
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-12-06 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 프로세스 실행

## 1. 리눅스 프로세스 생성

- 프로그램 안에서 다른 프로그램을 실행해 새로운 프로세스를 생성하는 것
- 프로세스 생성 함수

```c
  프로그램 실행 : int system(const char *string);
  프로세스 생성 : pid_t fork(void);
               pid_t vfork(void);
```

- 프로세스 종료 함수

```c
  프로세스 종료 : void exit(int status);
               void _exit(int status);
  종료 시 수행할 작업 지정 : int atexit(void(*func)(void));
```

- 정상 종료시 0 리턴, 실패시 0이 아닌값

#### (1) exec 함수군

- 인자로 받은 다른 프로그램을 자신을 호출한 프로세스의 메모리에 덮어씀
- 프로세스가 수행중이던 기존 프로그램을 중지되고 새로 덮어쓴 프로그램 실행
- fork 함수와 연결해 fork 생성한 자식 프로세스가 새로운 프로그램을 실행하도록 함

#### (2) 프로세스 동기화

- 좀비 프로세스 방지

```c
  임의의 자식 프로세스 상태값 구하기 : pid_t wait(int *stat_loc);
```

### 1) fork() 함수

- 새로운 프로세스를 생성 : 자식 프로세스
- fork 함수를 호출한 프로세스 : 부모 프로세스
- **자식 프로세스는 부모 프로세스의 메모리를 복사** (공유)

#### (1) 자식 프로세스 상속받는 속성

- RUID, EUID, RGID, EGID
- 환경변수
- 열린 파일기술자
- 시그널 처리
- setuid, setgid
- 현재 작업 디렉토리
- umask
- 사용가능자원 제한

#### (2) 부모 프로세스와 다른 점

- 자식 프로세스는 유일한 PID를 가짐
- 자식 프로세스는 유일한 PPID를 가짐
- 부모 프로세스가 설정한 프로세스 잠금, 파일 잠금, 기타 메모리 잠금은 상속 안함
- 자식 프로세스의 tms구조체 값은 0으로 설정
- 부모 프로세스와 자식 프로세스는 열린 파일을 공유하므로 읽거나 쓸 때 주의해야 함

![alt](/assets/images/post/ComputerStudy/346.png)

## 2. 리눅스 프로세스 생성 함수

### 1) 프로세스 생성

#### (1) 프로그램 실행 : system(3)

- 프로그램 안에서 새로운 프로그램 실행
- 쉘까지 동작시키므로 비 효율적

```c
  #include <stdlib.h>
  int system(const char *string);
```

- string : 실행할 명령이나 실행 파일명

#### (2) fork(2)

- 새로운 자식 프로세스 생성
- **성공 시 부모는 자식 프로세스의 ID 리턴, 자식 프로세스는 0리턴, 실패 시 -1리턴**

```c
  #include <sys/types.h>
  #include <unistd.h>
  pid_t fork(void);
```

- 인자를 받지 않음
