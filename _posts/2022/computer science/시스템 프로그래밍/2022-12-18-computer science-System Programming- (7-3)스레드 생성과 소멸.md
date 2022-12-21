---
title: (시스템 프로그래밍) 7-3 스레드 생성/소멸
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 스레드 생성/소멸
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-12-18 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 스레드 생성/소멸

## 1. 리눅스 스레드 구현

### 1) 스레드 생성

#### (1) 특징

- 스레드의 집합과 자원의 집합
- 수행 유닛은 스레드임
- 프로세스는 스레드의 수행 환경을 제공
- Thread ID를 가지고 있음

### 2) 프로세스와 스레드 함수 비교

![alt](/assets/images/post/ComputerStudy/401.png)

## 2. Pthread 생성 및 종료

### 1) Pthread_self() 함수

- 자신의 스레드 ID를 얻음
- 성공 : 호출한 스레드의 스레드ID를 리턴
- 실패 : 정의 되어 있지 않음

```c
  #include <pthread.h>

  Pthread_t pthread_self(void);
```

### 2) Pthread_create() 함수

- 스레드를 생성함
- 성공 : 0을 리턴
- 실패 : 0이 아닌 에러코드 리턴 (EAGAIN, EINVAL, EPERM)

```c
  #include <pthread.h>

  int pthread_create(pthread_t *restrict thread,const pthread_attr_t *restrict attr,
          void *(*start_routine)(void*), void *restrict arg);
```

- thread : 스레드 ID를 가리키는 포인트
- attr : 스레드와 관련된 특성을 지정하기 위한 용도로 사용
- 마지막 두개의 인자는 실행을 시작할 함수와 이 함수에 전달할 인자를 스레에게 알려줌

### 3) Pthread_exit() 함수

- 프로세스를 종료시키지 않고, 호출한 스레드만 종료
- 성공 : 0을 리턴
- 실패 : 에러 정의되어 있지 않음

```c
  #include <pthread.h>

  void pthread_exit(void *value_ptr);
```

- value_ptr : 스레드가 참조하는 데이터를 가리키는 포인터
  - pthread_join 함수 호출이 성공했을 때 사용

### 4) Pthread_join() 함수 (=waitpid)

- 명시된 스레드가 종료할 때까지 호출한 스레드를 대기시킴
- 성공 : 0을 리턴
- 실패 : 0이 아닌 에러코드 리턴

```c
  #include <pthread.h>

  void pthread_join(pthread_t thread,void **value_ptr);
```

- thread : 종료를 기다리는 스레드
  - thread가 종료되어야 현재 스레드는 join에서 벗어남
- value_ptr : 타겟 스레드의 리턴 상태를 가리키는 포인터를 저장하기 위한 위치
  - 리턴 상태는 타겟 스레드가 pthread_exit 함수나 return 문으로 넘겨준 값

### 5) Pthread_cancel() 함수

- 다른 스레드를 제거
- 성공 : 0 리턴
- 실패 : 0이 아닌 에러코드 리턴

```c
  #include <pthread.h>

  int pthread_cancel(pthread_t thread);
```

- thread : 취소하고자 하는 스레드 ID

### 6) Pthread_cleanup_push() 함수

- 스레드 cleanup handlers 를 스택 메모리에 push 함
- 성공 : 0을 리턴
- 실패 : 0이 아닌 에러코드 리턴

```c
  #include <pthread.h>

  int pthread_cleanup_push(void(*routine(void*),void *arg));
```

- arg : 스레드 핸들러 루틴 argument

### 7) Pthread_cleanup_pop() 함수

- 스택에 push된 cleanup handler를 제거함

```c
  #include <pthread.h>

  int pthread_cleanup_pop(int execute);
```

- execute : 0 또는 0이 아닌 값
