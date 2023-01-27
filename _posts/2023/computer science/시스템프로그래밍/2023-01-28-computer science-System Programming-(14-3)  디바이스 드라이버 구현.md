---
title: (시스템 프로그래밍) 14-3 디바이스 드라이버 구현 (디바이스 드라이버 모듈)
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
last_modified_at: "2023-01-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 디바이스 드라이버 구현 (디바이스 드라이버 모듈)

## 1. 디바이스 드라이버 모듈

### 1) 디바이스 드라이버 구성

#### (1) 디바이스 처리

- 응용 프로그램은 디바이스 파일을 통해 디바이스 드라이버 함수와 연결

##### (1-1) 디바이스 드라이버

- 하드웨어를 제어

##### (1-2) 디바이스 파일

- 디바이스 형식과 주번호를 이용해 커널내에 등록된 디바이스 드라이버 함수를 연결

##### (1-3) 문자 디바이스 드라이버

- 응용 프로그램에서 해당 디바이스 드라이버와 디바이스 파일을 호출

##### (1-4) 블록 디바이스 드라이버

- 커널에 직접 호출해서 사용

### 2) 문자 디바이스 드라이버의 기본 구성

#### (1) 문자 디바이스 드라이버의 제작 최소 항목

- 커널 소스 헤더파일
- 저수준 파일 입출력에 대응하는 `file_operations`구조체에 등록할 함수
- `file_operations` 변수
- 문자 디바이스 드라이버를 등록하는 모듈 초기화 함수
- 문자 디바이스 드라이버를 제거하는 모듈 마무리 함수
