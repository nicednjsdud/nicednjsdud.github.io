---
title: (시스템 프로그래밍) 9-3 시그널 관련 함수
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

# 시스템 프로그래밍 - 시그널 관련 함수

## 1. 시그널 관련 함수

### 1) sigaction 함수

- signal이나 sigset 함수처럼 시그널을 받았을 때 이를 처리하는 함수 지정
- signal, sigset 함수보다 다양하게 시그널 제어 가능

#### (1) sigaction 구조체

```c
  struct sigaction {
      int sa_flags;
      union{
        void (*sa_handler)();
        void (*sa_sigaction)(int, siginfo_t *, void *);
      } _funcptr;
      sigset_t sa_mask;
  };
```

- sa_flags : 시그널 전달 방법을 수정할 플래그
- sa_handler/sa_sigaction : 시그널 처리를 위한 동작 지정
- sa_flagsdp SA_SIGINFO가 설정되어 있지 않으면 sa_handler에 시그널 처리 동작 지정
- sa_flags에 SA_SIGINFO가 설정되어 있으면 sa_sigaction 멤버 사용
- sa_mask : 시그널 핸들러가 수행되는 동안 블록될 시그널을 지정한 시그널 집합
- sa_flags에 지정할 수 있는 값(sys/signal.h)

#### (2) sigaction() 함수

```c
  #include <signal.h>

  int sigaction(int sig, const struct sigaction *restrict act,
                  struct sigaction *restrict oact);
```

- sig : 처리할 시그널
- act : 시그널을 처리할 방법을 지정한 구조체 주소
- oact : 기존에 시그널을 처리하던 방법을 저장할 구조체 주소

#### (3) 시그널 발생 원인 검색

- sa_flags에 SA_SIGINFO 플래그를 지정하면 시그널 발생원인을 알 수 있음

```c
  void handler(int sig, siginof_t *sip, ucontext_t *ucp);
```

- sip : 시그널이 발생한 원인을 담은 siginfo_t 구조체 포인터
- ucp : 시그널을 받는 프로세스의 내부 상태를 나타대는 구조체 포인터

##### (3-1) siginfo_t 구조체

```c
  typedef struct{
        int si_signo;
        int si_errno;
        int si_code;
        union sigval si_value;
        union{
          ...
        }__data;
  } siginfo t;
```

- si_signo : 시그널 번호
- si_errno : 0 또는 오류번호
- si_code : 시그널 발생 원인 코드
- `__data` : 시그널 종류에 따른 값

### 2) 시그널 발생 원인 출력 : psginfo(3)

- 시그널 발생 원인을 출력 : si_code 값이 양수면 시스템에서 시그널 생성

```c
  #include <siginfo.h>
  void psiginfo(siginfo_t *pinfo, char *s);
```

- pinfo : 시그널 발생원인 정보를 저장한 구조체
- s: 출력할 문자열

## 2. 인터벌 타이머

### 1) 알람 시그널

- 일정한 시간이 지난 후에 자동으로 시그널이 발생하도록 하는 시그널
- 일정 시간 후에 한번 발생시키거나, 일정 간격을 두고 주기적으로 발송 가능
- 일정 시간이 지나면 SIGALRM 시그널 발생
- 프로세스 별로 알람시계가 하나 밖에 없으므로 알람은 하나만 설정 가능

#### (1) 알람 시그널 생성 : alarm(2)

```c
  #include <unistd.h>

  unsigned int alarm(unsigned int sec);
```

- sec : 알람이 발생시킬 때까지 남은 시간 (초 단위)

### 2) 인터벌 타이머

#### (1) 타이머의 종류

##### (1-1) ITIMER_REAL

- 실제 시간 사용
- SIGALRM 시그널 발생

##### (1-2) ITIMER_VIRTUAL

- 프로세스의 가상 시간 사용, SIGVTALRM 시그널 발생

##### (1-3) ITIMER_PROF

- 시스템이 프로세스를 위해 실행중인 시간과 프로세스의 가상 시간을 모두 사용
- SIGPROF 시그널 발생

##### (1-4) ITIMER_REALPROF

- 실제 시간 사용
- 멀티스레드 프로그램의 실제 실행시간 측정시 사용
- SIGPROF 시그널 발생

#### (2) 타이머 정보 검색 : getitimer(2)

- 타이머 정보 검색 함수

```c
  #include <sys/time.h>

  int getitimer(int which, struct itimerval *value);
```

- which : 검색할 타이머의 종류
- value : 타이머 정보를 저장할 구조체 포인터

##### (2-1) itimerval/ timeval 구조체

- itimerval 구조체

```c
  struct itimerval{

      struct timeval it_interval;
      struct timeval it_value;
  };
```

- timeval 구조체

```c
  struct timeval {
        time_t tv_sec;
        suseconds_t tv_usec;
  };
```

- it_interval : 타이머 간격 정보 저장
- it_value : 타이머가 만료될때까지 남은 시간 저장
- tv_sec : 초단위 시간 저장

#### (3) 타이머 설정 : setitimer(2)

```c
  #include <sys/time.h>

  int setitimer(int which, const struct itimerval *value,
                                   struct itimerval *ovalue);
```

- which : 설정할 타이머의 종류
- value : 설정할 타이머 정보를 저장한 구조체 포인터
- ovalue : 이전 타이머 정보를 저장할 구조체 포인터

### 3) 기타 시그널 처리 함수

#### (1) 시그널 블록킹과 해제

- 인자로 받은 시그널을 시그널 마스크에 추가하거나 해제

```c
  #include <signal.h>

  int sighold(int sig);
  int sigrelse(int sig);
```

- int sig : 블록하거나 해제할 시그널

#### (2) 시그널 집합 블록과 해제 : sigprocmask(2)

```c
  #include <signal.h>

  int sigprocmask(int how, const sigset_t *restrict set,
                  sigset_t *restrict oset);
```

- how : 시그널을 블록할 것인지, 해제할 것인지 여부
  - SIG_BLOCK : set에 지정한 시그널 집합을 시그널 마스크에 추가
  - SIG_UNBLOCK : set에 지정한 시그널 집합을 시그널 마스크에서 제거
  - SIG_SETMASK : set에 지정한 시그널 집합으로 현재 시그널 마스크 대체
- set : 블록하거나 해제할 시그널 집합 주소
- oset : NULL 또는 이전 설정값을 저장한 시그널 집합 주소

#### (3) 시그널 무시처리 : sigignore(3)

- 인자로 지정한 시그널의 처리방법을 SIG_IGN으로 설정

```c
  #include <signal.h>

  int sigignore(int sig);
```

- sig : 무시할 시그널 번호
