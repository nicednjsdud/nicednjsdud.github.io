---
title: (시스템 프로그래밍) 10-3 메모리 관련 함수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 메모리 관련 함수
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

# 시스템 프로그래밍 - 메모리 관련 함수

## 1. 메모리 매핑 활용 데이터 교환

- **부모 프로세스와 자식 프로세스가 메모리 매핑을 사용하여 데이터 교환 가능**

### 1) 매핑된 메모리 동기화 : msync

- 매핑된 메모리의 내용과 백업 내용이 일치하도록 동기화 필요
- addr로 시작하는 메모리 영역에서 len 길이 만큼의 내용을 백업 저장장치에 기록

```c
  #include <sys/mman.h>

  int msync(void *addr, size_t len, int flags);
```

- addr : 매핑된 메모리의 시작 주소
- len : 메모리 영역의 크기
- flags : 동기화 동작

#### (1) flags : 함수의 동작 지시

- MS_ASYNC : 비동기 쓰기 작업
- MS_SYNC : 쓰기 작업을 완료할 때까지 msync 함수는 리턴 안함
- MS_INVALIDATE : 메모리에 복사되어 있는 내용을 무효화

### 2) 데이터 교환하기

- 부모 프로세스나 자식 프로세스가 매핑된 메모리의 내용을 변경하면 다른 프로세스도 변경 내용을 알 수 있다.
