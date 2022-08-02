---
title: (Spring) 15. Spring SOLID
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Spring SOLID
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-25 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# SOLID (Spring)

## 1. SOLID

---

클린코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리

- SRP : 단일 책임 원칙 (single responsibility principle)
- OCP : 개방 - 폐쇄 원칙 (Open/closed principle)
- LSP : 리스코프 치환 원칙 (Liskov substitution principle)
- ISP : 인터페이스 분리 원칙 (Interface segregation principle)
- DIP : 의존관계 역전 원칙 (Dependency inversion principle)

## 2. SRP 단일 책임 원칙

---

- 한 클래스는 하나의 책임만 가져야 한다.
- 하나의 책임이라는 것은 모호하다.
  - 클 수 있고, 작을수도 있다.
  - 문맥과 상황에 따라 다르다.
- **중요한 기준은 변경**이다. 변경이 있을때 파급효과가 적으면 단일 책임 원칙을 잘 따른것
- ex) UI변경, 객체의 생성과 사용을 분리

## 3. OCP 개방 - 폐쇄 원칙

---

- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야한다.
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현

## 4. LSP 리스코프 치환 원칙

---

- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀수 있어야 한다.
- 다형성에서 하위클레스는 인터페이스 규약을 다지켜야 한다는 것, 다형성을 지원하기 위한 원칙,  
  인터페이스를 구현한 구현체는 믿고 사용하려면 이 원칙이 필요하다.
- 단순히 컴파일에 성공하는 것을 넘어서는 이야기

## 5.ISP 인터페이스 분리 원칙

---

- 특정 클라이언트를 위한 인터페이스 여러개가 범용 인터페이스 하나보다 낫다.

```
    자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
    사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리
```

- 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음.
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.

## 6. DIP 의존관계 역전 원칙

---

- 프로그래머는 "추상화에 의존해야지, 구체화에 의존하면 안된다." 의존성 주입은 이원칙  
  을 따르는 방법 중 하나이다.

## 7. 정리

---

- 객체 지향의 핵심은 다형성
- 다형성 만으로 쉽게 부품을 갈아 끼우듯이 개발할 수 없다.
- 다형성 만으로 구현 객체를 변경할때 클라이언트 코드도 함께 변경된다.
- **다형성 만으로는 OCP,DIP를 지킬 수 없다.**

<a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8">출처 : 인프런 스프링</a>
