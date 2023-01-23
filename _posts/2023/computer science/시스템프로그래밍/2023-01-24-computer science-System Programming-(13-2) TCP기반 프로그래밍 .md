---
title: (시스템 프로그래밍) 13-2 TCP 기반 프로그래밍
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: TCP 기반 프로그래밍
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-24 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - TCP 기반 프로그래밍

## 1. TCP 기반 프로그래밍

### 1) 동작 방식

#### (1) 반복 서버

- 데몬 프로세스가 직접 모든 클라이언트의 요청을 차례로 처리

#### (2) 동시동작서버

- 데몬 프로세스가 직접 서비스를 제공하지 않음
- 서비스와 관련있는 다른 프로세스를 `fork()`함수로 생성해 클라이언트와 연결시켜줌

#### (3) 인터넷 소켓 활용 통신 절차

![alt](/assets/images/post/ComputerStudy/779.png)

#### (4) 유형 - standalone 타입

- 시스템에서 독자적으로 프로세스가 구동되어 서비스를 제공하는 데몬
- 메모리에 항상 구동되어 있음
- 웹서버 (httpd), DB서버 (mysqld) 등
- 데몬 실행 스크립트 파일 : `/etc/init.d`에 주로 있음

#### (5) 유형 - xinetd 타입

- inetd의 단점을 개선한 데몬
- 대부분의 리눅스에 사용
- 수퍼 데몬이라고 하며 다른 하위의 데몬을 관리하는 상위 데몬
- 외부에서 요청이 있을때만 하위 데몬을 실행시킨 후에 그 데몬이 서비스를 담당하도록 하고 서비스가 종료되면 데몬 종료
- xinetd 데몬 위치 : `/etc/xinetd.d`
- 데몬 설정 파일 : `/etc/xinetd.conf`

## 2. 반복서버와 동시동작 서버


