---
published: true
title: Java 44. State Pattern (Design Pattern - 12)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: State Pattern (Design Pattern - 12)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-25 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# State Pattern

## 1. State Pattern 이란?

- 클래스가 하나의 상태에 따라 그 내부의 여러 메서드의 기능이 바뀐다고 하면 이를 각각의 클래스로 분리

## 2. 의도와 동기

- 객체의 기능은 상태에 따라 달라질 수 있는데, 이러한 상태가 여러가지이고, 클래스 전반의 모든 기능이 상태에 의존적이라 하면, 상태를  
  클래스로 표현하는것이 적절함
- 클래스로 분리하지 않게 되면 상태가 여러가지인 경우 많은 if-else문이 사용되고 추후 상태가 추가되거나 삭제될 때 수정해야 하는 사항이 너무 많아짐

## 3. 객체 협력

### 1) Context

- ConcreteState의 인스턴스를 관리하고 서로 상태가 바뀌는 순간을 구현할 수 있다.

### 2) State

- Context가 사용할 메서드를 선언한다.

### 3) ConcreteState

- 각 상태 클래스가 수행할 State에 선언된 메서드를 구현
