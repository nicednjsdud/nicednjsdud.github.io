---
title: (자료구조) 9-1 큐와 선형 큐
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 큐와 선형 큐
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-12-20 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 큐와 선형 큐

## 1. 큐의 이해

### 1) 큐 (Queue)

- 삽입과 삭제의 위치와 방법이 제한된 유한 순서 리스트
- 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 할 수 있는 구조
- 삽입한 순서대로 원소가 나열되어 가장 먼저 삽입한 원소는 맨앞에 있다가 가장 먼저 삭제
- **선입선출 구조 (FIFO, First-In-First-Out)**

### 2) 스택과 큐의 비교

![alt](/assets/images/post/ComputerStudy/404.png)

### 3) 큐의 구조

![alt](/assets/images/post/ComputerStudy/405.png)

![alt](/assets/images/post/ComputerStudy/406.png)

### 4) 큐의 연산

- 삽입 : enQueue
- 삭제 : deQueue

## 2. 추상 자료형 큐

### 1) 큐의 연산 과정

#### (1) 공백 큐 생성 : createQueue();

![alt](/assets/images/post/ComputerStudy/407.png)

#### (2) 원소 A 삽입 : enQueue(Q,A);

![alt](/assets/images/post/ComputerStudy/408.png)

- rear <- Last Data

#### (3) 원소 B 삽입 : enQueue(Q,B);

![alt](/assets/images/post/ComputerStudy/409.png)

#### (4) 원소 삭제 : deQueue(Q);

![alt](/assets/images/post/ComputerStudy/410.png)

#### (5) 원소 C 삽입 : enQueue(Q,C);

![alt](/assets/images/post/ComputerStudy/411.png)

#### (6) 원소 삭제 : deQueue(Q);

![alt](/assets/images/post/ComputerStudy/412.png)

#### (7) 원소 삭제 : deQueue(Q);

![alt](/assets/images/post/ComputerStudy/413.png)

## 3. 선형큐의 구현

### 1) 순차 자료구조를 이용한 큐의 구현

#### (1) 1차원 배열을 이용한 큐

- 큐의 크기 : 배열의 크기
- 변수 front : 저장된 첫 번째 원소의 인덱스 저장
- 변수 rear : 저장된 마지막 원소의 인덱스 저장

#### (2) 상태표현

- 초기 상태 : front = rear = -1
- 공백 상태 : front = rear
- 포화 상태 : rear = n - 1 (n : 배열의 크기,n-1 : 배열의 마지막 인덱스)

### 2) 선형 큐 알고리즘

#### (1) 초기 공백 큐 생성 알고리즘

- 크기가 n인 1차원 배열 생성
- front와 rear를 -1로 초기화

```c
  CreateQueue()
      Q[n];
      front <- -1;
      rear <- -1;
  end createQueue()
```

#### (2) 공백 큐 검사 알고리즘과 포화 상태 검사 알고리즘

- 공백 상태 : front = rear
- 포화 상태 : rear = n - 1 (n : 배열의 크기,n-1 : 배열의 마지막 인덱스)

```c
  isEmpty(Q)
      if(front = rear) then return true;
      else return false;
  end isEmpty()

  isFull(Q)
      if(rear = n-1) then return true;
      else return false;
  end isFull()
```

#### (3) 큐의 삽입 알고리즘

```c
  enQueue(Q, item)
      if(isFull(Q)) then err;
      else{
          rear <- rear+1;         // (1)
          Q[rear] <- item;        // (2)
      }
  end enQueue();
```

- 마지막 원소의 뒤에 삽입하여야 하므로
  - 마지막 원소의 인덱스를 저장한 rear의 값을 하나 증가시켜 삽입할 자리 준비
  - 그 인덱스에 해당하는 배열원소 `Q[rear]`에 item을 저장

#### (4) 큐의 삭제 알고리즘

```c
  deQueue(Q)
      if(isEmpty(Q)) then err;
      else{
        front <- front + 1;       // (1)
        return Q[front];          // (2)
      }
  end deQueue()

  delete(Q)
      if(isEmpty(Q)) then err;
      else front <- front + 1;
  end delete();
```

- 가장 앞에 있는 원소를 삭제해야 하므로
  - front의 위치를 한자리 뒤로 이동하여 큐에 남아있는 첫 번째 원소의 위치를 이동하여 삭제할 자리 준비
  - 그 자리의 원소는 삭제하여 반환함

#### (5) 큐의 검색 알고리즘

```c
  peek(Q)
    if(isEmpty(Q)) then err;
    else return Q[front + 1];
  end peek();
```

- 가장 앞에 있는 원소를 검색하여 반환하는 연산
- 현재 front의 한자리 뒤(front + 1)에 있는 원소
- 큐에 있는 첫번째 원소를 반환
