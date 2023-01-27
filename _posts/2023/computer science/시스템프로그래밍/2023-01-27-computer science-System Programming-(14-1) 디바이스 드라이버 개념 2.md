---
title: (시스템 프로그래밍) 14-1 디바이스 드라이버 개념 (디바이스 파일 생성)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 디바이스 드라이버 개념
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 디바이스 드라이버 개념

## 1. 디바이스 파일 생성

### 1) 특징

- 호스트 시스템의 디바이스 파일이 있는 `/dev` 디렉토리 내용 관찰

#### (1) 디바이스 파일의 생성

```c
  mknod<디바이스 파일명> <디바이스 파일 형식> <주번호> <부번호>
```

- 디바이스 파일은 `/dev`에서 관리
- 디바이스 파일 형식 : 문자형 c, 블록형 b
- 리눅스에서 사용되는 디바이스 파일의 주번호

![alt](/assets/images/post/ComputerStudy/804.png)

#### (2) mknod 명령으로 디바이스 파일 생성하기

- 디바이스 이름이 `fd0`, 주번호가 `250`, 부번호가 `0`인 문자 디바이스 파일 생성

```c
  mknod fd0 c 250 0
```

### 2) 디바이스 드라이버

- 디바이스와 시스템 사이에 데이터를 주고 받기 위한 인터페이스
- 표준적으로 동일한 서비스 제공을 목적

#### (1) 커널의 일부분으로 내장

- 커널이 직접 하드웨어를 제어하지 않고 디바이스 드라이버의 인터페이스를 통해 하드웨어 제어

![alt](/assets/images/post/ComputerStudy/805.png)

- 디바이스 하드웨어에 데이터를 읽거나 쓰거나 제어하는 루틴의 집합
- 루틴들은 운영체제에 잘 연동
- 운영체제가 하드웨어를 제어할 수 있도록 인터페이스 제공

![alt](/assets/images/post/ComputerStudy/806.png)

![alt](/assets/images/post/ComputerStudy/807.png)
