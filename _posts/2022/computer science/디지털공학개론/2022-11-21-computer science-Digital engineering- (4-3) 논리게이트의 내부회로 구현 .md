---
title: (디지털 공학) 4-3 논리게이트의 내부회로 구현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 논리게이트의 내부회로 구현
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

# 디지털 공학 개론 - 논리게이트의 내부회로 구현

## 1. MOS 게이트 회로

- 전계효과 트랜지스터 (field-effect transistor: FET) 이용
- JFET - 선형회로(아날로그 회로)에 주로 사용
- MOSFET - 디지털 게이트 회로 구현에 사용

### 1) MOSFET(Metal-Oxide Silicon FET)

- 고밀도 집적 가능(TTL의 20~30%)
- LSI 및 VLSI에서 주로 사용
- 세 단자로 구성 : 드레인 (drain: D), 소스(source: S), 게이트(gate: G)
- NMOS : n-채널 트랜지스터
- PMOS : p-채널 트랜지스터

![alt](/assets/images/post/ComputerStudy/100.png)

#### (1) NMOS 트랜지스터 및 스위칭 회로

![alt](/assets/images/post/ComputerStudy/101.png)

#### (2) NAND 게이트의 NMOS 구현

- 두개의 NMOS 트랜지스터를 직렬로 접속하여 구성

![alt](/assets/images/post/ComputerStudy/102.png)

#### (3) MOS 게이트 회로

![alt](/assets/images/post/ComputerStudy/103.png)

- 입력단 트랜지스터 추가 -> 3-입력 NAND 게이트
- 출력단에 스위칭 회로 접속(인버터) -> AND 게이트

#### (4) NMOS 저항을 이용한 게이트 구현

- NMOS 저항 : NMOS의 드레인과 게이트를 접속했을 때 소스와 드레인 간에 존재하는 저항 성분
- 게이트 회로에서 부하 저항(RD)으로 사용 -> 제조 면적 감소

### 2) CMOS(Complementary MOS)게이트

- NMOS 및 PMOS 트랜지스터를 함께 이용하여 구현
- 장점 : 저전력

#### (1) NAND 게이트의 CMOS 구현

- 두개의 PMOS 트랜지스터를 벙렬로 접속하고, 두개의 NMOS 트랜지스터는 직렬로 접속

![alt](/assets/images/post/ComputerStudy/104.png)
![alt](/assets/images/post/ComputerStudy/105.png)

#### (2) NOR 게이트의 CMOS 구현

- 두개의 PMOS 트랜지스터를 직렬로 접속하고, 두개의 NMOS 트랜지스터는 병렬로 접속

![alt](/assets/images/post/ComputerStudy/106.png)

## 2. 논리게이트 IC칩을 이용한 회로 구현

### 1) 반도체 IC 칩

- 논리게이트는 반도체 IC 칩으로 제조
- IC칩에는 많은 수의 트랜지스터를 집적시킬 수 있으므로 하나의 IC칩에 여러개의 게이트들을 포함
- 국제 공통으로 부여된 고유번호에 의해 구분됨

#### (1) SSI 칩 (14핀)

- 4 ~ 6 개 정도의 게이트로 구성

### 2) SSI 칩들의 내부 구성

- 7408 : AND 게이트 4개, Vcc, GND
- 7432 : OR 게이트 4개, Vcc, GND
- 7400 : NAND 게이트 4개, Vcc, GND
- 7402 : NOR 게이트 4개, Vcc, GND
- 7404 : Hex Inverter (NOT 게이트 6개, Vcc, GND)

![alt](/assets/images/post/ComputerStudy/107.png)
![alt](/assets/images/post/ComputerStudy/108.png)
![alt](/assets/images/post/ComputerStudy/109.png)

### 3) XOR 게이트와 XNOR 게이트를 위한 IC 칩

![alt](/assets/images/post/ComputerStudy/110.png)
