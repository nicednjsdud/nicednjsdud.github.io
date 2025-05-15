---
published: true
title: "📦 응집도, 결합도, 캡슐화 - 객체지향 설계의 핵심을 제대로 이해하기"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "높은 응집도, 낮은 결합도, 강한 캡슐화는 좋은 객체지향 설계를 위한 기본기입니다. 개념뿐 아니라 예시를 통해 쉽게 이해해봅니다."
tag: "OOP, 설계원칙, 응집도, 결합도, 캡슐화"
article_tag1: "객체지향 설계"
article_section: "소프트웨어 디자인"
meta_keywords: "응집도, 결합도, 캡슐화, 객체지향, 모듈화"
last_modified_at: "2025-05-15 02:10:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

## ✅ 개념 요약

| 용어 | 정의 |
|------|------|
| **응집도(Cohesion)** | 모듈 내부 구성 요소끼리 **서로 관련된 정도** |
| **결합도(Coupling)** | 한 모듈이 다른 모듈에 **얼마나 의존하고 있는지** |
| **캡슐화(Encapsulation)** | 객체 내부 상태/로직을 **외부로부터 숨기는 것** |

---

## 🎯 좋은 설계란?

> 일반적으로 좋은 설계는 **높은 응집도와 낮은 결합도**를 가진 구조입니다.

- 응집도 ↑: 모듈 내부가 하나의 책임에 집중 → **변경에 강한 코드**
- 결합도 ↓: 다른 모듈과 얽히지 않음 → **재사용성과 유지보수 ↑**
- 캡슐화 ↑: 내부 구현을 숨김 → **결합도 감소에 기여**

---

## 💡 예제 1: 응집도가 낮은 클래스

```java
public class EmployeeManager {
    public void calculateSalary() {
        // 급여 계산 로직
    }

    public void sendEmailToCustomer() {
        // 고객에게 이메일 보내는 로직
    }

    public void printMonthlyReport() {
        // 월간 보고서 출력
    }
}
```

### ❌ 문제점

- 하나의 클래스가 너무 많은 책임을 가짐
- 급여, 이메일, 보고서 출력은 **연관성 낮은 작업**
- **응집도가 낮음 → 변경 시 서로 영향을 줄 가능성**

---

## ✅ 개선: 응집도 높은 구조

```java
public class PayrollService {
    public void calculateSalary() {
        // 급여 관련 책임만 수행
    }
}

public class EmailService {
    public void sendEmailToCustomer() {
        // 이메일 전송만 수행
    }
}

public class ReportPrinter {
    public void printMonthlyReport() {
        // 보고서 출력만 수행
    }
}
```

- 각각의 클래스는 **단일 책임(SRP)** 에 충실
- 내부 요소들끼리 관련 있고 응집력이 높음

---

## 💡 예제 2: 결합도가 높은 구조

```java
public class OrderService {
    private UserService userService = new UserService(); // 직접 생성

    public void placeOrder() {
        userService.checkUserStatus();
        // 주문 처리 로직
    }
}
```

### ❌ 문제점

- `OrderService`는 `UserService`의 **구체적인 생성 방식까지 알고 있음**
- `UserService`를 교체하려면 `OrderService`도 함께 수정 필요

---

## ✅ 개선: 낮은 결합도 (의존성 주입 활용)

```java
public class OrderService {
    private final UserService userService;

    public OrderService(UserService userService) {
        this.userService = userService;
    }

    public void placeOrder() {
        userService.checkUserStatus();
    }
}
```

- `OrderService`는 `UserService`의 **구체 구현을 몰라도 됨**
- 의존성 역전(DIP) → 결합도 낮아짐 → 테스트나 변경이 쉬움

---

## 🧪 예제 3: 캡슐화가 약한 객체

```java
public class BankAccount {
    public int balance;

    public void deposit(int amount) {
        balance += amount;
    }
}
```

### ❌ 문제점

- 외부에서 `balance`를 **직접 변경 가능** → 무결성 깨질 수 있음

```java
BankAccount account = new BankAccount();
account.balance = -1000; // 의도치 않은 상태
```

---

## ✅ 캡슐화 강화: 접근 제어자 활용

```java
public class BankAccount {
    private int balance;

    public void deposit(int amount) {
        if (amount <= 0) throw new IllegalArgumentException();
        balance += amount;
    }

    public int getBalance() {
        return balance;
    }
}
```

- 내부 상태를 외부에 노출하지 않음
- 메서드로만 조작 → **상태 안정성 보장**
- 캡슐화를 통해 **결합도 감소 + 응집도 증가**

---

## 🔄 요약 비교

| 기준 | 좋지 않은 설계 | 좋은 설계 |
|------|----------------|------------|
| 응집도 | 여러 책임 혼합된 클래스 | 하나의 책임에 집중 |
| 결합도 | 구체 클래스에 의존 | 추상화, DI로 분리 |
| 캡슐화 | 필드 직접 접근 허용 | 상태 은닉, 메서드 제공 |

---

## ✅ 마무리 정리

- 좋은 설계는 **캡슐화를 통해 내부 구현을 숨기고**,  
  **응집도는 높이고 결합도는 낮추는 것**입니다.

- 이를 통해 시스템은 **변경에 강하고**,  
  **유지보수가 쉬우며 재사용 가능한 구조**가 됩니다.


