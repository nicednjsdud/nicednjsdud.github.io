---
title: (시스템 프로그래밍) 10-2 메모리 매핑
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 메모리 매핑
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

# 시스템 프로그래밍 - 메모리 매핑

## 1. 메모리 매핑

### 1) 메모리 매핑의 개념

- 파일을 프로세스의 메모리에 매핑
- 프로세스에 전달할 데이터를 저장한 파일을 직접 프로세스의 가상 주소 공간으로 매핑
- **read,write 함수를 사용하지 않고도 프로그램 내부에서 정의한 변수를 사용해 파일에서 데이터를 읽거나 쓸 수있음**

### 2) 메모리 매핑과 기존 방식의 비교

#### (1) 기존방식

- 파일을 읽고 필요에 따라 파일의 오프셋을 이동시키고 read() 함수 호출해 데이터를 buf로 읽어와서 작업

```c
  fd = open(...)
  lseek(fd, offset, whencd);
  read(fd, buf, len);
```

#### (2) 메모리 매핑 함수 사용

- 파일을 열고 열린 파일의 내용을 mmap() 함수를 사용해 메모리에 매핑하고, 이후의 address가 가리키는  
  메모리 영역의 데이터를 대상으로 수행
- **매번 read() 함수로 데이터를 읽어올 필요가 없음 (수행속도 ^)**

```c
  #include <sys/mman.h>
  fd = open(...)
  addr = mmap((caddr_t)0, len, (PROT_READ|PROT_WRITE), MAP_PRIVATE, fd, offset);
```

## 2. 메모리 매핑 함수

### 1) 메모리 매핑 : mmap

- fildes가 가리키는 파일에서 off로 지정한 오프셋부터 len 크기만큼 데이터를 읽어 addr가 가리키는  
  메모리 공간에 매핑
- 성공 : 매핑된 메모리 시작 주소 리턴
- 실패 : 상수 MAP_FAILED 리턴

```c
  #include <sys/mman.h>
  void *mmap(void *addr, size_t len, int prot, int flags, int fildes, off_t off);
```

- addr : 매핑할 메모리 주소 혹은 NULL
- len : 메모리 공간의 크기
- prot : 보호 모드
- flags : 매핑된 데이터의 처리 방법을 지정하는 함수
- fildes : 파일 기술자
- off : 파일 오프셋

#### (1) 시스템 호출의 오류 처리 방법 (prot)

- PROT_READ : 매핑된 파일을 읽기만 함
- PROT_WRITE : 매핑된 파일에 쓰기 허용
- PROT_EXEC : 매핑된 파일을 실행 가능
- PROT_NONE : 매핑된 파일에 접근 불가
- **prot에 PROT_WRITE를 지정하려면 flags에 MAP_PRIVATE를 지정하고, 파일을 쓰기 가능 상태로 열어야함**

#### (2) flags : 매핑된 데이터를 처리하기 위한 정보 저장

- **MAP_SHARED : 다른 사용자와 데이터의 변경 내용 공유**
- MAP_PRIVATE : 데이터의 변경 내용 공유 안함
- MAP_FIXED : 매핑할 주소를 정확히 지정(권장 x)
- MAP_NORESERVE : 매핑된 데이터를 복사해 놓기 위한 스왑영역 할당 안함
- MAP_ANON : 익명의 메모리 영역 주소를 리턴
- MAP_ALIGN : 메모리 정렬 지정
- MAP_TEXT : 매핑된 메모리 영역을 명령을 실행하는 영역으로 사용
- MAP_INITDATA : 초기 데이터 영역으로 사용

### 2) 메모리 매핑 해제 : munmap

- addr이 가리키는 영역에 len 크기만큼 할당해 매핑한 메모리 해제
- 해제한 메모리에 접근하면 SIGSEGV 또는 SIGBUS 시그널 발생

```c
  #include <sys/man.h>
  int munmap(void *addr, size_t len);
```

- addr : 매핑된 메모리 시작 주소
- len : 메모리 영역의 크기

### 3) 메모리 매핑의 보호모드 변경 : mprotect

- mmap 함수로 메모리 매핑을 수행할 때 초기값을 설정한 보호모드를 mprotect 함수로 변경 가능
- prot에 지정한 보호모드로 변경

```c
  #include <sys/mman.h>

  int mprotect(void *addr, size_t len, int prot);
```

- addr : 매핑된 메모리의 시작 주소
- prot : 보호 모드
- len : 메모리 영역의 크기

### 4) 파일의 크기 확장 함수

- 존재하지 않거나 크기가 0인 파일은 메모리 매핑할 수 없음
- 빈 파일 생성시 파일의 크기를 확장한 후 메모리 매핑을 해야함
- truncate(), ftruncate()

#### (1) 경로명을 사용한 파일 크기 확장 : truncate

- path에 지정한 파일의 크기를 length로 지정한 크기로 변경

```c
  #include <unistd.h>

  int truncate(const char *path, off_t length);
```

- path : 크기를 변경할 파일의 경로

#### (2) 파일 기술자를 사용한 파일 크기 확장 : ftruncate

- 일반 파일과 공유메모리에만 사용가능
- 이 함수로 디렉토리에 접근하거나 쓰기 권한이 없는 파일에 접근하면 오류 발생

```c
  #include <unistd.h>

  int ftruncate(int fildes, off_t length);
```

- fildes : 크기를 변경할 파일의 파일 기술자
- length : 변경하려는 크기
