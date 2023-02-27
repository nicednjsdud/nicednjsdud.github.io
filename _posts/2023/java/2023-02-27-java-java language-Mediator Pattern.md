---
published: true
title: Java 48. Mediator Pattern (Design Pattern - 16)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Mediator Pattern (Design Pattern - 16)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Mediator Pattern

## 1. Mediator Pattern 이란?

- 객체간의 상호 작용을 하나의 객체에서 캡슐화하여 처리
- UI프로그래밍에서 많이 사용되는 방법으로 Widget 간의 상호처리를 서로간에 처리하는 것이 아닌 한 객체가 전담하여 처리하도록 하는 방식
- 객체 서로간의 메세지를 전달할 일이 있을 때도 중재자를 두고 전달할 수 있음
- N:N의 관계를 1:N의 관계로 바꿀수 있음

## 2. 의도와 동기

- 객체 지향 방법론에서는 객체의 관련된 처리는 객체 내부에서 하는것이 맞지만, 그렇게하면 상호작용의 급증이 발생하고 시스템의 변경이 어려움
- Mediator 객체가 상호작용을 제어하고 조율하게함.
- 각 객체는 다른 객체의 참조자는 알 필요가 없고 Mediator만 알면 됨
