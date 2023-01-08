---
title: (시스템 프로그래밍) 11-3 이름 있는 파이프
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 이름 있는 파이프
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-06 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 이름 있는 파이프

## 1. 이름 있는 파이프

### 1) FIFO

- 리눅스에서는 Named PIPE 기법을 위해 FIFO 라는 특수 파일을 제공
- 부모-자식간이 아닌 독립적인 프로세스 간에 통신하기 위해서는 이름 잇는 파이프 사용
- FIFO로 사용할 특수파일을 명령이나 함수로 먼저 생성해야 함

#### (1) 특수 파일로 생성되는 FIFO

- 생성 방법에 차이는 있지만 PIPE와 거의 유사
- 익명의 파이프는 따로 이름이 없는 통신 채널인데 비해서 FIFO는 mkfifo()함수에 의해 실제로 생성되는 특수 파일
- 어떤 프로세스라도 생성된 경로로 파일에 접근하여 다른 파일을 사용하듯 읽거나 쓰기 가능
- FIFO로 pipe와 마찬가지로 단방향 통신, **반드시 읽기전용,쓰기전용** 으로만 열어야 함

### 2) 명령으로 FIFO 파일 생성

- mknod 명령
- mkfifo 명령

#### (1) mknod 명령

- FIFO 파일/ 특수 파일 생성
- 형식 mknod filename p

```c
  mknod HAN_FIFO p
```

### 3) 함수로 특수파일 생성

#### (1) 특수파일 생성 : mknod

- 성공 : 0 리턴
- 실패 : -1 리턴

```c
  #include <sys/stat.h>
  int mknod(const char *path, mode_t mode, dev_t dev);
```

- path : 특수 파일을 생성할 경로
- mode : 특수 파일의 종류와 접근 권한 지정

##### (1-1) mode 생성할 특수파일의 종류 지정

- S_IFIFO : FIFO 특수 파일
- S_IFCHAR : 문자 장치 특수 파일
- S_IFDIR : 디렉토리
- S_IFDIR : 블록장치 특수파일
- S_IFREG : 일반 파일

#### (2) FIFO 파일 생성 : mkfifo

- path로 지정한 경로에 접근 권한을 지정해 FIFO 파일 생성
- 성공 : 0 반환
- 실패 : -1 반환

##### (2-1)

- mkfifo() 함수가 정상적으로 실행되면 인자로 넘긴 경로에 특수 파일로 FIFO가 등록됨

##### (2-2)

- 다른 프로세스는 일반 파일에서 사용하는 것 처럼 FIFO를 사용 가능하지만 특정 프로세스가 FIFO를 쓰기용으로  
  열기 전가지는 다른 읽기용 개방은 블럭(Block)됨

##### (2-3)

```c
  #include <sys/types.h>
  #include <sys/stat.h>

  int mkfifo(const chat *pathname, mode_t mode);
```

##### (2-4)`const char *pathname`

- fifo 파일이 생성될 경로를 지정함
- 일반 파일의 경로를 지정하는 것과 동일

##### (2-5) `mode_t mode`

- 생성 될 fifo 파일의 접근 권한을 지정함

## 2. 이름 있는 파이프 관련 함수

### 1) FIFO로 데이터 주고받기

* FIFO 파일을 생성하면 저수준 파일 입출력 함수로 파일을 읽거나 쓸 수 있음

![alt](/assets/images/post/ComputerStudy/577.png)

