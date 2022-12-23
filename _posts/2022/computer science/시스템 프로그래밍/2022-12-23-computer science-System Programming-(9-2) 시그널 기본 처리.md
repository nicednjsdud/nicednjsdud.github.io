---
title: (시스템 프로그래밍) 9-2 시그널 기본 처리
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

# 시스템 프로그래밍 - 시그널 기본 처리

## 1. 시그널 핸들러 함수

### 1) 시그널 보내기 : kill 명령

- 프로세스에 시그널을 보내는 명령
- 예) 3255 프로세스에 9번 시그널(SIGKILL)보내기 -> 프로세스 강제종료
- 블로그 주인은 스프링 부트에서 톰캣이 중복 실행 오류 떳을때 사용

```c
  # kill -9 3255
```

- pid에 대응하는 프로세스에 sig로 지정한 시그널 보냄
- sig 0(NULL 시그널) : 실제로 시그널 보내지 않고 정상인지 오류인지 확인
- 함수원형

```c
  #include <sys/types.h>
  #include <signal.h>

  int kill(pit_t pid, int sig);
```

- pid : 시그널을 받을 프로세스의 ID
- sig : pid로 지정한 프로세스에 보내려는 시그널

#### (1) pid 값에 따른 처리

##### (1-1) pid가 0보다 큰 수

- pid로 지정한 프로세스에 시그널 발송

##### (1-2) pid가 -1이 아닌 음수

- 프로세스 그룹ID가 pid의 절대값인 프로세스 그룹에 속하고 시그널을 보낼 권한을 가지고 있는 모든 프로세스에  
  시그널 발송

##### (1-3) pid가 0

- 특별한 프로세스를 제외하고 프로세스 그룹ID가 시그널을 보내는 프로세스의 프로세스 그룹ID와 같은 모든  
  프로세스에게 시그널 발송

##### (1-4) pid가 -1

- 시그널을 보내는 프로세스의 유효 사용자ID가 root가 아니면, 특별한 프로세스를 제외하고  
  프로세스의 실제 사용자ID와 시그널을 보내는 프로세스의 유효 사용자ID와 같은 모든 프로세스에 시그널 발송

### 2) 시그널 보내기 : raise(2)

- 함수를 호출한 프로세스에 시그널 발송

```c
  #include <signal.h>

  int raise(int sig);
```

- sig : 보내려는 시그널 번호

### 3) 시그널 보내기 : abort(3)

- 함수를 호출한 프로세스에 SIGABRT시그널 발송
- SIGABRT 시그널은 프로세스를 비정상적으로 종료시키고 코어덤프 생성

```c
  #include <stdlib.h>

  void abort(void);
```

- 프로세스 종료, 리턴하지 않음

### 4) 시그널 핸들러 지정 : signal(3)

- 함수원형

```c
  #include <signal.h>

  void (*signal(int sig, void (*disp)(int)))(int);
```

- sig : 시그널 핸들러로 처리하려는 시그널
- disp : 시그널 핸들러 함수명

#### (1) disp 인자

- SIG_IGN : 시그널을 무시하도록 지정 (ignore)
- SIG_DFL : 기본 처리 방법으로 처리하도록 지정 (default)
- signal함수는 시그널이 들어올 때마다 시그널 핸들러를 호출하려면 매번 시그널 핸들러를 재 지정해야함

### 5) 시그널 핸들러 지정 : sigset(3)

- signal 함수와 달리 시그널 핸들러가 한 번 호출된 후에 기본동작으로 재설정 하지 않고, 시그널 핸들러를  
  자동으로 재 지정함
- 성공 : 시그널 핸들러 함수의 주소
- 실패 : SIG_ERR 리턴

```c
  #include <signal.h>

  void (*sigset(int sig, void(*disp)(int)))(int);
```

- sig : 시그널 핸들러로 처리하려는 시그널
- disp : 시그널 핸들러 함수명

## 2. 시그널 집합 (signal set)

### 1) 개념

- 시그널을 개별적으로 처리하지 않고, 복수의 시그널을 처리하기 위해 도입한 개념
- 시그널 : 비트 마스트로 표현, 각 비트가 특정 시그널과 1:1로 연결
- 비트 값이 1이면 해당 시그널 설정
- 비트 값이 0이면 시그널 설정 않음

#### (1) 시그널 집합의 처리를 위한 구조체 : sigset_t

```c
  typedef struct{
            unsigned int _sigbits[4];
  } sigset_t;
```

### 2) 시그널 집합 비우기 : sigemptyset(3)

- 시그널 집합에서 모든 시그널 0으로 설정

```c
  #include <signal.h>

  int sigemptyset(sigset_t *set);
```

- set : 비우려는 시그널 집합의 주소

### 3) 시그널 집합에 모든 시그널 설정 : sigfillset(3)

- 시그널 집합에서 모든 시그널 0으로 설정

```c
  #include <signal.h>

  int sigfillset(sigset_t *set);
```

- set : 설정하려는 시그널 집합의 주소

### 4) 시그널 집합에 시그널 설정 추가 : sigaddset(3)

- signo로 지정한 시그널을 시그널 집합에 추가

```c
  #include <signal.h>

  int sigaddset(sigset_t *set, int signo);
```

- set : 시그널을 추가하려는 시그널 집합의 주소
- segno : 시그널 집합에 추가로 설정하려는 시그널

### 5) 시그널 집합에서 시그널 설정 삭제 : sigdelset(3)

- signo로 지정한 시그널을 시그널 집합에서 삭제

```c
  #include <signal.h>

  int sigdelset(sigset_t *set, int signo);
```

- set : 시그널을 삭제하려는 시그널 집합의 주소
- segno : 시그널 집합에서 삭제하려는 시그널

### 6) 시그널 집합에서 설정된 시그널 확인 : sigismember(3)

- signo로 지정한 시그널이 시그널 집합에 포함되어 있는지 확인

```c
  #include <signal.h>

  int sigismember(sigset_t *set,int signo);
```

- set : 확인하려는 시그널 집합의 주소
- segno : 시그널 집합에서 설정되었는지 확인하려는 시그널
