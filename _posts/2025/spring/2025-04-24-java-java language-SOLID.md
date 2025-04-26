---
published: true
title: "🎯 SOLID 원칙 한방 정리 + 실무 적용 및 리팩토링 예시"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
description: "객체지향 설계의 핵심 SOLID 원칙을 이해하고, 각 원칙별로 간단한 리팩토링 전/후 예제를 통해 바로 적용할 수 있게 정리했습니다."
tag: "SOLID, 객체지향, 백엔드, 리팩토링, 클린코드"
article_tag1: "SOLID"
article_section: "Backend"
meta_keywords: "SOLID 리팩토링, 객체지향 설계 원칙, 클린코드, 백엔드 설계"
last_modified_at: "2025-04-24 22:30:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🎯 SOLID 원칙 한방 정리 + 실무 적용 및 리팩토링 예시

---

## 📌 SOLID란?

> 객체지향 설계의 5대 원칙  
> 유지보수성, 확장성, 유연성의 기반이 되는 설계 원칙입니다.  
> Solid 원칙은 아래처럼 구성됩니다:

- **S**ingle Responsibility Principle
- **O**pen-Closed Principle
- **L**iskov Substitution Principle
- **I**nterface Segregation Principle
- **D**ependency Inversion Principle

---

## 1️⃣ SRP - 단일 책임 원칙

> 클래스는 단 하나의 책임만 가져야 한다

### 🔧 리팩토링 전

```java
class UserService {
    public void registerUser() {
        // 회원가입 로직
    }

    public void sendWelcomeEmail() {
        // 이메일 전송 로직
    }
}
```

➡ 회원 가입과 이메일 전송이 **동시에 책임지고 있음**

### ✅ 리팩토링 후

```java
class UserService {
    private EmailService emailService;

    public void registerUser() {
        // 회원가입 로직
        emailService.sendWelcomeEmail();
    }
}

class EmailService {
    public void sendWelcomeEmail() {
        // 이메일 전송
    }
}
```

➡ 각각의 책임을 분리함으로써 변경 포인트가 줄어듦

---

## 2️⃣ OCP - 개방 폐쇄 원칙

> 확장에는 열려 있고, 변경에는 닫혀 있어야 한다

### 🔧 리팩토링 전

```java
class DiscountService {
    public int calculateDiscount(String grade, int price) {
        if (grade.equals("VIP")) return price - 1000;
        else return price - 500;
    }
}
```

➡ 등급이 추가될 때마다 `if-else` 수정 필요

### ✅ 리팩토링 후

```java
interface DiscountPolicy {
    int discount(int price);
}

class VIPDiscount implements DiscountPolicy {
    public int discount(int price) {
        return price - 1000;
    }
}

class BasicDiscount implements DiscountPolicy {
    public int discount(int price) {
        return price - 500;
    }
}

class DiscountService {
    public int calculate(DiscountPolicy policy, int price) {
        return policy.discount(price);
    }
}
```

➡ 새로운 정책 추가 시 클래스만 추가하면 됨

---

## 3️⃣ LSP - 리스코프 치환 원칙

> 자식 클래스는 언제나 부모 클래스로 대체 가능해야 한다

### 🔧 리팩토링 전

```java
class Rectangle {
    protected int width, height;

    public void setWidth(int w) { width = w; }
    public void setHeight(int h) { height = h; }

    public int getArea() { return width * height; }
}

class Square extends Rectangle {
    @Override
    public void setWidth(int w) {
        width = height = w;
    }

    @Override
    public void setHeight(int h) {
        width = height = h;
    }
}
```

➡ `Square`는 `Rectangle`의 기대 동작을 깨트림

### ✅ 리팩토링 후

```java
interface Shape {
    int getArea();
}

class Rectangle implements Shape {
    private int width, height;

    Rectangle(int w, int h) {
        this.width = w;
        this.height = h;
    }

    public int getArea() {
        return width * height;
    }
}

class Square implements Shape {
    private int side;

    Square(int s) {
        this.side = s;
    }

    public int getArea() {
        return side * side;
    }
}
```

➡ 더 이상 `Rectangle`에 억지 상속하지 않고, 역할만 공유

---

## 4️⃣ ISP - 인터페이스 분리 원칙

> 클라이언트는 자신이 사용하지 않는 메서드에 의존하지 않아야 한다

### 🔧 리팩토링 전

```java
interface Animal {
    void fly();
    void walk();
}

class Dog implements Animal {
    public void fly() {
        // 아무 동작 안함
    }

    public void walk() {
        // 걷기
    }
}
```

➡ `Dog`는 `fly()`를 쓸 일이 없음에도 구현해야 함

### ✅ 리팩토링 후

```java
interface Walkable {
    void walk();
}

interface Flyable {
    void fly();
}

class Dog implements Walkable {
    public void walk() {
        // 걷기
    }
}
```

➡ 필요한 인터페이스만 구현하게 분리

---

## 5️⃣ DIP - 의존성 역전 원칙

> 상위 모듈은 하위 모듈에 의존하지 않고, 추상화에 의존해야 한다

### 🔧 리팩토링 전

```java
class MySQLRepository {
    public void save() {
        // DB 저장
    }
}

class UserService {
    private MySQLRepository repo = new MySQLRepository();

    public void register() {
        repo.save();
    }
}
```

➡ 구현체에 직접 의존 → 교체, 테스트 불가

### ✅ 리팩토링 후

```java
interface Repository {
    void save();
}

class MySQLRepository implements Repository {
    public void save() {
        // DB 저장
    }
}

class UserService {
    private final Repository repo;

    public UserService(Repository repo) {
        this.repo = repo;
    }

    public void register() {
        repo.save();
    }
}
```

➡ 인터페이스를 통해 의존성 주입 → 유연성 증가

---

## 💡 SOLID 한줄 암기 팁

```
🐟 소오리인터역
→ 단일 책임, 개방 폐쇄, 리스코프 치환, 인터페이스 분리, 의존성 역전
```

---

## ✅ 마무리 요약

| 원칙 | 핵심 목적                       |
| ---- | ------------------------------- |
| SRP  | 하나의 책임만 가지자            |
| OCP  | 변경 없이 기능 확장             |
| LSP  | 자식은 부모처럼 사용            |
| ISP  | 인터페이스는 작게 쪼개자        |
| DIP  | 구현이 아니라 추상화에 의존하자 |

---
