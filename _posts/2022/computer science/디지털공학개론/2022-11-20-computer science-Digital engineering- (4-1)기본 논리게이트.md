---
title: (디지털 공학) 4-1 기본 논리게이트
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 사용자 관리
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,디지털 공학
last_modified_at: "2022-11-20 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 디지털 공학 개론 - 기본 논리게이트

## 1. AND, OR, NOT 게이트

![alt](/assets/images/post/ComputerStudy/73.png)

### 1) AND 게이트

- 두 개 혹은 그 이상의 입력 신호들에 대하여 AND 연산을 수행하고 결과 신호를 출력하는 게이트
- 두 입력 파형들에 대한 AND 게이트의 출력 파형

![alt](/assets/images/post/ComputerStudy/74.png)

#### (1) 다중 입력 AND 게이트

- AND 게이트의 동작은 3개 혹은 그 이상의 입력신호에서도 동일한 동작을 수행함.

![alt](/assets/images/post/ComputerStudy/75.png)

### 2) OR 게이트

- 두 개 혹은 그이상의 입력 신호들에 대하여 OR 연산을 수행하고 결과 신호를 출력하는 게이트
- 두 입력 파형들에 대한 OR 게이트의 출력 파형

![alt](/assets/images/post/ComputerStudy/76.png)

#### (2) 다중 입력 OR 게이트

- 3개 혹은 그 이상의 입력에 대해서도 같은 결과를 출력해 냄

![alt](/assets/images/post/ComputerStudy/77.png)

### 3) NOT 게이트 (인버터)

- 입력 신호의 반전(invert)된 신호를 출력하는 게이트
- 입력 파형에 대한 NOT 게이트의 출력

![alt](/assets/images/post/ComputerStudy/78.png)

## 2. NAND 와 NOR게이트, XOR게이트, XNOR게이트

### 1) NAND 게이트

- AND 게이트와 반대되는 출력을 발생하는 게이트
- 내부회로는 **AND 게이트보다 더 간단**하다.

![alt](/assets/images/post/ComputerStudy/79.png)

#### NAND 게이트의 입출력 파형

![alt](/assets/images/post/ComputerStudy/80.png)

#### (1) NAND게이트의 재구성

- NAND 게이트를 이용하여 다른 게이트 구성가능
- 만능 게이트(universal gate)라고도 부름

![alt](/assets/images/post/ComputerStudy/81.png)

### 2) NOR 게이트

- OR 게이트와 반대되는 출력을 발생하는 게이트
- 내부 회로는 OR게이트 보다 더 간단

![alt](/assets/images/post/ComputerStudy/82.png)

#### NOR 게이트의 입출력 파형

![alt](/assets/images/post/ComputerStudy/83.png)

#### (1) NOR게이트의 재구성

- NOR 게이트를 이용하여 다른 게이트 구성 가능
- 만능 게이트(universal gate)라고도 부름

![alt](/assets/images/post/ComputerStudy/84.png)

### 3) XOR게이트 (Exclusive - OR게이트)

- 두 입력이 서로 다른 값을 가지면, 1을 출력
- 두 입력이 같은 값을 가지면, 0을 출력

![alt](/assets/images/post/ComputerStudy/85.png)

#### XOR 게이트의 입출력 파형

![alt](/assets/images/post/ComputerStudy/86.png)

### 4) XNOR 게이트 (Excelusive - NOR 게이트)

- 두 입력이 값은 값을 가지면, 1을 출력
- 두 입력이 서로 다른 값을 가지면, 0을 출력

![alt](/assets/images/post/ComputerStudy/87.png)

#### XNOR 게이트의 입출력 파형

![alt](/assets/images/post/ComputerStudy/88.png)
