---
published: true
title: (10분 테코톡) Java 63. Gradle
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-06-13 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Gradle

## 1. Gralde이란?

- 거의 모든 유형의 소프트웨어를 빌드할 수 있을 만큼 **유연한 빌드 자동화 도구**이다.

### 1) 빌드란?

![alt](/assets/images/post/ComputerStudy/1041.png)

- 소스 코드를 실행 가능한 파일로 변환 해주어야하는데, 이것을 **빌드**라고한다.

![alt](/assets/images/post/ComputerStudy/1042.png)

### 2) 빌드 도구의 역할

- 빌드 도구는 코드를 실행 가능한 파일로 만들어주는 과정 및 라이브러리 관리, 테스팅 등을 자동화 하여 수행

### 3) 빌드 도구의 필요성

#### 3-1) 빌드 도구를 사용하지 않을 때의 문제점

1. 반복적인 작업을 수작업으로 진행해야 하므로 비효율적이다.
2. 라이브러리르 직접 다운로드 및 버전 업데이트해야 한다.
3. 프로젝트의 의존성을 파악하기 어렵다.

## 2. 빌드 도구의 역사

### 1) Gradle 등장 전의 빌드 도구

#### 1-1) `<APACHE ANT>`

- 기본적인 컴파일, 패키징, 배포 작업 수행가능
- XML 기반의 스크립트 사용
- 작성에 정해진 규칙이 없어 유연성을 가짐

##### 1) 단점

- 라이브러리 의존관계를 정의하는 구조의 부재
- 정해진 규칙이 없어 유지보수가 어려움

#### 1-2) MAVEN

- 정해진 라이프 사이클에 따라 빌드 진행
- pom.xml 파일 사용
- 라이브러리 의존성 자동 관리 기능 추가

##### 1) 단점

- xml 파일 기반으로 가독성이 좋지 않음
- 상속구조를 이용한 멀티 모듈 구현
- 의존관계가 복잡한 프로젝트에는 부적절

## 3. Gradle 장점 - 호환성 & 유연성

- **Gradle은 Groovy기반의 스크립트 언어이다.**

### 1) 스크립트 언어

- 동적으로 실행 가능하다.
- 추가적인 로직을 작성하고 싶을 때 스크립트 로직을 직접 작성할 수 있다.
- 또는 Gradle이 지원하는 플러그인을 호출할 수도 있다.

### 2) Groovy 기반의 DSL

- Groovy 기반으로, 자바와 유사한 문법 구조를 가지며 Java와 호환된다.
- JVM에서 실행되는 스크립트 언어이다.

## 4. 빌드 스크립트

- build.gradle을 빌드 스크립트라고 한다.

### 1) Plugins

- Plugin이란 특정 작업을 위해 모아놓은 task들의 묶음

![alt](/assets/images/post/ComputerStudy/1043.png)

#### 1-1) 예시) Gradle의 'java' 플러그인

- 자바 플러그인을 추가하면, 다음과 같은 태스크들이 추가되어 수행할 수 있다.

![alt](/assets/images/post/ComputerStudy/1044.png)

### 2) 의존성 관리

- Dependencies(의존성 관리)
- 프로젝트에서 사용하는 라이브러리나 패키지를 '의존성'이라고 한다.
- 프로젝트별로 어떤 의존성을 갖는지 명시해주어야 한다.

![alt](/assets/images/post/ComputerStudy/1045.png)

#### 2-1) 종류 (Dependencies Configuration)

- Implementation: 런타임 + 컴파일 시점 모두에서 사용
- compileOnly: 컴파일 할때만 사용되고 런타임 때에는 미사용
- runtimeOnly : 런타임 때에만 사용
- testImplementation : 테스트할 때에만 사용

- 라이브러리를 추가하는 시점을 설정할 수 있다.
- 특정 시점에 불필요한 특정 라이브러리를 추가한다면 리소스 낭비이다.

### 3) Repositories

![alt](/assets/images/post/ComputerStudy/1046.png)

- Repositories는 라이브러리(모듈)가 저장된 위치를 정의한다.
- 대표적으로 Maven Central(), Jcenter(), Google Android()가 있다.
- 라이브러리의 저장소를 명시해주면 Gradle이 해당 저장소에서 필요한 라이브러리를 가져온다.

## 5. Gradle의 특징

![alt](/assets/images/post/ComputerStudy/1047.png)

### 1) 성능

![alt](/assets/images/post/ComputerStudy/1048.png)

#### 1-1) Build Cache

- 빌드 결과물을 캐싱하여 재사용
- 라이브러리 의존성을 캐시로 저장 후 이전에 다운로드한 라이브러리 재사용

#### 1-2) 점진적 빌드

- 마지막 빌드 호출 이후 변경된 부분만 빌드
- 변경되지 않은 부분은 캐시 결과를 검색해 재사용
- 태스크의 입력, 출력 혹은 변경되지 않은 부분은 빌드하지 않음

#### 1-3) 데몬 프로세스 아용

- 다음 빌드 작업을 위해 백그라운드에서 대기하는 프로세스
- 초기 빌드 이후 빌드 실행시 초기화 작업을 거치지 않음
- 이로 인해 한 번 빌드된 프로젝트는 다음 빌드에서 매우 적은 시간만 소요됨

#### 1-4) 멀티 프로젝트의 필요성

- 관리자 프로젝트, 일반 회원 프로젝트 모두 멤버 클래스를 추가하는 방식이 있지만, 관리가 어렵다는 단점이 있다.
- Gradle을 활용해 공통모듈을 관리할 수 있다.

##### 1) 멀티 프로젝트 빌드 지원

- 멀티 프로젝트란?
- 공통되는 도메인을 사용하는 프로젝트를 하나의 프로젝트로 묶어서 관리하는 것이다.
- Gradle은 각 프로젝트가 공통으로 사용하는 클래스를 모듈로 만들어 독립적인 각 프로젝트에서 사용할 수 있도록 한다.

![alt](/assets/images/post/ComputerStudy/1049.png)

- root 프로젝트 : 공통 모듈 '멤버'를 사용하는 관리자, 일반 회원 프로젝트를 묶는 프로젝트
- 공통 모듈 : 각 프로젝트에서 사용되는 클래스를 하나의 모듈로 저장한다.
- Gradle은 독립적인 두 프로젝트에서 멤버 모듈을 사용할 수 있도록 도와준다.

##### 2) Root 프로젝트 설정

```java
 root > settings.gradle
```

![alt](/assets/images/post/ComputerStudy/1050.png)

##### 3) 하위 프로젝트 설정

```java
 root > build.gradle
```

![alt](/assets/images/post/ComputerStudy/1051.png)

- 프로젝트별 의존성 추가
- 각 프로젝트가 common-module을 사용한다는 것을 명시

##### 4) Root 프로젝트 설정

```java
  root > build.gradle
```

![alt](/assets/images/post/ComputerStudy/1052.png)

- 하위 프로젝트들에 공통 설정 주입

##### 5) Configuration Injection

![alt](/assets/images/post/ComputerStudy/1053.png)

- 필요한 정보를 직접 프로젝트에 주입하는 방식
- 공통되는 정보는 묶어서 주입 가능
- 프로젝트별로 설정을 다르게 주입 가능
- Maven의 상속 구조와 비교했을때 가독성 측면에서 우월

### 2) jar 생성 비활성화

```java
  root > build.gradle
  common-project > build.gradle
```

![alt](/assets/images/post/ComputerStudy/1054.png)

- root 프로젝트와 common-project는 main 없이 라이브러리의 역할을 하는 모듈이기 때문에 실행하지 않는다는 것을 명시해주기 위해  
  bootJar.enabled = false 해준다.

## 6. 정리

### 1) Gradle이란

- 프로그래머가 작성한 코드를 실행 가능한 파일로 변환해주고,
- 라이브러리, 테스트, 배포 등을 자동화하여 관리해주는 빌드 자동화 도구이다.

### 2) Gradle은

- Groovy 기반의 스크립트 언어로서 유연성을 갖는다.
- 성능 측면에서 유리한 빌드 도구이다.
- configuration Injection 방식을 통해 편리한 멀티프로젝트 빌드를 지원한다.

## 출처

<a href="https://www.youtube.com/watch?v=V4knLFDG-ZM">메리의 Gradle</a>
