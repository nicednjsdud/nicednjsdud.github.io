---
title: (자료구조) 7-2 스택의 구현과 기본 응용
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

## 1. 순차 자료구조인 1차원 배열을 이용하여 스택을 구현

### 1) 순차 자료구조인 1차원 배열을 이용하여 스택을 구현

- 스택의 크기 : 배열의 크기
- 스택에 쌓이는 순서 : 배열의 인덱스
  - 스택의 첫 번째 원소 : 인덱스 0번
  - 스택의 n번째 원소 : 인덱스 n-1
- 변수 top : 스택에 저장된 마지막 원소에 대한 인덱스 저장
  - 공백 상태 : top = -1(초기값)
  - 포화상태:top=n–1

![alt](/assets/images/post/ComputerStudy/389.png)

### 2) 스택 구현

```c
  #include <stdio.h>
  #include <stdlib.h>
  #define STACK_SIZE 100

  typedef int element;    // int를 스택 element의 자료형으로 정의
  element stack[STACK_SIZE];
  int top = -1;           // 스택의 top의 초기값을 -1로 설정

  void push(element item)
  {
    if(top >= STACK_SIZE-1){    // 스택이 이미 full인경우
          printf("\n\n Stack is FULL ! \n");
          return;
    }
    else
      stack[++top] = item;
  }

  element pop() // 스택의 삭제 후 반환 연산
  {
    if(top == -1){  // 현재 스택이 공백인 경우
          printf("\n\n Stack is Empty ! \n");
          return 0;
    }

    return stack[top--];
  }

  void del()    // 스택의 삭제 연산
  {
    if(top == -1){    // 현재 스택이 공백인 경우
          printf("\n\n Stack is Empty ! \n");
          exit(1);
    }
    top --;
  }

  element peek()     // 스택의 top 원소 검색 연산
  {
    if(top == -1){    // 현재 스택이 공백인 경우
          printf("\n\n Stack is Empty ! \n");
          exit(1);
    }
    return stack[top];
  }

  void printStack()   // 스택 내용 출력 연산
  {
    int i;
    printf("\n STACK [");
    for(i = 0; i<=top; i++)
        printf("%d ",stack[i]);
    printf("] ");
  }
```

## 2. 연결 자료 구조를 이용한 스택의 구현

### 1) 단순 연결 리스트를 이용하여 스택을 구현

#### (1) 스택의 원소 : 단순 연결 리스트의 노드

- 스택 원소의 순서 : 연결 리스트 노드의 링크로 표현
- push : 리스트의 마지막에 노드 삽입
- pop : 리스트의 마지막 노드 삭제

#### (2) 변수 top

- 단순 연결 리스트의 마지막 노드를 가리키는 포인터 변수
- 초기 상태 : top = null

![alt](/assets/images/post/ComputerStudy/383.png)

### 2) 단순 연결 리스트를 사용한 스택에서의 연산 과정

#### (1) 공백 스택 생성 : createStack(S);

![alt](/assets/images/post/ComputerStudy/384.png)

#### (2) 원소 A 삽입 : push(S, A);

![alt](/assets/images/post/ComputerStudy/385.png)

#### (3) 원소 B 삽입 : push(S, B);

![alt](/assets/images/post/ComputerStudy/386.png)

#### (4) 원소 C 삽입 : push(S, C);

![alt](/assets/images/post/ComputerStudy/387.png)

#### (5) 원소 삭제 : pop(S, C);

![alt](/assets/images/post/ComputerStudy/388.png)

## 3. 역순 문자열 만들기

### 1) LIFO 성질을 이용하여 역순 문자열 만들기

#### (1) 문자열을 순서대로 스택에 삽입

![alt](/assets/images/post/ComputerStudy/390.png)

#### (2) 스택을 pop하여 문자열로 저장하기

![alt](/assets/images/post/ComputerStudy/391.png)
