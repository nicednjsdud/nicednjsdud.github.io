---
title: (시스템 프로그래밍) 6-2 프로세스 종료
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로세스 종료
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

# 시스템 프로그래밍 - 프로세스 종료

## 1. 리눅스 프로세스 종료

### 1) 프로그램 종료 함수의 일반적 종료 절차

- 모든 파일 기술자를 닫음
- 부모 프로세스에 종료 상태를 알림
- 자식 프로세스들에 SIGHUP 시그널을 보냄
- 부모 프로세스에 SIGCHLD 시그널을 보냄
- 프로세스간 통신에 사용한 자원을 반납함

### 2) 프로세스 종료 특징

1. 프로세스가 마지막 명령 실행, 종료하여 운영체제에 프로세스의 삭제 요청
2. abort 명령어로 프로세스 종료
3. 부모 프로세스의 자식 프로세스 종료
4. exit 명령어 : 유닉스에서 프로세스 종료
5. wait 명령어 : 부모 프로세스가 자식 프로세스의 종료 기다림
6. 프로세스 종료 이유

#### (3-1)

- 보통 부모 프로세스 종료하면 운영체제가 자식 프로세스도 종료(연속 종료)
- 자식 프로세스가 할당된 자원을 초과하여 자원을 사용할 때
- 자식 프로세스에 할당한 작업이 더는 없을 때

#### (6-1)

- 정상 종료 : 프로세스가 운영체제의 서비스 호출
- 시간 초과
- 실패 : 파일 검색 실패, 입출력이 명시된 횟수 초과하여 실패할 때
- 산술 오류, 보호 오류, 데이터 오류 등, 메모리 부족, 액세스 위반 등

## 2. 리눅스 프로세스 종료 함수

### 1) 프로그램 종료 함수

```c
  프로세스 종료 : void exit(int status);
              void _exit(int status);
  종료시 수행할 작업 지정 : int atexit(void (*func)(void));
```

#### (1) 프로그램 종료 : exit(2)

```c
  #include <stdlib.h>
  void exit(int status);
```

- status : 종료 상태 값

#### (2) 프로그램 종료시 수행할 작업 예약 : atexit(2)

```c
  #include <stdlib.h>
  int atexit(void (*func)(void));
```

- func : 종료시 수행할 작업을 지정한 함수명

#### (3) 프로그램 종료 : `_exit(2)`

```c
  #include <unistd.h>
  void _exit(int status);
```

- 일반적으로 프로그램에서 직접 사용하지 않고 exit 함수 내부적으로 호출
