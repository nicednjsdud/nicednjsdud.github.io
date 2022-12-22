---
title: (자료구조) 9-3 큐의 구현 - 덱
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 큐의 구현 2
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-12-22 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 큐의 구현 - 덱

## 1. 덱의 이해

### 1) 덱 (Deque)

- 큐의 양쪽 끝에서 삽입 연산과 삭제 연산을 수행할 수 있는 확장된 큐
- 큐 2개를 반대로 붙여서 만든 자료구조

![alt](/assets/images/post/ComputerStudy/432.png)

### 2) 덱에 대한 추상 자료형

- 덱의 연산 과정

#### (1) createDeque();

![alt](/assets/images/post/ComputerStudy/433.png)

#### (2) insertFront(DQ, 'A');

![alt](/assets/images/post/ComputerStudy/434.png)

#### (3) insertFront(DQ, 'B');

![alt](/assets/images/post/ComputerStudy/435.png)

#### (4) insertRear(DQ, 'C');

![alt](/assets/images/post/ComputerStudy/436.png)

#### (5) deleteFront(DQ);

![alt](/assets/images/post/ComputerStudy/437.png)

#### (6) deleteRear(DQ);

![alt](/assets/images/post/ComputerStudy/438.png)

#### (7) insertRear(DQ, 'D');

![alt](/assets/images/post/ComputerStudy/439.png)

#### (8) insertFront(DQ, 'E');

![alt](/assets/images/post/ComputerStudy/440.png)

#### (9) insertFront(DQ, 'F');

![alt](/assets/images/post/ComputerStudy/441.png)

- 최종적으로 F E A D

## 2. 덱의 구현

- 양쪽 끝에서 삽입, 삭제 연산을 수행하면서 크기 변화와 저장된 원소 순서 변화가 많으므로 순차 자료구조는  
  비효율적
- 양방향으로 연산이 가능한 이중 연결 리스트를 이용함

![alt](/assets/images/post/ComputerStudy/442.png)

## 3. 큐의 응용

### 1) 운영체제의 작업 큐

#### (1) 프린터 버퍼 큐

- CPU에서 프린터로 보낸 데이터 순서대로 (선입선출) 프린터에서 출력하기 위해서 선입선출 구조의 큐 사용

#### (2) 스케줄링 큐

- CPU 사용을 요청한 프로세서들의 순서를 스케줄링하기 위해서 큐를 사용

![alt](/assets/images/post/ComputerStudy/443.png)

#### (3) 시뮬레이션 큐잉 시스템

- 시뮬레이션을 위한 수학적 모델링에서 대기행렬과 대기시간 등을 모델링 하기 위해서 큐잉 이론 사용
