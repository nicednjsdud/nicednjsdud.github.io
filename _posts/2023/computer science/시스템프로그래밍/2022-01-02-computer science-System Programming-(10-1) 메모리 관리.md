---
title: (시스템 프로그래밍) 10-1 메모리 관리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 메모리 관리
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-02 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 메모리 관리

## 1. 메모리 관리

### 1) 프로세스간 통신 (IPC : Inter Process Communication)

- 동일한 유닉스/리눅스 시스템에서 수행 중인 프로세스끼리 데이터를 주고받는 것
- **파이프(pipe) 특수 파일 이용**
- 메모리 매핑이나 공유 메모리 영역을 이용
- **유닉스 V : 메세지 큐, 공유 메모리, 세마포어 등**

#### (1) 넓은 의미

- 종료 상태와 시그널 같은 정수값을 주고 받는 것
- 시그널 : 미리 정의된 상수를 프로세스간에 주고받는 것

#### (2) 리눅스에서 IPC

##### (2-1) 이름 없는 익명의 파이프

- 간단한 파이프 생성

```c
  FILE *popen(const char *command, const char *mode);
  int pclose(FILE *stream)
```

- 복잡한 파이프 생성

```c
  int pipe(int fildes[2])
```

##### (2-2) 이름 있는 익명의 파이프

- FIFO 생성 명령

```c
  mknod name p
  mkfifo [-m mode] path...
```

- FIFO 생성 함수

```c
  int mknod(const char *path, mode_t mode, dev_t dev);
  int mkfifo(const char *path, mode_t mode);
```

### 2) 네트워크를 이용한 통신

- TCP/IP 프로토콜을 기본으로 소켓 라이브러리 이용
- TLI (Transport Layer Interface)

## 2. 메모리 관리 함수

### 1) 메모리 매핑 관련 함수

- **메모리 매핑**

```c
  void *mmap(void *addr,size_t len,int prot,int flags,int fildes,off_t off);
```

- 메모리 매핑 해제

```c
  int munmap(void *addr,size_t len);
```

- 파일 크기 조정

```c
  int truncate(const char *path, off_t length);
  int ftruncate(int fildes, off_t length);
```

- 매핑된 메모리 동기화

```c
  int msync(void *addr,size_t len,int flag);
```

### 2) 메모리 매핑 : mmap

- fildes가 가리키는 파일에서 off로 지정한 오프셋부터 len 크기만큼 데이터를 읽어 addr이 가리키는 메모리  
  공간에 매핑
- 성공 : 매핑된 메모리 시작 주소 리턴
- 실패 : 상수 MAP_FAILED 리턴

### 3) 메모리 매핑 해제 함수 : munmap

- addr이 가리키는 영역에 len크기 만큼 할당해 매핑한 메모리 해제
- 해제한 메모리에 접근하면 SIGSEGV 또는 SIGBUS 시그널 발생
