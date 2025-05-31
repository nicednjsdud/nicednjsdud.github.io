---
published: true
title: "URI, URL, URN의 차이점 완벽 정리"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
description: "URI, URL, URN의 차이점이 헷갈리셨나요? 각각의 개념과 예제를 통해 확실하게 정리해드립니다."
tag: [URI, URL, URN, 인터넷 식별자, 백엔드 개념]
article_section: "Web"
meta_keywords: "URI, URL, URN, 웹 주소, 식별자, 백엔드 지식"
last_modified_at: "2025-05-31 10:00:00 +0900"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🌐 URI, URL, URN의 차이점

URI, URL, URN은 웹 개발과 네트워크 분야에서 자주 등장하는 용어입니다. 이들이 어떻게 다른지, 그리고 각각 어떤 역할을 하는지 쉽게 정리해보겠습니다.

---

## 🔑 1. URI란?

**URI (Uniform Resource Identifier)** 는 웹 상의 **자원을 식별하는 고유한 문자열**입니다.  
URI는 **URL**과 **URN**을 포함하는 **상위 개념**입니다.

```
URI = URL + URN
```

---

## 🌍 2. URL이란?

**URL (Uniform Resource Locator)** 은 URI의 하위 개념 중 하나로,  
**자원이 어디에 있는지**를 알려주는 주소입니다.

- **위치 기반 식별자**
- **접근 방법 (프로토콜) 포함**

### ✅ 예시

```
https://www.example.com/index.html
```

- `https`: 프로토콜
- `www.example.com`: 호스트
- `/index.html`: 자원의 경로

---

## 🧾 3. URN이란?

**URN (Uniform Resource Name)** 은 **자원의 이름**을 식별합니다.  
**자원의 위치와 무관**하게 **영구적인 식별자** 역할을 합니다.

- **이름 기반 식별자**
- **위치 정보 없음**

### ✅ 예시

```
urn:isbn:0451450523
```

- `isbn:0451450523` → 특정 책의 ISBN 번호

---

## 📌 표로 정리해보기

| 항목           | URI                                            | URL                   | URN                   |
| -------------- | ---------------------------------------------- | --------------------- | --------------------- |
| 의미           | 자원 식별자                                    | 자원의 위치           | 자원의 이름           |
| 포함 관계      | ✅ 상위 개념                                   | ✅ URI의 하위         | ✅ URI의 하위         |
| 자원 위치 제공 | ❌ (필수 아님)                                 | ✅                    | ❌                    |
| 자원 이름 제공 | ❌ (필수 아님)                                 | ❌                    | ✅                    |
| 예시           | `urn:isbn:0451450523`<br>`https://example.com` | `https://example.com` | `urn:isbn:0451450523` |

---

## ✅ 마무리 요약

- **URI**는 통합 개념으로 **식별**을 위한 모든 표현을 포함합니다.
- **URL**은 자원의 **위치를 알려주는 주소**입니다.
- **URN**은 자원의 **영구적인 이름**입니다.

URL과 URN 모두 URI의 한 형태라는 점만 기억해도 개념 정리에 큰 도움이 됩니다!
