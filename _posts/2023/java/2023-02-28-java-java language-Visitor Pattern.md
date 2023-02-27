---
published: true
title: Java 50. Visitor Pattern (Design Pattern - 18)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Visitor Pattern (Design Pattern - 18)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-28 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Visitor Pattern

## 1. Visitor Pattern 이란?

- 구조안을 돌아다니며 일을 함 "방문자"
- 객체 구조의 요소들이 수행해야할 기능을 모아둔 패턴
- 각 객체 요소를 변경하지 않고, 기능을 추가할 수 있음
- 데이터의 구조와 처리를 분리하여 치리하는 부분을 객체로 만들어 각 데이터 구조를 돌아다니며 오퍼레이션이 수행되도록 함
- 각 데이터는 이러한 visitor를 accept 함

## 2. 의도와 동기

- 추상구문 트리의 예
- 문법적 처리를 위해 각 노드마다 수행해야 하는 기능을 따로 정의 해야함
- 유사한 오퍼레이션들이 여러 객체 분산되어 있어서 디버깅이 어렵고, 가독성이 떨어짐
- 각 클래스로부터 관련한 클래스를 모아서 Visitor를 별도로 만들어줌
- 각 노드 클래스는 visitor가 방문하면 accept하여 해당 노드에 대한 기능이 수행되도록 함

## 3. 객체 협력

### 1) Visitor

- 각 객체에서 수행해야 할 기능을 선언
- 메서드의 이름은 요청을 받을 객체를 명시

### 2) ConcreteVisitor

- Visitor 클래스에 선언된 메서드를 구현
- 각 메서드는 객체에 해당하는 알고리즘을 구현

### 3) Element

- Visitor가 수행될 수 있는 Accept()메서드를 선언

### 4) ConcretElement

- 매개변수로 Visitor를 받아주는 Accept()메서드를 구현

### 5) ConcreteAggregate

- 해당하는 ConcreteIterator의 인스턴스를 반환하도록 Iterator 생성 인터페이스를 구현

## 4. 중요한 결론

- 여러 요소에 대해 유사한 기능의 메서드를 한곳에 모아서 관리하게 되고, 여러 클래스에 걸친 메서드를 추가하기 용이함
- 각 클래스에 대한 기능이 자주 변경되거나 알고리즘의 변화가 많을때 사용하는것이 효율적임
- 새로운 요소 클래스를 추가하게 되면 그에 해당되는 기능을 모든 Visitor에서 구현해야 함
- 따라서 요소의 변화가 거의 없고 기능의 추가 삭제가 자주 발생할때 사용하는 것이 좋음
- 각 객체의 오퍼레이션이 외부에 노출되는 것이므로 객체지향 프로그래밍의 캡슐화 전략에 위배
- 주로 Composite 패턴에서 자주 사용될 수 있음
