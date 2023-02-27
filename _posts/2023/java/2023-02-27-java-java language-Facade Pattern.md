---
published: true
title: Java 47. Facade Pattern (Design Pattern - 15)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Facade Pattern (Design Pattern - 15)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Facade Pattern

## 1. Facade Pattern 이란?

- 간단한 창구
- 서브 시스템이 여러개인 경우 통합한 하나의 인터페이스를 제공
- 서비 시스템을 좀 더 편하게 이용하기 위한 높은 수준의 인터페이스를 정의
- 각 서브시스템의 역할이나 의존관계를 내부에서 순서로 사용할 수 있도록 외부에는 간단한 인터페이스를 제공

## 2. 의도와 동기

- 서브 시스템을 합성하여 사용하는 다수 객체의 집합에 대한 하나의 일관된 인터페이스를 제공함으로써 사용하기 쉽게 함
- 사용의 오류를 방지
- 컴파일러 시스템의 경우 컴파일 명렁어만 사용할 뿐 내부의 각 서브시스템의 구조는 알 필요가 없음

## 3. 객체 협력

### 1) Facade

- 하나의 일관된 인터페이스 제공

## 4. 중요한 결론

- 복잡한 서브시스템들에 대한 단순하고 기본적인 인터페이스를 앞에서 제공
- 클라이언트와 서브 시스템간의 결합도를 줄임
