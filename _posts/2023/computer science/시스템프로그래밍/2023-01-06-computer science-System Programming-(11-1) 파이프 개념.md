---
title: (시스템 프로그래밍) 11-1 파이프 개념
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 파이프 개념
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

# 시스템 프로그래밍 - 파이프 개념

## 1. 파이프 개념 및 종류

### 1) 파이프

- 여러 개의 프로세스가 공통으로 사용하는 **임시공간**
- **임시공간**은 실제로 파일 시스템에 생성되는 임시 파일
- 하나의 프로세스가 파이프에 쓰게 되면 다른 프로세스는 그 파이프에서 읽는 방식으로 쓰게 됨
- 파이프는 시스템 내부에서 관리하는 임시 파일을 이용하므로, 다른 IPC 기법 중 하나인 SIGNAL 과는 다르게  
  **대용량의 메세지도 전송이 가능**

#### (1) 흐름도

![alt](/assets/images/post/ComputerStudy/570.png)

#### (2) 종류

- 이름 없는 익명의 파이프
- 이름을 가진 Named Pipe

#### (3) 이름 없는 익명의 파이프의 특성

##### (3-1) 파이프는 입구와 출구의 개념이 없음

- 방향성이 없기 때문에 자신이 쓴 메세지를 자신이 읽을 수 있음
- 두 개의 프로세스가 통신할 때는 읽기전용 파이프와 쓰기 전용 파이프의 두개의 파이프를 사용
- 두개의 파이프를 생성하고, 한쪽 파이프를 일부러 닫아 버리는 것
- 파이프를 두개 생성하여 하나의 방향으로만 갈수 있도록 함

![alt](/assets/images/post/ComputerStudy/571.png)

##### (3-2) 파이프는 fork() 함수에 의해 복사 되지 않음

- fork() 함수에 의해서 프로세스가 생성되면 자식 프로세스는 부모가 사용하던 변수를 복사하게 됨
- 하지만 파이프의 경우 복사되는 것이 아니라 File Descriptor를 공유하게 되며, 즉 자식 프로세스와  
  부모 프로세스가 같은 파이프를 가리키게 됨

##### (3-3) 부모 자식프로세스 사이에서만 파이프를 사용 가능 (단점)

- 파이프는 운영체제에서 **임시로 생성되는 파일**이고, 접근 가능한 방법은 File Descriptor(파일 디스크립터)를  
  공유하는 방법만이 존재

![alt](/assets/images/post/ComputerStudy/572.png)

##### (3-4)

- Named PIPE(네임드 파이프)의 경우 다른 프로세스도, 지정한 이름으로 파일 디스크립터를 열수 있음
- 부모 자식 프로세스 간이 아니더라도 사용할 수 있음

## 2. PIPE/ FIFO 개념

### 1) 파이프 생성 : popen

- fork()함수를 실행해 자식 프로세스를 만들고 command에서 지정한 명령을 exec()함수를 실행해 자식 프로세스가  
  수행하도록 함
- 성공 : 파일 포인터
- 실패 : 널 포인터

### 2) 파이프 닫기 : pclose

- 지정한 파이프를 닫음
- 관련된 waitpid() 함수 수행 후 자식 프로세스들이 기다렸다가 리턴
- 성공 : 자식 프로세스의 상태 값 리턴
- 실패 : -1 리턴

```c
  #include <stdio.h>
  int pclose(FILE *stream);
```

### 3) pipe

- 리눅스에서는 파이프를 사용하기 위해서 pipe() 함수를 제공함

#### (1) 파이프의 Descriptor를 저장할 배열

- `filedes[0]`에는 PIPE의 읽기전용 Descriptor 저장
- `filedes[1]`에는 PIPE의 쓰기전용 Descriptor 저장

#### (2)

- pipe() 함수에 의해 생성되는 파일 디스크립터에는 일반 파일처럼 읽기/쓰기 작업이 가능
- 파이프로 사용할 파일 기술자 2개를 인자로 지정
- `filedes[0]`는 읽기, `filedes[1]`은 쓰기용 파일 기술자

```c
  #include <unistd.h>
  int pipe(int filedes[2])'
```

- 성공 : 0 반환
- 실패 : -1 반환

##### (2-1)

- 익명의 파이프는 외부 프로세스와 파일 디스크립터를 공유할 방법이 없음
- 부모와 자식 프로세스 사이에서만 통신 가능

##### (2-2)

- fork()함수를 이용한 통신방식

#### (3) pipe 함수로 통신과정

##### (3-1) pipe 함수를 호출하여 파이프로 사용할 파일 기술자 생성

![alt](/assets/images/post/ComputerStudy/573.png)

##### (3-2) fork 함수로 자식 프로세스 생성

- pipe도 자식 프로세스로 복사됨

![alt](/assets/images/post/ComputerStudy/574.png)

##### (3-3) 통신방향 결정 (파이프는 기본적으로 단방향)

![alt](/assets/images/post/ComputerStudy/575.png)

### 4) FIFO

* 양방향 파이프의 활용
* 파이프는 기본적으로 단방향이므로 양방향 통신을 위해서는 파이프를 2개 생성함

![alt](/assets/images/post/ComputerStudy/576.png)
