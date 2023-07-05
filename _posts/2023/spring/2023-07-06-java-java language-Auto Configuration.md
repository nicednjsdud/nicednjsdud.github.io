---
published: true
title: (10분 테크톡) (Spring) 18. Servlet vs Spring
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
last_modified_at: "2023-07-06 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Auto Configuration

## 목차

1. Auto Configuration?
2. @SpringBootApplication부터 따라가보기
3. Annotation 살펴보기
4. DataSourceAutoConfiguration 살펴보기
5. 왜 학습해야 할까?

## 1. Auto Configurtation

- 필요한 Bean을 자동으로 구성하는 기능

## 2. @SpringBootApplication부터 따라가보기

### 순서

1. @SpringBootApplication
2. @EnableAutoConfiguration
3. @Import & ImportSelector
4. AutoConfigurationImportSelector
5. AutoConfiguration.imports

### 1) @SpringBootApplication

- Configuration, @EnableAutoConfiguration, @ComponentScan이 결합된 Annotation
- ApplicationContext를 구성하는데 필요한 메타데이터 제공

![alt](/assets/images/post/ComputerStudy/1059.png)

### 2) @EnableAutoConfiguration

- @AutoConfiguration Annotation이 명시된 모든 클래스 스캔

![alt](/assets/images/post/ComputerStudy/1060.png)

### 3) @Import & ImportSelector

- @Import : Import할 하나 이상의 대상 지정
- ImportSelector : 등록할 대상을 동적으로 구성 가능

### 4) AutoConfigurationImportSelector

- 특정 조건에 따라 @AutoConfiguration Class를 동적으로 import 하기 위한 클래스

### 5) AutoConfiguration.imports

![alt](/assets/images/post/ComputerStudy/1061.png)

- 애플리케이션 한경에 따라 전달받은 후보들을 필터링

## 3. Annotation 살펴보기

### 순서

1. @AutoConfiguration : AutoConfiguration Class 명시 & 순서 제어
2. Condition & @Conditional : 조건에 따라 적용할지 안할지
3. @ConditionOn\* : 손쉽게 사용하기
4. @ConfigurationProperties : 설정을 자바 객체로 Binding
5. @EnableConfigurationProperties : Binding한 자바 객체 주입

### 1) @AutoConfiguration

- 스프링 부트에서 Auto Configuration으로 처리될 수 있는 후보를 명시하는 역할
- before, after 속성을 통해 Auto Configuration시 처리 순서를 제어할 수 있음

### 2) Condition & @Conditional

![alt](/assets/images/post/ComputerStudy/1062.png)

- 해당빈이 등록이 될지 안될지를 판단

![alt](/assets/images/post/ComputerStudy/1063.png)

- Condition 인터페이스를 사용하기위해 필요
- 여러개의 Condition을 등록할 수 있음
- 모든 Condition이 true을 반환해야 해당 빈이 등록된다고 볼수 있음

### 3) @ConditionalOn\*

- **Spring Boot : 자주 쓰는 Condition 구현체들을 @Conditional(구현체)로 미리 구현해 제공**
- Spring : 특정 조건이 필요할 때 마다 Condition 인터페이스 구현 필요

####

- @ConditionalOnBean
- @ConditionalOnMissingBean
- @ConditionalOnClass
- @ConditionalOnMissingClass
- @ConditionalOnProperty
- @ConditionalOnSingleCandidate

### 4) @ConfigurationProperties

- 외부 설정(외부 파일 등)을 Java 객체에 binding하기 위한 Annotation

![alt](/assets/images/post/ComputerStudy/1064.png)

## 4. DataSourceAutoConfiguration 살펴보기

![alt](/assets/images/post/ComputerStudy/1065.png)

- @AutoConfiguration : AutoConfiguration Class 명시 & 순서 제어
- @ConditionalOn\* : 조건에 따라 적용할지 안할지
- @EnableConfigurationProperties : Binding한 자바 객체 주입
- @ConfigurationProperties : 설정을 자바 객체로 Binding

## 5. 왜 학습해야 할까

1. 효율적인 Bean Customizing
2. Bean Customizing 시 발생할 수 있는 문제 대응

## 출처

<a href="https://www.youtube.com/watch?v=TSCHTPZ3PSQ">지토의 Auto Configuration</a>
