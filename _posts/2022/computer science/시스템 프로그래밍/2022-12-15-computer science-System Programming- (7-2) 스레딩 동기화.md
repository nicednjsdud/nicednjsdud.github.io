---
title: (시스템 프로그래밍) 7-2 스레딩 동기화
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 스레딩 동기화
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-12-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 스레딩 동기화

## 1. 스레딩 동기화

### 1) 필요성

- 하나의 프로세스에서 2개의 스레드가 같이 공유하고 있는 자원(code,data,files)에 동시에 접근하는  
  것을 막아야함
- 하나의 자원에 하나의 스레드가 접근하도록 제어 필요
- 다수의 스레드가 하나의 자원에 순차적으로 접근할 수 있도록 제어 필요

### 2) 임계영역

- 서로 공유하는 자원들을 순차적으로 접근하기 위한 제어 공간
- 다수의 프로세스 및 스레드가 접근 가능하지만 어느 한 순간에서는 프로세스 및 스레드 하나만 사용 가능

### 3) 동기화 기법

#### (1) 상호배제 (MUTEX : MUTual EXclusion)

- pthread_mutex_t 타입의 변수를 뮤텍스라고 표한함
- 한 스레드가 자원을 사용하기 위해 임계영역으로 들어가면 다른 스레드는 임계영역으로 들어가지 못하도록 하는 기법

##### (1-1) 작동 기본 원리

- 임계영역에 들어갈 때 뮤텍스를 잠그고 들어감
- 임계영역에서 빠져 나올 때 뮤텍스를 풀고 나감

##### (1-2) 상호배제의 조건

- 두 프로세스는 동시에 공유 자원에 진입 불가
- 프로세스의 속도나 프로세서 수에 영향 받지 않음
- 공유 자원을 사용하는 프로세스만 다른 프로세스 차단 가능
- 프로세스가 공유 자원을 사용하려고 너무 오래 기다려서는 안됨

##### (1-3) 주의점

- Deadlock (교착 상태)
- mutex의 파괴
- 다른 쓰레드가 lock한 뮤텍스를 unlock하는 상황

#### (2) Lock and unlock(Binary Semaphore)

- 세마포 S를 상호배제에 사용, 1또는 0으로 초기화 P와 V의 연산 교대 실행

### 4) 세마포어

- 프로세스 사이의 **동기**를 맞추는 기능 제공
- 한 번에 한 프로세스만 작업을 수행하는 부분에 접근해 잠그거나, 다시 잠금을 해제하는 기능을 제공하는 정수형 변수

#### (1)

- 에츠허르 데이크스트라 처음 사용
- 테스 명령어의 문제 해결을 위해 제안
- 세마포어 값은 ture나 false로, P와 V연산과 관련
  - 네덜란드어로 P는 검사 Proberen, V는 증가 Verhogen 의미

#### (2)

- 세마포를 의미하는 S는 표준 단위 P(프로세스 대기하는 wait동작, 임계 영역에 진입하는 연산)와  
  V(대기 중인 프로세스를 깨우려고 신호 보내는 signal 동작, 임계 영역에서 나오는 연산)로만  
  접근하는 정수 변수시하고 해체함수는 v로 표현

#### (3) 세마포어 기본 동작 구조

- 중요 처리부분(임계 영역)에 들어가기 전에 p 함수를 실행하여 잠금 수행
- 처리를 마치면 v 함수를 실행하여 잠금 해제

```c
  p(sem);       // 잠금
  중요한 처리 부분
  v(sem);       // 잠금 해제
```

#### (4) p 함수의 기본 동작 구조

```c
  p(sem){
    while sem = 0 do wait;
    sem 값을 1 감소;
  }
```

- sem의 초기값은 1
- sem이 0이면 다른 프로세스가 처리부분을 수행하고 있다는 의미이므로 1일 될 때까지 기다림
- sem이 0이 아니면 0으로 만들어 다른 프로세스가 들어오지 못하게 함

#### (5) v 함수의 기본 동작 구조

```c
  v(sem) {
    sem 값을 1 증가;
    if( 대기중인 프로세스가 있으면 )
      대기중인 첫번째 프로세스를 동작시킨다.
  }
```

### 5) 세마포어 관련 함수

#### (1) 세마포어 생성 : semget(2)

```c
  #include <sys/types.h>
  #include <sys/ipc.h>
  #include <sys/sem.h>
  int semget(key_t key, int nsems, int semflg);
```

- nsems : 생성할 세마포어 개수
- semflg : 세마포어 접근 속성 (IPC_CREAT,IPC_EXCL)

##### (1-1) semid_ds 구조체

![alt](/assets/images/post/ComputerStudy/398.png)

- sem_perm : IPC 공통 구조체
- sem_base : 세마포어 집합에서 첫번째 세마포어의 주소
- sem_nsems : 세마포어 집합에서 세마포어 개수
- sem_otime : 세마포어 연산을 수행한 마지막시간
- sem_ctime : 세마포어 접근권한을 마지막으로 변경한 시간
- sem_binary : 세마포어 종류를 나타내는 플래그

##### (1-2) sem 구조체

- 세마포어 정보를 저장하는 구조체

```c
  struct sem {
    ushort_t    semval;
    pid_t       sempid;
    ushort_t    semncnt;
    ushort_t    semzcnt;
    kcondvar_t  semncnt_cv;
    kcondvar_t  semzcnt_cv;
  }
```

- semval : 세마포어 값
- sempid : 세마포어 연산을 마지막으로 수행한 프로세스 PID
- semncnt : 세마포어 값이 현재 값보다 증가하기를 기다리는 프로세스 수
- semzcnt : 세마포어 값이 0기 되기를 기다리는 프로세스 수

#### (2) 세마포어 제어 : semctl(2)

```c
  #include <sys/types.h>
  #include <sys/ipc.h>
  #include <sys/sem.h>
  int semctl(int semid, int semnum, int cmd, ...);
```

- semnum : 기능을 제어할 세마포어 번호
- cmd : 수행할 제어 명령
- ... : 제어 명령에 따라 필요시 사용할 세마포어

##### (2-1) 공용체 주소 (선택 사항)

```c
  union semun {
    int   val;
    struct semid_df *buf;
    ushort_t *array;
  } arg;
```

- cmd에 지정할 수 있는 값
  - GETPID : 세마포어의 sempid 값을 읽어옴
  - GETNCNT, GETZNCNT : 세마포어의 semncnt, semzcnt 값을 읽어옴
  - GETALL : 세마포어 집합에 있는 모든 세마포의 semval 값을 arg.array에 저장
  - SETALL : 세마포어 집합에 있는 모든 세마포어의 semval 값을 arg.array의 값으로 설정

#### (3) 세마포어 연산 : semop(2)

```c
  #include <sys/types.h>
  #include <sys/ipc.h>
  #include <sys/sem.h>
  int semop(int semid, struct sembuf *sops, size_t nsops);
```

- sedmid : semget() 함수로 생성한 세마포어 식별자
- sops : sembuf 구조체 주소
- nsops : sops가 가리키는 구조체 크기

```c
  struct sembuf {
    ushort_t sem_num;
    short    sem_op;    // 세마포어 연산을 의미
    short    sem_flg;
  };
```

### 6) 뮤텍스 조작 함수

#### (1) Pthread_mutex_init()

- 사용 : 뮤텍스를 초기화
- 성공시 0 실패시 0이 아닌 errno 설정

![alt](/assets/images/post/ComputerStudy/399.png)

```c
  #include <pthread.h>

  int pthread_mutex_init(pthread_mutex_t *restrict mutex,
                        const pthread_mutextattr_t *restrict attr);
```

- mutex : 초기화 할 뮤텍스 객체의 포인터
- attr : 뮤텍스에 지정할 속성, default 는 NULL

#### (2) Pthread_mutex_destroy()

- 사용 : 뮤텍스를 파괴
- 성공 시 0 실패 시 non-zero 리턴,errno 설정

![alt](/assets/images/post/ComputerStudy/400.png)

```c
  #include <pthread.h>

  int pthread_mutex_destory(pthread_mutext_t *mutex);
```

- Mutex : 제거 할 뮤텍스 객체의 포인터

#### (3) Pthread_mutex_lock()

- 사용 : 뮤텍스를 lock 시킴
- 만약 뮤텍스가 lock된 상태라면 unlock 될때까지 block 됨
- 성공시 0 리턴, 실패시 non-zero 리턴,errno 설정

```c
  #include <pthread.h>

  int pthread_mutex_lock(pthread_mutext_t *mutex);
```

- Mutex : lock 시킬 뮤텍스 객체의 포인터

#### (4) Pthread_mutext_trylock

- 사용 : pthread_mutex_lock의 non-blocking 버전
- 성공시 0리턴, 실패시 non-zero리턴, errno 설정

```c
  #include <pthread.h>

  int pthread_mutex_trylock(pthread_mutext_t *mutex);
```

- mutex : trylock 시킬 뮤텍스 객체의 포인터

#### (5) Pthread_mutex_unlock()

- 사용 : lock된 뮤텍스를 unlock 시킴
- 성공시 0 리턴, 실패시 non-zero 리턴,errno 설정

```c
  #include <pthread.h>

  int pthread_mutex_unlock(pthread_mutext_t *mutex);
```

- Mutex : unlock 시킬 뮤텍스 객체의 포인터
