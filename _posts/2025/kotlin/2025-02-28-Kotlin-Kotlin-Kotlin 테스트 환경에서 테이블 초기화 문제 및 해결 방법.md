---
published: true
title: "(Kotlin) 테스트 환경에서 테이블 초기화 문제 및 해결 방법 (삽질 기록)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Kotlin
  - Testing
description: "Kotlin과 Exposed를 사용한 테스트 환경에서 테이블 초기화 문제 해결 방법"
tag: "Kotlin, Testing, Exposed, Database"
article_tag1: "Kotlin"
article_section: "Testing"
meta_keywords: "Kotlin, Testing, Exposed, Database, Spring, Rollback"
last_modified_at: "2025-02-28 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **📌 Kotlin 테스트 환경에서 테이블 초기화 문제 및 해결 방법**

---

## **📌 1. 문제 상황**

Kotlin에서 테스트를 진행할 때, **각 테스트가 겹치지 않도록 테이블을 초기화하는 방법**에 대한 삽질 기록입니다.  
Spring Boot에서는 `@Transactional`과 `@Rollback`을 활용하여 **각 테스트가 독립적으로 실행**되었지만,  
Kotlin (특히 **Exposed + Ktor** 환경)에서는 이러한 기능이 자동으로 제공되지 않았습니다.

## 1) 예) **userServiceTest에 userRepositoryTest 기록이 남아있는 상황**

- 각각 단위테스트는 통과하지만, 빌드시에 테스트가 실패하는 상황

```kotlin
--- userRepositoryTest.class

@BeforeAll
fun setUp() {
    transaction(database) {
        SchemaUtils.create(UserTable)
    }
    userRepository = UserRepository(database)
}

--- userServiceTest.calss

@BeforeAll
fun setUp() {
    transaction(database) {
        SchemaUtils.create(UserTable)
    }
    userRepository = UserRepository(database)
}

@AfterEach
fun tearDown() {
    transaction {
        SchemaUtils.drop(UserTable)   // 기존 테이블 삭제
        SchemaUtils.create(UserTable) // 새로 생성
    }
}

```

---

## **📌 2. 기존 Spring Boot 환경에서는?**

Spring Boot에서는 다음과 같은 방식으로 **각 테스트가 실행될 때마다 DB 상태를 초기화**할 수 있었습니다.

```java
@Transactional
@Rollback
public void someTest() {
    // 테스트 실행 후, 자동으로 롤백됨
}
```

📌 하지만 **Kotlin에서는 이러한 롤백 개념이 없고**,  
테스트 실행 후 **테이블이 유지되므로 데이터가 남아있음** 😱

---

## **📌 3. Kotlin에서는 어떻게 해결할까?**

### **1️⃣ 해결 방법: `@BeforeAll` & `@AfterEach` 활용**

각 테스트(+ 클래스)마다 **테이블을 명확하게 초기화**하는 방법을 사용해야 합니다.

```kotlin
@BeforeAll
fun setUp() {
    transaction(database) {
        SchemaUtils.create(UserTable) // 테이블 생성
    }
    userRepository = UserRepository(database)
}

@AfterEach
fun tearDown() {
    transaction {
        SchemaUtils.drop(UserTable)   // 기존 테이블 삭제
        SchemaUtils.create(UserTable) // 새로 생성
    }
}
```

---

## **📌 4. 각 코드 설명**

### **🔹 `@BeforeAll` - 테스트 시작 전 테이블 생성**

```kotlin
@BeforeAll
fun setUp() {
    transaction(database) {
        SchemaUtils.create(UserTable)
    }
    userRepository = UserRepository(database)
}
```

- **테스트 실행 전에 테이블을 생성**합니다.
- `UserRepository`를 초기화하여 사용할 수 있도록 설정합니다.

### **🔹 `@AfterEach` - 각 테스트 후 테이블 초기화**

```kotlin
@AfterEach
fun tearDown() {
    transaction {
        SchemaUtils.drop(UserTable)   // 기존 테이블 삭제
        SchemaUtils.create(UserTable) // 새로 생성
    }
}
```

- 각 테스트 실행 후 **기존 테이블을 삭제하고 다시 생성**하여 초기화합니다.
- 이를 통해 **이전 테스트의 데이터가 남지 않도록 보장**할 수 있습니다.

---

## **📌 5. 결론**

✅ **Spring Boot에서는 `@Transactional` + `@Rollback`을 활용했지만**,  
✅ **Kotlin + Exposed에서는 `@BeforeAll`과 `@AfterEach`를 활용해야 함**  
✅ **테스트 실행 후 데이터를 남기지 않으려면 `drop()` 활용**

---

**💡 더 나은 방법이 있다면 댓글로 공유해주세요! 😊**
