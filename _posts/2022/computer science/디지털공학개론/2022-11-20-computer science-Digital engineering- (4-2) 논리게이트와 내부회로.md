---
title: (디지털 공학) 4-2 논리게이트와 내부회로
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 논리게이트와 내부회로
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

# 디지털 공학 개론 - 논리게이트의 내부회로

## 1. 논리게이트에 구현되는 트랜지스터와 부품의 종류

### 1) 논리게이트의 구성

- 논리게이트는 전자회로 소자들(트랜지스터, 다이오드,저항, 등)을 이용하여 반도체 칩에 제조

#### (1) 구현에 사용되는 소자들에 따른 계열 분류

- RTL(Resistor-Transistor Logic)
- DTL(Diode-Transistor Logic)
- TTL(Transistor-Transistor Logic)
- MOSFET(Metal-Oxide Semiconducotr Field-Effect Transistor)
- CMOS(Complementary Metal-Oxide Semiconductor)

### 2) 트랜지스터(transistor)

#### (1) 종류

- NPN 트랜지스터
- PNP 트랜지스터

#### (2) 입출력단자

- 콜렉터(collector: C) - 전원공급
- 에미터(emitter: E) - 접지
- 베이스(base: B) - 스위칭

### 3) NPN 트랜지스터의 그래픽 기호 및 스위칭 회로

![alt](/assets/images/post/ComputerStudy/89.png)

## 2. RTL과 DTL, TTL 게이트 화로

- RTL,DTL 반도체 개발 초기에 사용 - 현재 거의 사용 X

### 1) RTL 스위칭 회로

#### (1) RTL 스위칭 회로

- 저항(resistor) 및 NPN트랜지스터로 구현

![alt](/assets/images/post/ComputerStudy/90.png)

- 인버터(NOR 게이트) 기능 수행

#### (2) NAND 게이트의 RTL 구현

- 두개의 NPN 트랜지스터를 직렬로 접속하여 구성
- 입력단 트랜지스터 회로 추가 하면 3 - 입력 NAND 게이트
- 출력단에 스위칭 회로 접속하면 - AND 게이트 **(NAND + NOT) -> AND**

![alt](/assets/images/post/ComputerStudy/91.png)

#### (3) NAND 게이트 화로

![alt](/assets/images/post/ComputerStudy/92.png)

#### (4) NOR 게이트의 RTL 구현

- 두개의 NPN 트랜지스터를 벙렬로 접속하여 구성
- 입력단 트랜지스터 회로 추가하면 3 - 입력 NOR 게이트
- 출력단에 스위칭 회로 접속 - OR 게이트 **(NOR + NOT) -> OR**

![alt](/assets/images/post/ComputerStudy/93.png)

#### (5) NOR 게이트 화로

![alt](/assets/images/post/ComputerStudy/94.png)

### 2) DTL 게이트 회로

- 다이오드(diode)와 트랜지스터를 이용하여 구현

#### (1) 다이오드의 특성

- 애노드(anode: A)**(+극)**와 캐소드(cathode: C)**(-극)**로 구성
- 애노드와 캐소드 간의 전압(V ac)이 정방향(애노트 측의 전압이 더 높음)으로 걸리면  
  전류가 흐름(전도상태)
- Vac가 0V 혹은 역방향(애노드 측 전압이 더 낮음)으로 걸리면 전류가 흐르지 못함(차단 상태)

#### (2) 다이오드 그래픽 회로

![alt](/assets/images/post/ComputerStudy/95.png)

#### (3) DTL NAND 게이트 회로

![alt](/assets/images/post/ComputerStudy/96.png)
![alt](/assets/images/post/ComputerStudy/97.png)

### 3) TTL 게이트 회로

- 회로 안정성 향상을 위하여 트랜지스터들만으로 회로 구현
- 소규모 반도체 IC(SSI) 칩으로 제조

![alt](/assets/images/post/ComputerStudy/98.png)

#### (1) 표준 TTL 게이트 IC칩의 특성

- 유형에 따른 칩 번호, 전력 소모량, 속도

##### ex)

- NAND 게이트 - 7400
- AND 게이트 - 7408
- OR 게이트 - 7432

![alt](/assets/images/post/ComputerStudy/99.png)
