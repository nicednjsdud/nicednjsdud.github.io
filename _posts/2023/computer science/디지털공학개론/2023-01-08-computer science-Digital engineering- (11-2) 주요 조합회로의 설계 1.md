---
title: (디지털 공학) 11-2 주요 조합회로의 설계 1
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 조합회로의 기본 구조
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,디지털 공학
last_modified_at: "2023-01-08 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 디지털 공학 개론 - 주요 조합회로의 설계 1

## 1. 가산기

### 1) 가산기

- 수치적 데이터들 간의 덧셈을 수행하는 조합 회로

#### (1) 반가산기 (Half adder : HA)

- 두 비트들을 더하고, 합과 올림수를 발생하는 회로

#### (2) 전가산기 (Full adder : FA)

- 세개의 비트들을 더하고, 합과 올림수 비트를 발생하는 회로
- 일반적으로 세개의 입력들 중의 두개는 더해질 비트들이며, 나머지 한 비트는 아래 자리수로부터 올라오는 올림수 비트

### 2) 반 가산기

![alt](/assets/images/post/ComputerStudy/589.png)

#### (1) 반가산기의 덧셈규칙 : 2- 비트 덧셈 규칙

```c
  0 + 0 = 0, 올림수 = 0
  0 + 1 = 1, 올림수 = 0
  1 + 0 = 1, 올림수 = 0
  1 + 1 = 0, 올림수 = 1
```

#### (2) 반가산기의 진리표

![alt](/assets/images/post/ComputerStudy/590.png)

```c
  S = A'B + AB' = A + B
  C = AB
```

![alt](/assets/images/post/ComputerStudy/591.png)

### 3) 전가산기

- 3-비트 덧셈 회로 : 두 입력 비트들 및 올림수 간의 덧셈을 수행

![alt](/assets/images/post/ComputerStudy/592.png)

#### (1) 전가산기의 진리표

![alt](/assets/images/post/ComputerStudy/593.png)

#### (2) 카르노맵으로 간략화

![alt](/assets/images/post/ComputerStudy/594.png)

### 4) 병렬 가산기

- 여러 비트들로 이루어진 2진수들 간의 덧셈을 수행하는 회로
- 4 - 비트 병렬가산기 : 네개의 전가산기(FA)들로 구성

![alt](/assets/images/post/ComputerStudy/595.png)

#### (1) 8, 16, 32 - 비트 벙렬 가산기

- 그 수만큼의 FA들을 같은 방법으로 구성
- 덧셈에 걸리는 시간 ( 각 게이트 지연시간 : 2ns로 가정 )
- 각 FA에서 두 비트 덧셈에 걸리는 시간 = 6ns
- 4-비트 덧셈 시간 = 6ns x 4 = 24ns
- 8-비트 덧셈 시간 = 48ns
- 16-비트 덧셈 시간 = 96ns
- 32-비트 덧셈 시간 = 192ns

## 2. 디코더와 엔코더

### 1) 디코더(Decoder)

- 해독기라고도 부름
- 2진수에 대응되는 10진수(혹은 그 위치)를 가리키는 동작을 한다.
- N-비트 2진수 입력을 받아 2(N승)개의 출력들 중의 하나를 지정해주는 조합회로

![alt](/assets/images/post/ComputerStudy/596.png)

#### (1) 2x4 디코더의 진리표

![alt](/assets/images/post/ComputerStudy/597.png)
