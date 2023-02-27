---
published: true
title: Java 46. Memento Pattern (Design Pattern - 14)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Memento Pattern (Design Pattern - 14)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Memento Pattern

## 1. Memento Pattern 이란?

- 내부상태를 객체화하여, 나중에 객체가 이 상태로 복구 가능하게 함
- 인스턴스의 상태를 보존해 두었다가 보존해 둔 정보를 가지고 인스턴스를 원래 상태롭 복원
- 인스턴스를 복원하기 위해서는 내부 정보에 자유롭게 접근 가능해야 함
- 캡슐화가 파괴가 일어나지 않도록 주의해야 함

## 2. 의도와 동기

- 이전의 상태로 되돌리는 undo
- 했던 작업을 다시 하는 redo
- 기억해야 하는 순간을 저장하는 객체
- 오류를 복구하거나 수행 결과를 취소하기 위한 작업에 사용

## 3. 객체 협력

### 1) Memento

- Originator 객체의 내부 상태를 필요한 만큼 저장한다. Originator만이 Memento에 접근할 수 있다.

### 2) Originator

- Memento를 생성하여 현재 객체의 상태를 저장하고 내부 상태를 복구

### 3) CareTaker (undo mechanism)

- Memento의 보관을 책임지기는 하지만, memento의 내부를 확인할 수 없음

## 4. 중요한 결론

- 복잡한 Originator 클래스의 내부 상태를 다른 객체로 분리함으로써 상태에 대한 캡슐화를 보장
- 복구에 필요한 상태만 따로 관리함으로써 Originator내부에서 저장하지 않고 Originator가 단순해질 수 있다.
- Memento의 사용에 오버헤드가 발생할 수 있다.
