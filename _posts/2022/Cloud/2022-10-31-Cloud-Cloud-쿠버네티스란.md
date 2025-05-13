---
title: (Cloud) 쿠버네티스란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Cloud
description: 쿠버네티스란?
tag: Cloud
article_tag1: Cloud
article_section: computer
meta_keywords: Cloud
last_modified_at: "2022-10-31 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 쿠버네티스

![alt](/assets/images/post/cloud/4.png)

## 1. 쿠버네티스란?

- 쿠버네티스란 컨테이너화된 애플리케이션이 배포, 확장 및 관리를 자동화하는 오픈 소스 시스템이다.
- 1주일에 수십억 개의 컨테이너를 생성하는 Google이 내부 배포시스템으로 사용하던 `borg`를 기반으로  
  2014년 프로젝트를 시작했고, 여러 커뮤니티의 아이디어와 좋은 사례들을 모아 빠르게 발전하였다.
- 이후 Google이 CNCF(Cloud Native Computing Foundation)에 코드를 기부함으로써,  
  쿠버네티스는 오픈 소스 프로젝트가 되었다.

- 쿠버네티스는 단순한 컨테이너 플랫폼이 아닌 마이크로서비스,클라우드 플랫폼을 지향한다.
- 컨테이너로 이루어진 것들을 손쉽게 담고 관리할 수 있는 그릇 역할을 한다.
- 서버리스, CI/CD, 머신러닝 등 다양한 기능이 쿠버네티스 위에서 동작한다.

## 2. 필요한 이유

- 컨테이너화된 애플리케이션 환경 (Containerized Application)을 탄력적으로 실행할 수있게 된다.

![alt](/assets/images/post/cloud/5.png)

- 프로덕션 환경에서는 애플리케이션을 실행하는 컨테이너를 관리하고 가동 중지 시간이 없는지 확인한다.
- ex) 컨테이너가 다운된다면 다른 컨테이너를 다시 시작하여 가동 중지 시간을 최소화하여햐 한다.
- **이러한 문제를 시스템에 의해 관리되도록 하는 것이 쿠버네티스의 역할이다.**

## 3. 쿠버네티스가 제공하는 기능

![alt](/assets/images/post/cloud/6.png)

### 1) 서비스 디스크버리와 로드 밸런싱

- DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출

### 2) 스토리지 오케스트레이션

- 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소를 시스템에 자동으로 탑재

### 3) 자동화된 롤아웃과 롤백

- 원하는 상태를 서술하고 현재 상태를 원하는 상태로 설정한 속도에 따라 변경 가능

### 4) 자동화된 빈 패킹

- 각 컨테이너가 필요로 하는 CPU와 메모리 (RAM)을 제공

### 5) 자동화된 복구 (self-healing)

- 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체

### 6) 시크릿과 구성 관리

- 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리

<a href="https://tech.ktcloud.com/67">출처 : https://tech.ktcloud.com/67</a>
