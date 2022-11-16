---
title: (시스템 프로그래밍) 4-2 사용자 관리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 사용자 관리
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

# 시스템 프로그래밍 - 사용자 관리

## 1. 사용자 정보 개요

### 1) 개요

- 리눅스는 다중 사용자 시스템이므로 사용자를 구별하고 사용자에게 적절한 자원을 할당해주는  
  방법이 필요
- 사용자 계정은 사용자가 시스템에 접근할 수 있는 유일한 방법
- 시스템 관리자의 입장에서도 사용자의 접근 권한을 통제할 수 있는 중요한 수단

### 2) 사용자 계정 관련 파일

#### (1) /etc/passwd 파일

- 사용자 계정 정보가 저장된 기본 파일
- 한 행에 사용자 한명에 대한 정보가 기록되며, 쌍점(:)으로 구분되는 일곱 개의 항목으로 구성

![alt](/assets/images/post/ComputerStudy/69.png)

##### (a) 로그인 ID

- 사용자 계정의 이름, 32자를 넘을 수 없으나 8자로 제한하는 것이 좋음

##### (b) x

- 초기 유닉스 시스템에서 사용자 암호를 저장하던 항목, 요즘은 `/etc/shadow`파일에 별도로 보관

##### (c) UID

- 사용자 ID 번호로 시스템이 사용자를 구별하기 위해 사용하는 번호
- 0~999번과 65534번은 시스템 사용자를 위한 UID로 예약(0:root, 1:daemon, 2:bin, 7:ip 등)
- 일반 사용자들은 UID 1000번부터 할당
- 로그인 ID가 다르더라도 UID가 같으면 리눅스 시스템은 같은 사용자로 판단, 따라서 UID가  
  중복되지 않았는지 주의해야 함.

##### (d) GID

- 그룹ID, 시스템에 등록된 그룹에 대한 정보는 `/etc/group`파일에 저장

##### (e) 설명

- 사용자의 일반적인 정보를 나타내는 공간

##### (f) 홈 디렉터리

- 사용자 계정에 할당된 홈 디렉터리의 절대 경로를 기록

##### (g) 로그인 셸

- 사용자의 로그인 셸을 지정 우분투에서는 배시 셸`/bin/bash`을 기본 셸로 사용

#### (2) /etc/shadow 파일

- 사용자 암호에 관한 정보를 별도로 관리하는 파일
- root 계정으로만 내용을 볼 수 있음.

#### (3) /etc/group 파일

- 그룹에 대한 정보가 저장
- `/etc/passwd`파일의 GID 항목에 지정된 그룹이 기본 그룹이며, 사용자가 속한 2차 그룹은  
  `/etc/group`파일에 지정

#### (4) /etc/gshadow 파일

- 그룹 암호가 저장
- 리눅스에서만 사용하는 파일 (유닉스에는 없음)

### 3) 사용자 계정 관리 명령 : useradd

- 사용자 계정 생성
- useradd `[옵션]` `[login ID]`

#### (1) 옵션

```c
  -u uid : UID 지정
  -o     : UID 중복 허용
  -g gid : 기본 그룹의 GID 지정
  -G gid : 2차 그룹의 GID 지정
  -d 디렉터리명 : 홈디렉터리 지정
  -s 쉘 : 기본 쉘 지정
```

## 2. 사용자 정보 검색 함수

### 1) 로그인 명 검색 : getlogin(3),cuserid(3)

#### (1) getlogin()

- 현재 프로세스를 실행한 사용자의 로그인명을 리턴
- 성공 시 로그인명, 실패시 NULL 리턴

```c
    #include <unistd.h>

    char *getlogin(void);
```

#### (2) cuserid()

- 현재 프로세스의 소유자 정보로 로그인명을 찾아 리턴
- 성공 시 로그인명, 실패시 NULL 리턴

```c
  #include <stdio.h>

  char *cuserid(char *s);
```

- s : 검색한 로그인명을 저장할 주소

### 2) UID 검색 : getuid(2), geteuid

```c
  #include <sys/types.h>
  #include <unistd.h>

  uid_t getuid(void);
  uid_t geteuid(void);
```

#### (1) getuid(2)

- 현재 프로세스의 실제 사용자 ID

#### (2) geteuid(2)

- 유효 사용자 ID

### 3) 패스워드 파일 검색

#### (1) UID로 passwd 파일 읽기 : getpwuid(3)

```c
  #include <pwd.h>

  struct passwd *getpwuid(uid_t uid);
```

- uid : 검색할 UID

#### (2) 이름으로 passwd 파일 읽기 : getpwnam(3)

```c
  #include <pwd.h>

  struct passwd *getpwnam(const char *name);
```

- name : 로그인명

#### (3) /etc/passwd 파일 순차적으로 읽기

- getpwent() : 사용자 정보를 순차적으로 읽음
  - 파일끝에서 NULL 리턴
- setpwent() : 파일의 오프셋을 파이르이 처음으로 이동
- endpwent() : 파일을 닫음
- fgetpwent() : 파일 포인터 인자로 받음

```c
  #include <pwd.h>

  struct passwd *getpwent(void);
  void setpwent(void);
  void endpwent(void);
  struct passwd *fgetpwent(FILE *fp);
```

- fp : 파일 포인터

### 4) 섀도우 파일 검색

#### (1) /etc/shadow 파일 읽기 : getspnam(3)

```c
  #include <shadow.h>

  struct spwd *getspnam(const char *name);
```

#### (2) /etc/shadow 파일 순차적으로 읽기

```c
  #include <shadow.h>

  struct spwd *getspent(void);
  void setspent(void);
  void endspent(void);
  struct spwd *fgetspent(FILE *fp);
```

### 5) 그룹 정보 검색

#### (1) 그룹 ID 검색하기 : getgid(2), getegid(2)

```c
  #include <sys/types.h>
  #include <unistd.h>

  gid_t getgid(void);
  gid_t getegid(void);
```

### 6) 그룹 파일 검색

#### (1) /etc/group 파일 검색 : getgrnam(3), getgrgid(3)

```c
  #include <grp.h>

  struct group *getgrnam(const char *name);
  struct group *getgrgid(gid_t gid);
```

- name : 검색하려는 그룹명
- gid : 검색하려는 그룹의 ID

#### (2) /etc/group 파일 순차적으로 읽기

```c
  #include <grp.h>

  struct group *getgrent(void);
  void setgrent(void);
  void endgrent(void);
  struct group *fgetgrent(FILE *fp);
```

- fp : 파일 포인터

### 7) 로그인 기록 검색

#### (1) who 명령

- 현재 시스템에 로그인하고 있는 사용자 정보

#### (2) last 명령

- 시스템의 부팅 시간 정보와 사용자 로그인 기록 정보

#### (3) /var/adm/utmpx 파일 순차적으로 읽기

```c
  #include <utmpx.h>

  struct utmpx *getutxent(void);
  void setutxent(void);
  void endtxent(void);
  int utmpxname(const char *file);
```

- file : 교체할 파일명
