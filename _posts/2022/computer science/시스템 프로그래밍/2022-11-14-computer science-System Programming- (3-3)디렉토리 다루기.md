---
title: (시스템 프로그래밍) 3-3 디렉토리 다루기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 디렉토리 다루기
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

# 시스템 프로그래밍 - 디렉토리 다루기

## 1. 리눅스 디렉토리

### 1) 디렉터리

- 파일의 목록을 저장하기 위한 특수한 형태의 파일

#### (1) 디렉터리 데이터 블록

- 자기 자신의 항
- 부모 디렉터리 가르키는 항
- 자신에게 포함된 파일 목록
- 아이노드 블록의 번호

#### (2) 계층 구조 - 트리 구조

![alt](/assets/images/post/ComputerStudy/32.png)

### 2) 경로

- 파일의 위치

#### (1) 절대 경로

- 루트 디렉터리를 기준으로 파일의 위치 표현
- 현재 디렉터리 : .
- 부모 디렉터리 : ..
- 디렉터리 구분 : /(윈도우 운영체제는 ₩ 혹은 `\`)

## 2. 리눅스 디렉터리 관련 함수

### 1) 디렉터리 생성과 삭제

#### (1) 디렉터리 생성 : mkdir(2)

- path에 지정한 디렉터리를 mode 권환에 따라 생성

```c
  #include <sys/types.h>
  #include <sys/stat.h>
  int mkdir(const char *path, mode_t mode);
```

- path : 디렉터리가 포함된 경로
- mode : 접근 권한

#### (2) 디렉터리 삭제 : rmdir(2)

- 성공 시 0, 실패하면 -1를 리턴

```c
  #include <unistd.h>
  int rmdir(const char *path);
```

- path : 삭제할 경로

### 2) 디렉터리 관리

#### (1) 디렉터리 이름 변경 : rename(2)

```c
  #include <stdio.h>
  int rename(const char *old, const char *new);
```

- old : 변경할 파일/ 디렉터리 명
- new : 새 파일/ 디렉터리 명

#### (2) 현재 작업 디렉터리 위치 : getcwd(3)

- 디렉터리 작업 위치 알아낼 때 사용
- 현재 작업 위치 명령 : pwd

##### 실패시 : NULL 리턴

- 버퍼 주소가 NULL 이면 getcwd()는 직업 mallco으로 메모리 할당하고 주소 리턴

#### (3) 디렉터리 이동 : chdir(2)

- 프로그램에서 디렉터리 이동시 사용
- 리눅스 명령어 : cd

```c
  #include <unistd.h>
  int chdir(const char *path);
```

- path : 이동하려는 디렉터리 경로

### 3) 디렉터리 정보 검색

#### (1) 디렉터리 열기 : opendir(3)

- 지정한 디렉터리를 읽기 전용으로 연다.
- 성공 시 dir 포인터 리턴, 실패시 NULL 리턴

```c
  #include <sys/types.h>
  #include <dirent.h>
  DIR *opendir(const char *dirname);
```

- dirname : 열려는 디렉터리 명

#### (2) 디렉터리 닫기 : closedir(3)

- 지정한 DIR 포인터가 가르키는 디렉터리 닫음
- 성공 시 0, 실패 시 -1리턴

```c
  #include <sys/types.h>
  #include <direct.h>
  int clodedir(DIR *dirp);
```

- dirp : 닫으려는 디렉터리를 가르키는 포인터

#### (3) 디렉터리 정보 읽기 : readdir(3)

- 지정한 DIR 포인터가 가르키는 디렉터리 내용을 한번에 하나씩 읽음
- 성공 시 디렉터리 내용을 하나씩 읽음, 실패시 NULL을 리턴

```c
  #include <sys/types.h>
  #include <dirent.h>
  struct dirent *readdir(DIR *dirp);
```

- dirp : 정보를 읽어올 디렉터리를 가르키는 포인터
- dirent.h 구조체는 sys/dirent.h에 정의

#### (4) 디렉터리 오프셋 : telldir(3), seekdir(3), rewinddir(3)

- 파일 오프셋 / 디렉터리 오프셋
- 디렉터리 열고, 정보 읽을시 이동
- telldir : 디렉터리 오프셋의 현재 위치를 알려줌
- Seekdir : 디렉터리 오프셋을 loc에 지정한 위치로 이동시킴
- rewinddir : 디렉터리 오프셋을 디렉토리의 시작인 0으로 이동시킴

## 3. 윈도우에서 리눅스의 디렉터리 개념과 같은 개념

- 디렉터리 : 파일의 목록을 저장하기 위한 특수한 형태의 파일
- 디렉터리 데이터 블록 - 트리구조 : 절대 경로와 상대경로로 구분 윈도우에서는 폴더와 같은 개념
