---
title: (디지털 공학) 5-1 부울대수의 기본 개념
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 부울대수의 기본 개념
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,디지털 공학
last_modified_at: "2022-11-23 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 디지털 공학 개론 - 부울대수의 기본 개념

## 1. 부울대수란?

### 1) 부울 대수(Boolean Algebra)

- George Boole이 논리적 프로세스들을 표현하기 위하여 개발한 대수학
- 디지털 논리회로의 분석과 설계의 기본이 되는 수학

### 2) 부울 대수에 근거하여 표현되는 부울 함수의 구성 요소들

![alt](/assets/images/post/ComputerStudy/160.png)

#### (1) 부울 함수의 예

```c
  F = A + B'C
      A,B,C : 입력 변수들
      F : 출력 변수
```

#### (2) 논리 회로 구현

![alt](/assets/images/post/ComputerStudy/161.png)

## 2. 부울연산의 표현

### 1) 부울 보수(Boolean complement)

```c
  A' 혹은 A (A = 1 -> A' = 0, A = 0 -> A' = 1)
```

- `A프라임`으로 읽기로 함
- 인버터로 구현 (F=A')

![alt](/assets/images/post/ComputerStudy/162.png)

### 2) 부울 덧셈(Boolean addition)

- OR 게이트로 구현

#### 부울 덧셈의 규칙

```c
  0 + 0 = 0
  0 + 1 = 1
  1 + 0 = 1
  1 + 1 = 1
```

#### (1) 입력 변수의 수에 따른 함수의 표현

- 2-변수 OR 함수 : F2 = A + B
- 3-변수 OR 함수 : F3 = A + B + C
- 4-변수 OR 함수 : F4 = A + B + C + D

![alt](/assets/images/post/ComputerStudy/163.png)

### 3) 부울 곱셈(Boolean multiplication)

- AND 게이트로 구현

#### 부울 곱셈의 규칙

```c
  0 * 0 = 0
  0 * 1 = 0
  1 * 0 = 0
  1 * 1 = 1
```

#### (1) 입력 변수의 수에 따른 함수의 표현

- 2-변수 AND 함수 : F2 = AB
- 3-변수 AND 함수 : F3 = ABC
- 4-변수 AND 함수 : F4 = ABCD

![alt](/assets/images/post/ComputerStudy/164.png)

### 4) 기타 부울 함수들

#### (1) NOR 함수 : F = (A+B)'

- (A+B = OR)
- 그뒤에 NOT을 붙임 (인버터)

![alt](/assets/images/post/ComputerStudy/165.png)

#### (2) NAND 함수 : F = (AB)'

- (AB = AND)
- 그뒤에 NOT을 붙임 (인버터)

![alt](/assets/images/post/ComputerStudy/166.png)
