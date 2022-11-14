---
title: (시스템 프로그래밍) 3-2 파일 접근
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 파일 접근
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-14 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 파일 접근

## 1. 파일 사용 권한

### 1) 소유권

- 리눅스는 다중 사용자 지원 운영체제이다.
- 파일 접근 권한 보호

### 2) 파일 속성

```c
  user1@myubuntu:~$ -l /etc/hosts
  -rw-r--r-- 1 root root 223 11월 14 14:12 /etc/hosts
  user1@myubuntu:~$
```

- 총 10자리의 자리에 파일 종류, 소유자, 소유그룹, 사용자 권한을 표시

#### (1) st_mode 값의 구조

- 특수접근 권한이 추가됨.

![alt](/assets/images/post/ComputerStudy/25.png)

#### (2) 파일 종류

![alt](/assets/images/post/ComputerStudy/26.png)

#### (3) 특수접근 권한

![alt](/assets/images/post/ComputerStudy/27.png)

### 3) 파일 정보 검색

```c
  i-node 정보 검색 : stat(), lstat(), fstat() 함수 사용
```

#### (1) 파일명으로 파일 정보 검색 ㅣ stat(2)

- inode에 저장된 파일 정보 검색
- path에 검색할 파일의 경로를 지정하고, 검색한 정보를 buf에 저장

```c
#include <sys/types.h>
#include <sys/stat.h>
int fstat(int fd, struct stat *buf);
```

- path : 정보를 알고자 하는 파일명
- buf : 검색한 파일 정보를 저장할 구조체 주소

#### (2) stat 구조체

![alt](/assets/images/post/ComputerStudy/28.png)

#### (3) 파일명으로 i-node 정보 검색

```c
  #include <sys/types.h>
  #include <sys/stat.h>
  #include <stdio.h>

  int main(void){
    struct stat buf;

    stat("unix.txt", &buf);
    ...
  }
```

#### (4) 파일 기술자로부터 파일 정보 검색 : fstat(2)

- fd로 지정한 파일의 정보를 검색하여 buf에 저장

```c
  #include <sys/types.h>
  #include <sys/stat.h>
  int fstat(int fd,struct stat *buf)
```

- fd : 열려 있는 파일의 파일 기술자
- buf : 검색한 파일 정보를 저장할 구조체 주소

### 4) 파일 종류 검색

#### (1) 상수 이용한 파일 종류 검색

- 파일 종류 검색시 상수와 매크로 이용

![alt](/assets/images/post/ComputerStudy/29.png)

#### (2) 매크로 이용 파일 종류 검색

- 각 매크로는 인자로 받은 mode 값을 0xF000과 AND 연산 수행
- AND 연산의 결과를 파일의 종류별로 정해진 값과 비교하여 파일의 종류 판단
- 이 매크로는 POSIX 표준

![alt](/assets/images/post/ComputerStudy/30.png)

### 5) 파일 접근 권한 검색

#### (1) 상수 이용

- 소유자의 접근권한 추출과 관련된 상수만 정의

##### 소유자 외 그룹과 기타사용자의 접근권한은?

- st_mode의 값을 왼쪽으로 3비트 이동시키거나 상수값을 오른쪽으로 3비트  
  이동시켜 AND 수행
- st_mode & (S_IREAD >> 3)

![alt](/assets/images/post/ComputerStudy/31.png)

### 6) 함수 사용 파일 접근 권한 검색 : access(2)

- path에 지정된 파일이 amode로 지정한 권한을 가졌는지 확인하고 리턴
- 접근권한이 있으면 0을, 오류가 있으면 -1을 리턴

#### (1) 오류메세지

- ENOENT : 파일이 없음
- EACCESS : 접근권한이 없음

#### (2) amode 값

- R_OK : 읽기 권한 확인
- W_OK : 쓰기 권한 확인
- X_OK : 실행 권한 확인
- F_OK : 파일이 존재하는지 확인

#### (3)

```c
  #include <sys/erron.h>
  #include <unistd.h>
  #include <stdio.h>

  extern int errno;

  int main(void){
    int per;

    if (access("unix.bak",F_OK) == -1 && errno == ENOENT)
      printf("unix.bak: File not exist. \n");
  }
```

### 7) 접근 권한 변경

#### (1) 파일명으로 접근 권한 변경 : chmod(2)

- path에 지정한 파일의 접근권한을 mode값에 따라 변경
- 접근 권한을 더할 때는 OR 연산자를, 뺄 때는 NOT 연산 후 AND 연산자를 사용

```c
  - chmod(path, S_ORWXU);
  - chmod(path, S_IRWXU|S_IREGRP|S_IXGRP|S_IROTH);
  - mode |= S_IWGRP;
  - mode &= ~(S_IROTH);
```

#### (2) 파일 기술자로 접근 권한 변경 : fchmod(2)

```c
  #include <sys/types.h>
  #include <sys/stat.h>
  int fecmod(int fd, mode_t mode);
```

- fd : 열려 있는 파일의 파일 기술자
- mode : 접근 권한

## 2. 심볼릭 링크 및 하드 링크 파일

### 1) 링크

- 이미 있는 파일이나 디렉터리에 접근할 수 있는 새로운 이름
- 같은 파일/ 디렉터리지만 여러 이름으로 접근할 수 잇게 함.

#### (1) 하드링크

- 기존 파일과 동일한 i-node 사용
- i-node에 저장된 링크 개수 증가

#### (2) 심볼릭 링크

- 기존 파일에 접근하는 다른 파일 생성 (다른 i-node 사용)

### 2) 하드 링크의 특성

- 파일에 접근할 수 있는 파일명을 새로 생성
- **기존 파일과 동일한 i-node 사용**
- i-node에 저장된 링크 개수 증가

#### (1) 하드링크 생성 : link(2)

- 두경로는 같은 파일시스템에 존재해야 함.

```c
  #include <unistd.h>
  int link (const char *existing, const char *new);
```

- existing : 기존 파일의 경로
- new : 새로 생성할 링크의 경로

### 3) 심볼릭 링크 : symlink(2)

- 성공 시 0 리턴, 실패하면 -1 리턴

```c
  #include <unistd.h>
  int symlink(const char *name1, const char *name2);
```

- name1 : 기존 파일의 경로
- name2 : 새로 생성할 링크의 경로

#### (1) 심볼릭 링크 정보 검색 : lstat(2)

- 심볼릭 링크 자체의 파일 정보 검색
- stat() 검색시 원본파일 검색

#### (2) 심볼릭 링크 내용 읽기 : readlink(2)

- 심볼릭 링크의 데이터 블록에 저장된 내용 읽기

```c
  #include <unistd.h>
  ssize_t readlink(const char *restrict path, char *restrict buf,
                  size_t bufsiz);
```

- path : 심볼릭 링크의 경로
- buf : 읽어온 내용을 저장할 버퍼
- bufsiz : 버퍼의 크기

## 3. 다중 사용자 운영체제

### 1) 단일 사용자 운영체제 - 개인용

- DOS
- windows
- MAC

### 2) 다중 사용자 운영체제 - 서버용

- UNIX
- Linux, Windows NT

### 3) 모바일용 운영체제

- 안드로이드
- IOS
- 블랙베리
