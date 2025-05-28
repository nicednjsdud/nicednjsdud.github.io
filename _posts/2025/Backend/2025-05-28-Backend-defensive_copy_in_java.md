---
published: true
title: "자바에서의 방어적 복사(Defensive Copy)와 깊은 복사의 중요성"
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
last_modified_at: "2025-05-28 21:45:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---


## 🛡️ 방어적 복사란?

방어적 복사는 객체의 내부 상태가 외부로부터 변경되지 않도록 복사본을 제공하는 기법입니다. 이를 통해 객체의 불변성을 유지하고, 예기치 않은 사이드 이펙트를 방지할 수 있습니다.

### 📍 사용 시점

1. **생성자에서의 방어적 복사**: 외부에서 전달된 가변 객체를 내부에 저장할 때, 복사본을 만들어 저장합니다.
2. **Getter 메서드에서의 방어적 복사**: 내부의 가변 객체를 외부에 반환할 때, 복사본을 반환합니다.

---

## 🔄 깊은 복사와 얕은 복사의 차이

| 구분       | 설명                                               | 예시 코드 |
|------------|----------------------------------------------------|-----------|
| 얕은 복사  | 객체의 참조만 복사하여 원본과 복사본이 같은 객체를 참조 | `List<LottoNumber> copy = originalList;` |
| 깊은 복사  | 객체의 실제 값을 복사하여 원본과 복사본이 독립적인 객체를 참조 | `List<LottoNumber> copy = new ArrayList<>(originalList);` |

**주의**: `new ArrayList<>(originalList);`는 리스트 자체는 복사하지만, 리스트 안의 객체들은 동일한 참조를 가리키므로 완전한 깊은 복사가 아닙니다. 리스트 안의 객체들도 복사하려면 각 객체의 복사본을 생성해야 합니다.

---

## 🧪 예제 코드 분석

```java
public class Lotto {

  private final List<LottoNumber> numbers;

  public Lotto(List<LottoNumber> numbers) {
      validateSize(numbers);
      this.numbers = new ArrayList<>(numbers);  // 방어적 복사
  }

  private void validateSize(List<LottoNumber> numbers) {
      if (numbers.size() != 6) {
          throw new IllegalArgumentException("로또 번호는 6개여야 합니다.");
      }
  }
}
```

### 🔍 문제점 분석

1. **얕은 복사로 인한 불변성 위반 가능성**
2. **검증 시점의 문제** (복사 전에 검증이 이루어짐)

---

## ✅ 개선된 코드

```java
public class Lotto {

  private final List<LottoNumber> numbers;

  public Lotto(List<LottoNumber> numbers) {
      List<LottoNumber> defensiveCopy = new ArrayList<>();
      for (LottoNumber number : numbers) {
          defensiveCopy.add(new LottoNumber(number)); // 깊은 복사
      }
      validateSize(defensiveCopy);
      this.numbers = defensiveCopy;
  }

  private void validateSize(List<LottoNumber> numbers) {
      if (numbers.size() != 6) {
          throw new IllegalArgumentException("로또 번호는 6개여야 합니다.");
      }
  }
}
```

---

## 🔒 불변 컬렉션 사용

```java
public List<LottoNumber> getNumbers() {
    return Collections.unmodifiableList(numbers);
}
```

---

## 📌 결론

- **방어적 복사**는 객체의 불변성과 캡슐화를 유지하기 위한 중요한 기법입니다.
- **깊은 복사**와 **얕은 복사**의 차이를 이해하고, 상황에 맞게 적절한 복사 방법을 선택해야 합니다.
- **불변 컬렉션**을 사용하여 외부에서의 변경을 방지할 수 있습니다.
