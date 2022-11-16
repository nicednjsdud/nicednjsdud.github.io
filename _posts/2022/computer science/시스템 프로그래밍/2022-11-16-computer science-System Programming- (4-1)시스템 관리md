---
title: (시스템 프로그래밍) 4-1 시스템 관리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 시스템 관리
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-16 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 시스템관리

## 1. 리눅스 시스템

### 1) 개요

- 시스템 정보 검색 및 설정 함수 (하드웨어)

#### (1) 시스템 환경

- 운영체제 종류 관련 정보
- 메모리 페이지의 크기
- 최대 패스워드 길이 등

#### (2) 시스템 정보 검색 및 설정 함수

![alt](/assets/images/post/ComputerStudy/65.png)

### 2) 사용자 정보 관련 함수

#### (1) 로그인명 검색

```c
  char *getlogin(void);
  char *cuserid(cahr *s);
```

#### (2) UID 검색

```c
  uid_t getuid(void);
  uid_t geteuid(void);
```

#### (3) 패스워드 검색

```c
  struct passwd *getpwuid(uid_t uid);
  struct paaswd *getpwname(const char *name);
```

#### (4) 패스워드 파일 검색

```c
  struct passwd *getpwent(void);
  void setpwent(void);
  void endpwent(void);
  struct passwd *fgetpwent(FILE *fp);
```

#### (5) 새도우 정보 검색

- 처음부터 암호화 처리되서 만들어진 것

```c
  struct spwe *getspname(const char *name);
```

#### (6) 새도우 파일 검색

```c
  struct spwd *getspent(void);
  void setspent(void);
  void endspent(void);
  struct spwd *fgetpent(FILE *fp);
```

#### (7) 그룹 정보 검색

```c
  gid_t getgid(void);
  gid_t getegid(void);
```

#### (8) 그룹 파일 검색

```c
  struct group *getrname(const char *name);
  struct group *getgrgid(gid_t gid);
  struct group *getgrent(void);
  void setgrent(void);
  void endgrent(void);
  struct group *fgetgrent(FILE *fp);
```

#### (9) 로그인 기록 검색

```c
  struct utmpx *gettutxent(void);
  void setutxent(void);
  void endutxent(void);
  int utmpxname(const char *file);
```

### 3) 시간 정보 검색 함수

![alt](/assets/images/post/ComputerStudy/66.png)

#### (1) 현재 시간 정보 검색

```c
  time_t time(time_t *tloc);
  int gettimeofday(struct timeval *fp, void *tzp);
```

#### (2) 시간대 설정

```c
  void tzset(void);
```

#### (3) 시간 정보 분해

```c
  struct tm *localtime(const time_t *dock);
  struct tm *gmtime(const time_t *dock);
```

#### (4) 초 단위 시간 생성

```c
  time_t mktime(struct tmm *timeptr);
```

#### (5) 형식 지정 시간 출력

```c
  char *ctime(const time_t *dock);
  char *asctime(const struct tm *tm);
  size_t strftime(char *restrct s,size_t maxsize, const char *r,
                  estrit formant, const struct tm *restrict timeptr);
```

## 2. 리눅스 시스템 자원

### 1) 운영체제 기본 정보 검색

- 시스템에 설치된 운영체제에 대한 기본 정보 검색

![alt](/assets/images/post/ComputerStudy/67.png)

- 시스템은 인텔PC고 솔라시스 10 운영체제가 설치되어 있고, 호스트명은 hanbit

#### (1) 운영체제 정보 검색 함수 : uname(2)

```c
  #include <sys/utsname.h>

  int uname(struct utsname *name);
```

- name : utsname 구조체 주소

##### utsname 구조체 - sys/utsname.h

```c
  struct utsname{
    char sysname[_SYS_NMLN];
    char nodename[_SYS_NMLN];
    char release[_SYS_NMLN];
    char version[_SYS_NMLN];
    char machine[_SYS_NMLN];
  }
```

- utsname 구조체에 운영체제 정보 저장
- sysname : 현재 운영체제 이름
- nodename : 호스트명
- release : 운영체제의 릴리즈 번호
- version : 운영체제 버전 번호
- machine : 하드웨어 아키텍처 이름

#### (2) 시스템 정보 검색과 설정 : sysinfo(2)

- command에 검색하거나 설정할 명령 지정
- 성공 시 결과값, 실패 시 -1리턴

```c
  #include<sys/systeminfo.h>

  long sysinfo(int command, char *buf, long count);
```

- command : 검색 또는 설정할 명령
- buf : 버퍼 주소
- count : 버퍼 길이, 최댓값 257

##### command에 사용할 상주의 범주

![alt](/assets/images/post/ComputerStudy/68.png)

#### (3) 시스템 자원 정보 검색

- 하드웨어에 따라 사용할 수 있는 자원들의 최댓값 검색
- sysconf(), fpathconf(), pathconf()

##### (3-1) sysconf(3)

- 검색할 정보를 나타내는 상수를 사용해야 함
- sys/unistd.h 파일에 정의
- 성공 시 시스템 자원값 또는 옵션값, 실패시 -1 리턴

```c
  #include <unistd.h>

  long sysconf(int name);
```

- name : 검색할 정보를 나타내는 상수

##### (3-2) 파일과 디렉토리 관련 정보 검색 :fpathconf(3), pathconf(3)

- 성공 시 경로(path)나 파일 기술자에 지정된 파일에 설정된 자원값이나 옵션값을 정수로 리턴,  
  실패시 -1 리턴

```c
  #include <unistd.h>

  long pathconf(const char *path, int name);
  long fpathconf(int fildes, int name);
```

- path : 파일이나 디렉토리 경로
- name : 검색할 정보를 지정하는 상수
- fildes : 파일 기술자
