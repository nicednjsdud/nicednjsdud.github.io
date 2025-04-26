---
published: true
title: "💡 Ktor에서 HoconApplicationConfig로 YAML 설정이 안될 때 해결법 (.conf 도입) (삽질기록)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Kotlin
description: "Ktor에서 application.yaml 파일을 HoconApplicationConfig로 읽지 못할 때의 원인과 .conf(HOCON) 포맷을 활용한 해결 방법"
tag: "Kotlin, Ktor, Config, HOCON, YAML"
article_tag1: "Kotlin"
article_section: "Backend"
meta_keywords: "Ktor, Kotlin, ConfigFactory, Hocon, YAML, .conf 설정"
last_modified_at: "2025-03-31 17:30:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 💡 Ktor에서 HoconApplicationConfig로 YAML 설정이 안될 때 해결법 (.conf 도입)

---

## 🧩 발생 상황

Ktor 프로젝트에서 설정 정보를 `application.yaml`에 작성하고 아래처럼 불러오려 했습니다.

```kotlin
val config = HoconApplicationConfig(ConfigFactory.load("application.yaml"))
```

하지만 테스트 환경이나 커스텀 런타임 환경에서 다음과 같은 오류가 발생합니다:

```
Unresolved substitution
Unresolved reference
Missing configuration for 'jwt.issuer'
```

---

## 📌 원인 분석

```diff
ConfigFactory.load("application.yaml")
```

- ❌ **`application.yaml`은 기본 지원하지 않음**
- ✅ `ConfigFactory`는 **`.conf`, `.json`, `.properties`, `.env`** 등만 직접 파싱 가능
- `.yaml`은 **Typesafe Config 라이브러리(HOCON)**에서 **직접 파싱하지 않음**
- 별도의 YAML 파서를 붙이지 않는 이상, YAML은 읽히지 않음

---

## 🔧 해결 방법: .yaml → .conf 전환

### 🔁 기존 `.yaml` 설정 예시

```yaml
# application.yaml
jwt:
  secret: "secret-key"
  issuer: "issuer-value"
```

### ✅ 변환된 `.conf` 설정

```hocon
# application-test.conf
jwt {
  secret = "secret-key"
  issuer = "issuer-value"
}
```

### 💡 변경 후 코드

```kotlin
val config = HoconApplicationConfig(ConfigFactory.load("application-test.conf"))
```

✅ `.conf`는 **HOCON 포맷**으로, `.yaml`보다 더 유연하고 **include, reference** 등도 지원합니다.

---

## 🧪 테스트 환경에서의 활용 예시

```kotlin
class AuthServiceTest {

    private val config = HoconApplicationConfig(ConfigFactory.load("application-test.conf"))

    private val database = DatabaseFactory.init(config)
    private val jwtConfig = JwtConfig.init(config) // custom config
    private val authService = AuthService(repository, jwtConfig)

    // ...테스트 코드 작성
}
```

### ✅ 팁

- 테스트용 `.conf` 파일을 분리하여 환경에 맞는 설정만 따로 관리할 수 있음
- 여러 환경별 설정을 `include`로 나눠도 가능

---

## 🧠 정리

| 항목   | 내용                                                                 |
| ------ | -------------------------------------------------------------------- |
| 문제   | `application.yaml`을 `HoconApplicationConfig`로 로드하려 했지만 실패 |
| 원인   | Typesafe Config는 `.yaml` 포맷을 기본 지원하지 않음                  |
| 해결책 | `.yaml` → `.conf` 변환 후 `ConfigFactory.load()`로 불러오기          |
| 장점   | `.conf(HOCON)`은 유연하며, include 및 변수 치환 기능도 제공          |

---

## ✅ 결론

- Spring과 다르게 **Ktor는 설정 로딩 시 `.yaml` 지원이 제한적**입니다.
- Kotlin/Ktor 환경에서는 가능하면 `.conf` 포맷을 사용하는 것이 **더 안정적이고 유연**합니다.
- `.conf`는 문법도 직관적이며 `include`, `fallback`, `substitution` 등을 지원해 **환경 구성에 매우 강력**합니다.

---

📌 Ktor 테스트에서 설정이 제대로 안 읽힌다면, **YAML이 아닌 `.conf` 파일을 쓰는 습관**을 들이자! 💪

## 수정된 코드

<a href="https://github.com/nicednjsdud/M-rich_backend/commit/0d6e66e7f89ccdfdb4cfefd363df49ec78cfe4ab">
refactor : issue 1 해결
</a>
