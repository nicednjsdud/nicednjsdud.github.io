---
title: 1. 리눅스 와 커널
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Linux
description: Linux
tag: Linux
article_tag1: Linux
article_section: Linux
meta_keywords: Linux
last_modified_at: "2024-02-13 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Linux

## 목차

1. 커널과 운영체제와의 차이
2. 커널은 왜 존재하는가?

## 1. 커널과 운영체제의 차이

### 1) 운영체제가 더 큰 개념

- 커널 + 디바이스 드라이버 + 시스템 유틸리티 + 응용프로그램 + 등등
- 하드웨어와 컴퓨터 사용자의 중개자

### 2) 커널은 운영체제의 핵심 부분

- 하드웨어와 소프트웨어를 이어주는 중계자

## 2. 커널은 왜 존재 하는가?

1. 컴퓨터를 구입하고 부팅을 해보면, 아무것도 없다.
2. 만약 운영체제가 없다면 lol를 어떻게 할가?
3. CPU, GPU, 메모리, 하드디스크, 키보드, 마우스, 모니터, 랜카드, 스피커를 어떻게 사용해야 할까?
4. lol을 하면서, 브라우저 검색을 어떻게 할까?

### 1) 다양한 CPU, 다양한 메모리, 다양한 장치들을 관리

- 밑에것 들은 커널에 소스로 실제로 구현이 되어 있음
- 우리는 이런 것들을 분석하는 것

#### 1-1) Task(Process) Management

- CPU를 추상적 자원인 Task로 제공

#### 1-2) Memory Management

- 메모리를 추상적 자원인 Page, Segement로 제공

#### 1-3) File System

- 디스크를 추상적 자원인 File로 제공

#### 1-4) Network Management

- 네트워크 장치를 추상적 자원인 Socket으로 제공

#### 1-5) Device Driver Management

- 각종 외부 장치에 대한 접근

#### 1-6) Interrupt Handling

- 인터랩트 핸들러

#### 1-7) I/O Communication

- 입출력 통신 관리 ( 입출력 장치의 중개자 )

## 출처

<a href="https://www.youtube.com/watch?v=afkwBG39vzk">[한국에서 제일 쉬운 리눅스 커널 강의 ] 1. 왜 커널 공부를 해야하나</a>
