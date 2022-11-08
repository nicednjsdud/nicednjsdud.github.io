---
title: (Software) Data Structures & Algorithm
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Software
description: Data Structures & Algorithm
tag: Data Structures
article_tag1: Data Structures
article_section: Data Structures
meta_keywords: Data Structures, Computer, Software
last_modified_at: "2022-11-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조

## 1. 일상생활에서의 사물의 조직화

![alt](/assets/images/post/software/6.png)

## 2. 일상생활과 자료구조의 비교

![alt](/assets/images/post/software/7.png)

## 3. 자료구조와 알고리즘

- 프로그램 = 자료구조 + 알고리즘
- 예) 최대값 탐색 프로그램 = 배열 + 순차탐색

![alt](/assets/images/post/software/8.png)

## 4. 알고리즘

### 1) 알고리즘 (algorithm)

- 컴퓨터로 문제를 풀기 위한 단계적인 절차

### 2) 알고리즘의 조건

- 입력 : 0개 이상의 입력이 존재하여야 한다.
- 출력 : 1개 이상의 출력이 존재하여야 한다.
- 명백성 : 각 명령어의 의미는 모호하지 않고 명확해야 한다.
- 유한성 : 한정된 수의 단계 후에도 반드시 종료되어야 한다.
- 유효성 : 각 명령어들은 실행 가능한 연산이어야 한다.

## 5. 알고리즘의 기술 방법

- 1. 영어나 한국어와 같은 자연어
- 2. 흐름도 (flow chart)
- 3. 유사 코드 (pseudo-code)
- 4. C와 같은 프로그래밍 언어
- 예) 배열에서 최대값 찾기 알고리즘 ...ArrayMax(A,n)

### 1) 자연어로 표기된 알고리즘

- 인간이 읽기가 쉽다.
- 그러나 자연어의 단어들을 정확하게 정의하지 않으면 의미 전달이 모호해질 우려가 있다.
- 예) 배열에서 최대값 찾기 알고리즘

```java
ArrayMax(A,n)

1. 배열 A의 첫번째 요소를 변수 tmp에 복사
2. 배열 A의 다음 요소들을 차례대로 tmp와 비교하면 더 크면 tmp로 복사
3. 배열 A의 모든 요소를 비교했으면 tmp를 변환
```

### 2) 흐름도로 표기된 알고리즘

- 직관적이고 이해하기 쉬운 알고리즘 기술 방법
- 그러나 복잡한 알고리즘의 경우, 상당히 복잡해짐

![alt](/assets/images/post/software/9.png)

### 3) 유사코드로 표현된 알고리즘

- 알고리즘의 고수준 기술방법
- 자연어보다는 더 구조적인 표현 방법
- 프로그래밍 언어보다는 덜 구체적인 표현방법
- 알고리즘 기술에 가장 많이 사용
- 프로그램을 구현할 때의 여러가지 문제들을 감출 수 있다.
- 즉, 알고리즘의 핵심적인 내용에만 집중할 수 있다.

```c
  ArrayMax(A,n)

  tmp <- A[0];
  for i<- 1 to n-1 do
            if tmp < A[i] then
                    tmp <- A[i];
  return tmp;
```

### 4) C로 표현된 알고리즘

- 알고리즘의 가장 정확한 기술이 가능
- 반면 실제 구현시의 많은 구체적인 사항들이 알고리즘의 핵심적인 내용들의 이해를 방해할 수 있다.

```C
  #define MAX_ELEMENTS 100
  int score[MAX_ELEMENTS];
  int find_max_score(int n)
  {
    int i,tmp;
    tmp = score[0];
    for(int i; i<n ; i++){
      if(score[i] > tmp){
        tmp = score[i];
      }
    }
    return tmp;
  }
```
