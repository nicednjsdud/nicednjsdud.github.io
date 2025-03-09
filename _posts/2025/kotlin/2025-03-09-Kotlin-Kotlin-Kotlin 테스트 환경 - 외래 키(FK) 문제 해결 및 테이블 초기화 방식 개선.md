---
published: true
title: "🔍 Kotlin 테스트 환경 - 외래 키(FK) 문제 해결 및 테이블 초기화 방식 개선 (삽질 기록)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Kotlin
  - Testing
  - Exposed
description: "Kotlin 테스트 환경에서 FK(외래 키) 문제로 인해 발생한 오류를 해결하고 테이블 초기화 방식을 개선한 방법"
tag: "Kotlin, Testing, Exposed, Database, FK 문제 해결"
article_tag1: "Kotlin"
article_section: "Testing"
meta_keywords: "Kotlin, Testing, Exposed, Database, Spring, 외래 키, FK 문제 해결"
last_modified_at: "2025-03-09 16:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **🔍 Kotlin 테스트 환경 - 외래 키(FK) 문제 해결 및 테이블 초기화 방식 개선**

---

## **📌 1. 문제 상황**

### **🔹 기존 테스트 환경에서 발생한 FK 문제**

- 기존 코드

<a href="https://nicednjsdud.github.io/kotlin/testing/Kotlin-Kotlin-Kotlin-%ED%85%8C%EC%8A%A4%ED%8A%B8-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%B4%88%EA%B8%B0%ED%99%94-%EB%AC%B8%EC%A0%9C-%EB%B0%8F-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95/">(Kotlin) 테스트 환경에서 테이블 초기화 문제 및 해결 방법 (삽질 기록)</a>

- `mapleServiceTest`를 실행할 때 **`UserTable`이 외래 키(FK)로 설정되면서 삭제 순서 문제 발생**
- `SchemaUtils.drop(UserTable)`을 실행하려고 할 때, **FK 제약 조건 때문에 삭제되지 않는 문제 발생**
- 이를 해결하기 위해 **테스트 데이터 정리 방식 변경 필요**

---

## **📌 2. 기존 방식의 문제점**

### **🔹 기존 `@AfterEach`에서 `SchemaUtils.drop()`을 사용했던 문제**

```kotlin
@AfterEach
fun tearDown() {
    transaction {
        SchemaUtils.drop(UserTable) // FK 제약 조건 때문에 실패 가능
    }
}
```

✅ **문제 발생 이유**

- `UserTable`이 `MapleUserTable`과 FK 관계를 맺고 있음
- `drop(UserTable)`을 하려면 FK 관계가 해제되어야 하는데, **기본적으로 FK 설정이 활성화되어 있어 삭제 불가능**
- 즉, **참조하는 테이블(`MapleUserTable`)을 먼저 삭제해야 FK 문제를 방지할 수 있음**

---

## **📌 3. 해결 방법 - `deleteAll()`을 활용한 데이터 초기화**

### **🔹 FK 문제를 해결하는 새로운 테스트 환경 설정**

```kotlin
@BeforeAll
fun setUp() {
    transaction(database) {
        SchemaUtils.create(UserTable, MapleUserTable)
    }
    userRepository = UserRepository(database)
    mapleRepository = MapleRepository(database)
    mapleService = MapleService(config, client, mapleRepository, userRepository)
}

@AfterEach
fun tearDown() {
    transaction(database) {
        MapleUserTable.deleteAll() // FK를 가진 테이블 데이터를 먼저 삭제
        UserTable.deleteAll() // 이후 FK 대상 테이블 데이터 삭제
    }
}

@AfterAll
fun tearDownAll() {
    transaction {
        SchemaUtils.drop(MapleUserTable) // FK를 가진 테이블을 먼저 삭제
        SchemaUtils.drop(UserTable) // 이후 FK 대상 테이블 삭제
    }
}
```

---

## **📌 4. 핵심 변경 사항 및 이유**

### **🔹 1️⃣ `deleteAll()`을 사용하여 데이터만 삭제**

```kotlin
@AfterEach
fun tearDown() {
    transaction(database) {
        MapleUserTable.deleteAll() // FK를 가진 테이블 데이터를 먼저 삭제
        UserTable.deleteAll() // 이후 FK 대상 테이블 데이터 삭제
    }
}
```

✅ **이유**

- `deleteAll()`은 **테이블을 삭제하는 것이 아니라, 테이블의 모든 데이터를 삭제**
- 즉, FK 관계가 남아 있어도 데이터를 삭제하는 데 문제가 없음
- **테스트 실행 시 기존 데이터를 완전히 제거하면서도, 테이블 자체는 유지**

---

### **🔹 2️⃣ `@AfterAll`에서 `SchemaUtils.drop()`을 호출**

```kotlin
@AfterAll
fun tearDownAll() {
    transaction {
        SchemaUtils.drop(MapleUserTable) // FK를 가진 테이블을 먼저 삭제
        SchemaUtils.drop(UserTable) // 이후 FK 대상 테이블 삭제
    }
}
```

✅ **이유**

- `drop()`은 **테이블 자체를 삭제**하는데, FK가 있는 경우 먼저 참조하는 테이블을 삭제해야 함
- **`MapleUserTable`이 `UserTable`을 참조하므로, 먼저 삭제한 후 `UserTable`을 삭제해야 오류 방지 가능**

---

## **📌 5. `deleteAll()` vs `drop()` 차이점**

| 기능         | `deleteAll()`                            | `drop()`                                        |
| ------------ | ---------------------------------------- | ----------------------------------------------- |
| 동작 방식    | 테이블 내 모든 데이터 삭제 (테이블 유지) | 테이블 자체를 삭제                              |
| FK 관계 문제 | FK가 있어도 사용 가능                    | FK 관계가 있으면 오류 발생 가능                 |
| 성능         | 빠름 (데이터만 삭제)                     | 상대적으로 느림 (테이블 삭제 후 다시 생성 필요) |
| 사용 시점    | 개별 테스트 실행 후 데이터 초기화 시     | 테스트 종료 후 전체 테이블 삭제 시              |

---

## **📌 6. 결론**

🚀 **FK 제약 조건이 있는 경우 `SchemaUtils.drop()` 대신 `deleteAll()`을 활용하여 데이터만 삭제하는 것이 더 안정적**  
🚀 **테스트 실행 중에는 `deleteAll()`을 사용하여 데이터 초기화, 테스트 종료 후 `drop()`을 활용하여 테이블 삭제**  
🚀 **FK 제약 조건을 고려하여 테이블 삭제 순서를 조정해야 문제 발생을 방지할 수 있음**

📌 **이제 FK 문제로 인한 테스트 실패 없이 안정적으로 데이터 초기화 가능!** ✅

## 개선 코드

<a href="https://github.com/nicednjsdud/M-rich_backend/commit/4cc2f29ba5452e62d2f51844a918d5c75a1a4192">
깃허브 주소</a>
