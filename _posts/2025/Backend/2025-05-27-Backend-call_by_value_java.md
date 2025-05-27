---
published: true
title: "🔍 자바는 Call By Value일까, Call By Reference일까"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
  - Backend
description: "자바의 메서드 호출 방식은 Call By Value일까? 참조 타입 객체를 넘겼을 때 원본이 바뀌는 이유를 통해 정확히 이해해봅니다."
tag: [Java, Call By Value, Call By Reference, 메서드 호출, 스택, 힙]
article_section: "Java"
meta_keywords: "Java, Call By Value, Call By Reference, 스택 메모리, 힙 메모리, 참조형"
last_modified_at: "2025-05-27 21:45:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

## 🧠 메서드 호출 방식에는 어떤 게 있을까?

### ✅ 값에 의한 호출 (Call By Value)

- **값 자체를 복사해서 넘겨주는 방식**입니다.
- 호출된 함수 내부에서 파라미터 값을 변경해도 **원본은 바뀌지 않습니다.**
- **자바의 원시 타입**(`int`, `boolean`, `double` 등)은 이 방식입니다.

### ✅ 참조에 의한 호출 (Call By Reference)

- **참조(주소)를 넘겨주는 방식**입니다.
- 호출된 함수에서 객체를 변경하면 **원본 객체도 같이 변경됩니다.**
- C++에서는 참조자를 통해 이 방식이 가능합니다.

---

## ☕ 자바는 어떤 방식?

> 자바는 오직 **Call By Value만** 존재합니다.

### ✅ 그런데 참조형 객체 넘기면 바뀌지 않나요?

```java
public void foo() {
    Student student = new Student();
    var(student); // student 객체 넘김
}

public void var(Student student) {
    student.study(); // 원본 객체에 영향 줌
}
```

- 이 코드는 **Call By Reference처럼 보이지만**
- 자바는 `student`라는 **참조값 자체를 복사**해서 넘긴 것
- 결국, **값을 복사한 것** = Call By Value

---

## 📦 스택과 힙

### 🗃️ 변수 저장 구조

- **원시 타입**: 변수 + 값 모두 스택에 저장
- **참조 타입**: 변수(스택) + 객체(힙)에 저장됨

```text
메서드 호출 시 → 스택에 복사된 참조값만 전달
```

![alt](/assets/images/post/computer science/8.png)

---

## 🔄 정리

| 타입 | 호출 방식 | 원본 영향 여부 | 설명 |
|------|------------|----------------|------|
| 원시 타입 | Call By Value | ❌ 영향 없음 | 값만 복사됨 |
| 참조 타입 | Call By Value | ✅ 내부 값 변경 가능 | 참조값이 복사됨, 객체는 같음 |

---

## 💡 결론

- 자바는 무조건 **Call By Value**
- **참조형도 "참조값"을 복사**해서 넘기는 것
- **원본 객체 자체를 바꾸는 것이 아닌**, **같은 객체의 필드를 바꾸는 것**

---

📘 헷갈린다면?  
"자바는 Call By Reference가 **없다**.  
참조형은 **참조값을 복사해서 넘기는** Call By Value다."

