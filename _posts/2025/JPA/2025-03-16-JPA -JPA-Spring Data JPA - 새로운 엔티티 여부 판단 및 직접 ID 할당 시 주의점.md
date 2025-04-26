---
published: true
title: "🔍 Spring Data JPA - 새로운 엔티티 여부 판단 및 직접 ID 할당 시 주의점"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - JPA
description: "Spring Data JPA에서 새로운 엔티티 여부를 판단하는 방법과 직접 ID 할당 시 발생할 수 있는 문제점 및 해결 방법"
tag: "Spring, JPA, Hibernate, Persistable, 엔티티 관리"
article_tag1: "Spring"
article_section: "JPA"
meta_keywords: "Spring Data JPA, 엔티티 관리, Hibernate, Persistable, ID 할당"
last_modified_at: "2025-03-16 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🔍 Spring Data JPA - 새로운 엔티티 여부 판단 및 직접 ID 할당 시 주의점**

---

## **📌 1. Spring Data JPA에서 엔티티의 신규 여부 판단**

Spring Data JPA에서 **엔티티가 새로운지 여부를 판단하는 것은 매우 중요**합니다.  
이것은 JPA가 **엔티티를 데이터베이스에 저장할 때 `persist`를 사용할지, 아니면 `merge`를 사용할지를 결정**하는 데 직접적인 영향을 줍니다.

Spring Data JPA에서는 **`JpaEntityInformation`의 `isNew(T entity)` 메서드를 사용하여 엔티티의 신규 여부를 판단**합니다.  
이 메서드는 `JpaMetamodelEntityInformation` 클래스를 통해 동작하며, **엔티티의 `@Version` 필드나 `@Id` 필드의 상태를 기반으로 신규 여부를 결정**합니다.

✅ **즉, 엔티티가 새로운 경우 (`isNew()`가 `true` 반환)**  
→ `persist()`를 사용하여 **새로운 데이터로 삽입**

✅ **엔티티가 기존 데이터로 판단되는 경우 (`isNew()`가 `false` 반환)**  
→ `merge()`를 사용하여 **기존 데이터를 수정**

---

## **📌 2. 직접 ID 할당 시 발생하는 문제**

일반적으로 JPA에서는 `@GeneratedValue(strategy = GenerationType.IDENTITY)`을 사용하여 **자동으로 ID를 생성**합니다.  
그러나 개발자가 **직접 엔티티의 ID를 설정하는 경우**, 예상치 못한 문제가 발생할 수 있습니다.

### **🔹 문제 상황**

```java
@Entity
public class User {

    @Id
    private String id;  // 직접 ID 할당

    private String name;

    public User(String id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

위와 같이 `@GeneratedValue` 없이 **직접 ID를 설정**하는 경우,  
Spring Data JPA는 해당 엔티티를 **기존 데이터로 인식할 수 있습니다**.

### **🔹 발생하는 문제**

```java
User user = new User("123", "John Doe");
userRepository.save(user);
```

- `save()`를 호출하면 Spring Data JPA는 **해당 ID("123")가 존재하는지 확인하기 위해 먼저 조회 쿼리를 실행**
- **ID가 없으면 `persist()`를 실행하지만**, ID가 존재한다고 판단하면 **불필요한 `merge()`를 수행**
- **즉, 불필요한 데이터베이스 조회가 발생하며 성능 저하 가능성이 있음**

---

## **📌 3. 해결 방법 - `Persistable` 인터페이스 구현**

직접 ID를 설정하는 경우, **Spring Data JPA가 엔티티의 신규 여부를 정확히 판단할 수 있도록 `Persistable` 인터페이스를 구현**하는 것이 좋습니다.

### **🔹 `Persistable`을 활용한 해결 방법**

```java
import org.springframework.data.domain.Persistable;

import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Transient;

@Entity
public class User implements Persistable<String> {

    @Id
    private String id;
    private String name;

    @Transient // JPA가 인식하지 않도록 설정
    private boolean isNewEntity = false;

    public User(String id, String name) {
        this.id = id;
        this.name = name;
        this.isNewEntity = true; // 새 엔티티임을 표시
    }

    @Override
    public String getId() {
        return id;
    }

    @Override
    public boolean isNew() {
        return isNewEntity; // 새 엔티티 여부를 직접 관리
    }
}
```

✅ **설명**

- `Persistable<T>` 인터페이스를 구현하여 **Spring Data JPA가 `isNew()` 메서드를 호출하도록 유도**
- `isNew()`가 `true`이면 **`persist()`가 실행**되며, `false`이면 `merge()`가 실행됨
- `@Transient` 어노테이션을 사용하여 **JPA가 관리하지 않도록 설정** (`isNewEntity` 필드는 DB에 저장되지 않음)

---

## **📌 4. `isNew()` 내부 동작 방식**

Spring Data JPA에서 `isNew()`는 **엔티티의 ID 값 및 @Version 값을 확인하여 신규 여부를 결정**합니다.  
기본적으로 `JpaMetamodelEntityInformation`을 통해 엔티티의 상태를 확인합니다.

```java
@Override
public boolean isNew(T entity) {

    if(versionAttribute.isEmpty()
          || versionAttribute.map(Attribute::getJavaType).map(Class::isPrimitive).orElse(false)) {
        return super.isNew(entity);
    }

    BeanWrapper wrapper = new DirectFieldAccessFallbackBeanWrapper(entity);

    return versionAttribute.map(it -> wrapper.getPropertyValue(it.getName()) == null).orElse(true);
}
```

✅ **설명**

- `@Version`이 없는 경우, 또는 `@Version`이 primitive 타입이면 **기본 `isNew()`를 호출**
- `@Version`이 wrapper 타입이면 해당 필드가 `null`인지 확인하여 신규 여부를 판단

### **🔹 `AbstractEntityInformation`에서의 동작**

```java
public boolean isNew(T entity) {
    Id id = getId(entity);
    Class<ID> idType = getIdType();

    if (!idType.isPrimitive()) {
        return id == null;
    }

    if (id instanceof Number) {
        return ((Number) id).longValue() == 0L;
    }

    throw new IllegalArgumentException(String.format("Unsupported primitive id type %s", idType));
}
```

✅ **설명**

- `@Version`이 없으면 `@Id` 필드를 확인
- **primitive 타입이 아니면 `null` 여부**, **숫자(Number) 타입이면 `0` 여부**를 확인하여 신규 여부 판단

---

## **📌 5. 정리**

✅ **Spring Data JPA는 `JpaEntityInformation#isNew(T entity)`를 사용하여 엔티티의 신규 여부를 판단**  
✅ **ID를 직접 설정하면 JPA가 기존 엔티티로 오인할 가능성이 있음**  
✅ **불필요한 `SELECT` 및 `merge()`를 방지하기 위해 `Persistable` 인터페이스를 활용할 수 있음**  
✅ **`isNew()`의 내부 동작 방식은 `@Version` 및 `@Id` 필드의 상태를 기반으로 결정됨**

📌 **이러한 내용을 고려하여 ID를 직접 할당할 때 JPA의 동작을 이해하고 최적화하는 것이 중요합니다.** 🚀

---

## 출처

<a href="https://www.maeil-mail.kr/question/27">매일메일 : Spring Data JPA에서 새로운 Entity인지 판단하는 방법은 무엇일까요?</a>
