---
published: true
title: Java 33. 객체지향 프로그래밍과 객체지향 설계
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: 재귀의 귀재
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 객체지향 프로그래밍

## 1. 객체지향 프로그래밍

### 1) 추상화

- 어떤 영역에서 필요로 하는 속성이나 기능을 추출하는 작업
- 데이터 구조, 표현방법에 대한 추상화
- 처리 과정에 대한 추상화

### 2) 캡슐화

- 데이터를 감사서 외부에서 사용 가능한 부분만을 제공
- 사용하는 코드가 세부적인 사항을 알 필요가 없음
- 단순한 접근을 제공하여 오류가 생길 부분을 감소함

### 3) 상속성

- 일반적인 개념의 객체에서 보다 구체적인 개념의 객체의 관계를 표현
- 상속관계의 클레스는 상위 클래스의 타입을 내포함
- 상위 클래스의 속성과 기능을 하위 클래스에서 사용하거나 재정의 할 수 있음

### 4) 다형성

- 같은 메세지, 같은 구현에 대해 각 객체가 다른 표현과 결과를 나타내는 것
- 클래스의 상속, 인터페이스의 구현 시에 각각의 다른 구현을 가진 클래스들이 상위 타입으로 업캐스팅이 되고  
  이 때, 각 클래스에서 오버라이딩한 메서드가 존재하는 경우 같은 상위 타입으로 선언된다 하더라고 각기의 다른 인스턴스의  
  메서드가 호출됨
- C++의 경우 virtual function만이 재정의 된 함수가 호출되지만 자바의 경우는 모든 메서드가 가상함수 기반으로 구현  
  되므로 하위 클래스에 재정의 된 메서드가 있는 경우 재정의된 메서드가 호출 됨

## 2. 객체 지향 설계

- Design Heuistics
  - Abstract class vs Concrete class
  - Class Inheritance vs Object Compostion
  - Interface Inheritance vs Implementation Inheritance Etc..

## 3. 응집도와 결합도

- 잘 만들어진 소프트웨어는 응집도는 높고 결합도는 낮어야 함

### 1) 응집도

- 하나의 모듈, 객체 내부의 요소들간의 연관성
- 하나의 책임을 구현하는 하나의 객체는 높은 응집도를 가짐

### 2) 결합도

- 객체 상호관의 연관 관계
- 결합도가 높으면 하나의 객체를 수정할 때 다른 객체도 수정해야 함
