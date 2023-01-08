---
title: (디지털 공학) 11-1 조합회로의 기본 구조
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

# 디지털 공학 개론 - 조합회로의 기본 구조

## 1. 조합회로와 순차회로

### 1) 동작 특성에 따른 논리회로의 분류

#### (1) 조합회로

- 현재의 입력값들만 이용하여 출력값을 결정하는 회로로서, 입력 신호들을 받는 즉시 그들을 조합하여 최종 출력을 발생

#### (2) 순차회로

- 현재의 입력들 뿐 아니라 과거의 입력 혹은 출력값도 함께 고려하여 현재의 출력 값을 결정하는 회로로서, 조합회로에  
  기억소자를 추가하여 구성

## 2. 조합회로의 기본 구조 및 분석, 설계

### 1) 조합회로의 기본 구조

- `[비교]`순차회로는 **기억소자(플롭-플롭)**들과 게이트들을 이용하여 구현

![alt](/assets/images/post/ComputerStudy/578.png)

#### (1) 예 F = AB + CD를 구현한 4입력 1-출력 조합회로

![alt](/assets/images/post/ComputerStudy/579.png)

- 동작 지연 시간 = 5ns X 2 = 10ns
- (각 게이트 지연이 5ns일 경우)

#### (2) 3-입력 2-출력 조합 회로

![alt](/assets/images/post/ComputerStudy/580.png)

- 동작 지연 시간 = 5ns X 3 = 15ns
- (각 게이트 지연이 5ns일 경우)

### 2) 조합 회로의 분석 방법

- 부울 함수를 이용한 분석
- 진리표를 이용한 분석
- 입출력 신호 파형을 이용한 분석

#### (1) 부울 함수를 이용한 분석

- 회로의 게이트 출력들에 변수를 할당
  - 이때 게이트 출력에 대한 변수명은 분석을 위하여 임시적으로 배정한 것
  - 조합회로의 입력들 및 최종 출력 변수명과는 다른 유형의 기호들을 이용하는 것이 혼동을 방지
- 각 게이트의 입력 변수들을 이용하여 게이트 출력에 대한 부울함수를 구한다,
- 두번째 과정을 최종 출력에 도달할 때까지 반복
- 임시 변수들에 대한 표현을 대입함으로써, 최종 출력 변수에 대한 완전한 부울 함수를 구함

##### (1-1) 조합회로의 분석의 예

![alt](/assets/images/post/ComputerStudy/581.png)

##### (1-2) 부울 함수의 유도

```c
   x = ABC
   y = (B+C)
   z = (AB+BC)` = (A' + B')(B' + C')
     = A'B + A'C' + B' + B'C' = B' + A'C'
   T = yz = (B+C)(B' + A'C') = A'BC + B'C

최종 출력 (F) : F = x + T
                = ABC + A'BC' + B'C
```

#### (2) 진리표를 이용한 분석

![alt](/assets/images/post/ComputerStudy/582.png)
![alt](/assets/images/post/ComputerStudy/583.png)

- 각 게이트의 출력 값을 단계적으로 구하여 최종 출력 (F)를 결정

#### (3) 입출력 신호 파형을 이용한 분석

- 임의의 입력 신호들이 회로로 연속적으로 들어올 때 출력 파형들이 어떻게 생성되는지 확인함으로써  
  회로의 기능과 동작의 특성을 파악하는 방법

```c
   예) F = [(A+B)C]` = A`B` + C`
```

- 중간 결과 파형을 단계적으로 구하여 최종 파형을 찾음

![alt](/assets/images/post/ComputerStudy/584.png)
![alt](/assets/images/post/ComputerStudy/585.png)

### 3) 조합회로의 설계 방법

#### (1) 조합 회로 설계의 목표

- 최소 개수의 게이트 이용 구현 -> 최저 비용
- 간단한 구조 -> 최소 공간
- 적은 수의 단계를 거치도록 설계 -> 고속

#### (2) 설계 절차

- 구현할 기능 표현
- 입력 및 출력 변수 결정
- 입출력 관계를 분석하여 진리표 작성
- 카노프 맵을 이용하여 간략화 된 부울 함수 유도
- 회로 구성

#### (3) 다수결 회로

##### (3-1) 회로 기능 정의

- 세명의 위원들이 스위치를 한 개씩 배당 받아서 의사 결정 과정에서 찬성한다면 투표 스위치를 누르고 (출력 =1),  
  반대한다면 누르지 않는다. (출력 = 0)
- 만약 두개이상의 스위치가 눌러진다면 출력 램프가 켜진다.

##### (3-2) 변수 결정

- 세명의 위원들에 배정된 투표 스위치들을 통하여 회로로 들어오는 입력 신호들에 2진 변수 A,B,C를 각각 배정
- 그리고 출력 램프의 on/off를 구동하는 출력변수로는 F를 배정

##### (3-3) 진리표 작성

![alt](/assets/images/post/ComputerStudy/586.png)

```c
   F = A'BC + AB'C + ABC' + ABC
```

##### (3-4) 부울 함수의 간략화

![alt](/assets/images/post/ComputerStudy/587.png)

##### (3-5) 다수결 회로의 구성도

![alt](/assets/images/post/ComputerStudy/588.png)
