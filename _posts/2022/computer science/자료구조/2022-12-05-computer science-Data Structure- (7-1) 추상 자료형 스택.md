---
title: (자료구조) 7-1 추상 자료형 스택
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 추상 자료형 스택
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-12-05 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 추상 자료형 스택

## 1. 스택 (Stack)

- 접시를 쌓듯이 자료를 차곡차곡 쌓아 올린 형태의 자료구조
- 예) 뷔페식당에 쌓인 접시, 책상 위에 쌓아둔 책 등
- **같은 구조와 같은 크기의 자료**를 정해진 방향만 쌓을 수 있고, **top**이라고 **정해진 곳으로만 접근이 가능**
- top을 통해서 자료가 삽입되므로 현재 스택의 가장 위에 있는 마지막 자료를 가리키며 새 자료는 top이 가리키는  
  자료의 위에 쌓이게 됨
- 먼저 삽입한 자료는 아래에 쌓이고 나중에 삽입한 원소는 위에 쌓이는 구조
- 마지막에 삽입된 자료가 가장 먼저 삭제되는 구조
- **후입선출(LIFO : Last In First Out)**

![alt](/assets/images/post/ComputerStudy/379.png)

## 2. 스택의 연산

- push : 스택에서 top을 통한 삽입 연산
- pop : 스택에서 top을 통한 삭제 연산

![alt](/assets/images/post/ComputerStudy/380.png)

### 1) 스택에서의 원소 삽입, 삭제 연산

- 공백 스택에 원소 A, B, C 순서대로 삽입하고 다시 자료 하나를 삭제하는 연산과정 동안의 스택 변화

![alt](/assets/images/post/ComputerStudy/381.png)

## 3. 스택 알고리즘

### 1) 스택에 대한 추상 자료형

![alt](/assets/images/post/ComputerStudy/382.png)

### 2) push 알고리즘

```c
  push(S, x)
    top <- top + 1;   // (1)
    if(top > stack_SIZE) then
      overflow;
    else
      S(top) <- x;    // (2)
```

#### (1) top <- top + 1;

- 스택 S에서 top이 마지막 자료를 가리키고 있으므로 그 위에 자료를 삽입하려면 먼저 top의 위치를 하나 증가시킴
- 이때 top의 위치가 스택의 크기(stack_SIZE)보다 크면 오버플로우 상태가 되므로 삽입 연산을  
  수행하지 못하고 연산이 종료

#### (2) S(top) ← x;

- 오버플로우 상태가 아니라면 스택의 top이 가리키는 위치 S(top)에 x를 삽입

### 3) pop 알고리즘

```c
  pop(S)
    if(top = 0) then underflow;
    esle{
      return S(top);    // (1)
      top <- top -1;    // (2)
    }
```

#### (1) return S(top);

- 스택이 공백이 아니라면 top이 가리키는 원소를 먼저 반환

#### (2) top <- top -1;

- 스택의 마지막 자료가 삭제 되었으면 top의 위치는 그 아래 자료가 되므로 top의 위치를 하나 아래로 감소
