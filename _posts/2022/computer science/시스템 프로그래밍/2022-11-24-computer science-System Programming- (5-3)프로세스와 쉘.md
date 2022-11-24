---
title: (시스템 프로그래밍) 5-3 프로세스와 쉘
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 프로세스와 쉘
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

# 시스템 프로그래밍 - 프로세스와 쉘

## 1. 리눅스 쉘

### 1) 쉘의 역할

- 쉘은 사용자와 운영체제 사이에 창구 역할을 하는 소프트웨어

![alt](/assets/images/post/ComputerStudy/195.png)

#### 명령어 처리기 (command processor)

- 사용자가 입력한 명령을 해석하고 적절한 프로그램을 실행
- 사용자로부터 명령어를 입력받아 이를 처리함

#### (1) 시작 파일

- 로그인할 때 실행되어 사용자별로 맞춤형 사용 환경 설정

#### (2) 스크립트

- 쉘 자체 내의 프로그래밍 기능

![alt](/assets/images/post/ComputerStudy/196.png)

### 2) 유닉스/리눅스에서 사용 가능한 쉘의 종류

![alt](/assets/images/post/ComputerStudy/197.png)

#### (1) 본 쉘(Bourne shell)

- 벨 연구소의 스티븐 본 (Strphen Bourne)에 이해 개발됨
- 유닉스에서 기본 쉘로 사용됨

#### (2) 콘 쉘(Korn shell)

- 1980년대에는 역시 벨연구소에서 본 쉘을 확장해서 만듬

#### (3) Bash(Bourne again shell)

- GNU에서 본 쉘을 확장하여 개발한 쉘
- 리눅스 및 맥 OS X에서 기본 쉘로 사용되면서 널리 보급됨
- Bash 명령어의 구문은 본 쉘 명령어 구문을 확장함

#### (4) C쉘(C shell)

- 버클리대학의 빌 조이(Bill Joy)
- 쉘의 핵심 기능 위에 C언어의 특징을 많이 포함함
- BSD 계열의 유닉스에서 많이 사용됨
- 최근에 이를 개선한 tcsh이 개발되어 사용됨

### 3) 쉘의 실행 절차

![alt](/assets/images/post/ComputerStudy/198.png)

## 2. 리눅스 프로세스 처리 함수

### 1) 프로세스 실행 시간 측정

#### (1) 프로세스 실행 시간의 구성

- 프로세스 실행시간 = 시스템 실행시간 + 사용자 실행시간
- 시스템 실행시간 : 커널 코드를 수행한 시간 (시스템 호출로 소비한 시간)
- 사용자 실행시간 : 사용자 모드에서 프로세스를 실행한 시간

#### (2) 프로세스 실행 시간 측정

- 사용자 실행시간과 시스템 실행시간으로 나누어 tms 구조체에 저장
- 시간단위는 클록틱(sysconf 함수에서 `_SC_CLK_TCK`로 검색한 값)

```c
  #include <sys/times.h>
  #include <limits.h>

  clock_t times(struct tms *buffer);
```

- buffer : 실행 시간을 저장할 tms 구조체의 주소

##### (2-1) tms 구조체

```c
  struct tms {
    clock_t tms_utime;  // 사용자 모드 실행 시간
    clock_t tms_stime;  // 시스템 모드 실행 시간
    clock_t tms_cutime; // 자식 프로세스 사용자 모드 실행 시간
    clock_t tms_cstime; // 자식 프로세스의 시스템 모드 실행 시간
  }
```

### 2) 환경 변수의 이해

- 프로세스가 실행되는 기본 환경을 설정하는 변수
- 로그인명, 로그인 쉘, 터미널에 설정된 언어, 경로명 등
- 환경변수는 "환경변수=값"의 형태로 구성되며 관례적으로 대문자로 사용
- 현재 쉘의 환경 설정을 보려면 env 명령을 사용

![alt](/assets/images/post/ComputerStudy/199.png)

### 3) 환경변수의 사용

#### (1) 전역변수 사용 : environ

```c
  #include <stdlib.h>

  extern char **environ;
```

#### (2) 환경변수의 사용 : main 함수 인자 사용

```c
  int main(int argc, char **argv, char **envp){...}
```

#### (3) 환경변수의 검색 : getenv(3)

```c
  #include <stdlib.h>

  char *getenv(const char *name);
```

- name : 환경 변수명

#### (4) 환경변수 설정 : putenv(3)

```c
  #include <stdlib.h>

  int putenv(char *string);
```

- string : 설정할 환경 변수와 값으로 구성한 문자열

#### (5) 환경변수 설정 : setenv(3)

```c
  #include <stdlib.h>

  int setenv(const char *envname, const char *envval, int overwrite)
```

- envname : 환경변수명 지정
- envval : 환경변수 값 지정
- overwrite : 덮어쓰기 여부 지정, 0이 아니면 덮어쓰고, 0이면 덮어쓰지 않음

#### (6) 환경변수 설정 삭제 : unsetenv(3)

```c
  #include <stdlib.h>

  int unsetnev(const char *name);
```

- name : 환경 변수명
