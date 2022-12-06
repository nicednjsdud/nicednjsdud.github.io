---
title: (시스템 프로그래밍) 6-3 프로세스 동기화
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로세스 동기화
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

# 시스템 프로그래밍 - 프로세스 동기화

## 1. 프로세스 동기화

### 1) 부모 프로세스와 자식 프로세스의 종료절차

- 순서와 상관없이 실행하고 먼저 실행을 마친 프로세스는 종료
- 부모 프로세스와 자식 프로세스 사이에 종료절차가 제대로 진행되지 않으면 좀비 프로세스 발생

### 2) 동기화 필요 이유

#### (1) 좀비프로세스 종료

- 실행을 종료하고 자원을 반납한 자식 프로세스의 종료 상태를 부모 프로세스가 가져가지 않으면 좀비 프로세스 발생
- **좀비 프로세스는 프로세스 테이블에만 존재**
- 좀비 프로세스는 일반적인 제거 방법은 없음
- 좀비 프로세스를 방지하기 위해 부모 프로세스와 자식 프로세스를 동기화 해야함

#### (2) 고아프로세스 종료

- 자식 프로세스보다 부모 프로세스가 먼저 종료할 경우 자식 프로세스들은 고아 프로세스가 됨
- 고아 프로세스는 1번 프로세스(init)의 자식 프로세스로 등록

## 2. 프로세스 동기화 함수

### 1) 프로세스 동기화 : wait(3)

- 자식 프로세스가 종료할 때까지 부모 프로세스를 기다리게함
- 부모 프로세스가 wait함수를 호출하기 전에 자식 프로세스가 종료하면 wait함수는 즉시 리턴
- wait 함수의 리턴값은 자식 프로세스의 PID
  - 리턴값이 -1이면 살아있는 자식 프로세스가 하나도 없다는 의미

```c
  #include <sys/types.h>
  #include <sys/wait.h>
  pid_t wait(int *stat_loc);
```

- stat_loc : 상태정보를 저장할 주소

### 2) 특정 자식 프로세스와 동기화 : waitpid(3)

```c
  #include <sys/types.h>
  #include <sys/wait.h>
  pid_t waitpid(pid_t pid, int *stat_loc,int options);
```

#### (1) pid에 지정할 수 있는 값

##### (1-1) -1보다 작은 경우

- pid의 절댓값과 같은 프로세스 그룹ID에 속한 자식 프로세스 중 임의의 프로세스의 상태값 요청

##### (1-2) -1인 경우

- wait 함수처럼 임의의 자식 프로세스의 상태값을 요청

##### (1-3) 0인 경우

- 함수를 호출한 프로세스와 같은 프로세스 그룹에 속한 임의의 프로세스의 상태값 요청

##### (1-4) 0보다 큰 경우

- 지정한 PID의 상태값 요청

#### (2) options: waitpid 함수의 리턴 조건

##### (2-1) WCONTINUED

- 수행중인 자식 프로세스의 상태값 리턴

##### (2-2) WNOHANG

- pid로 지정한 자식 프로세스의 상태값을 즉시 리턴받을 수 없어도 이를 호출한 프로세스의 실행을 블록하지 않고  
  다른 작업을 수행토록 함
