---
title: (자료구조) 4-2 선형리스트 구현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 선형리스트 구현
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-21 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 선형 리스트의 구현

## 1. 1차원 배열을 이용한 구현

### 1) 개요

- 선형리스트를 순차 구조로 구현하기 위하여 배열을 사용
- 배열 : <인덱스,원소>의 쌍으로 구성
- 배열의 인덱스 : 배열 원소의 순서 표현

### 2) 1차원 배열을 이용한 선형리스트 구현

![alt](/assets/images/post/ComputerStudy/118.png)

#### (1) 배열을 이용한 구현

- 선형 리스트의 논리적 구조

![alt](/assets/images/post/ComputerStudy/119.png)

- 선형 리스트이 물리적 구조
- a + (i-1) X l

![alt](/assets/images/post/ComputerStudy/120.png)

#### (2) C 프로그램

```c
#include <stdio.h>

void main()
{
  int i, sale[4] = {157,209,251,312};

  for(i=0; i<4; i++){
    printf("\n address:%u sale[%d = %d]", &sale[i], i, sale[i]);
  }

  getchar();
}
```

- 실행 결과

```c
  address: 1245036 sale[0] = 157
  address: 1245040 sale[1] = 209
  address: 1245044 sale[2] = 251
  address: 1245048 sale[3] = 312
```

## 2. 2차원 배열을 이용한 구현

### 1) 2차원 배열을 이용한 선형리스트 구현

- 2009 ~ 2010년 분기별 노트북 판매량

![alt](/assets/images/post/ComputerStudy/121.png)

- 논리적 구조

![alt](/assets/images/post/ComputerStudy/122.png)

#### (1) 2차원 배열의 물리적 저장 방법

##### (1-1) 행 우선 순서 방법(row major order)

- 2차원 배열의 첫 번째 인덱스인 행을 기준으로 하여 같은 행 안에 있는 열을 저장

![alt](/assets/images/post/ComputerStudy/123.png)

- 원소의 위치 계산 방법 : a + (i X n(j) + j) X l

##### (1-2) 열 우선 순서 방법(column major order)

- 2차원 배열의 마지막 인덱스인 열을 기준으로 하여 같은 열 안에 있는 행을 저장

![alt](/assets/images/post/ComputerStudy/124.png)

- 원소의 위치 계산 방법 : a + (j X n(j) + i) X l

#### (2) C 프로그램

```c
#include <stdio.h>

void main()
{
  int i, n=0, *ptr;
  int sale[4] = {% raw %}{{63, 84, 140, 130},{157,209,251,312}};{% endraw %}
  // 2차원 배열 초기화

  ptr = &sale[0][0];
  for(i=0; i<8; i++){
    printf("\n address: %u sale %d = %d ", ptr, i, *ptr);
    ptr ++;
  }

  getchar();
}
```

- 실행 결과

```c
  address: 12345012 sale 0 = 63
  address: 12345016 sale 1 = 84
  address: 12345020 sale 2 = 140
  address: 12345024 sale 3 = 130
  address: 12345028 sale 4 = 157
  address: 12345032 sale 5 = 209
  address: 12345036 sale 6 = 251
  address: 12345040 sale 7 = 312
```

- C 컴파일러가 행 우선 순서 방법을 사용한다는 것을 확인할 수 있다.

## 3. 3차원 배열을 이용한 구현

### 1) 3차원 배열을 이용한 선형리스트 구현

- 1팀과 2팀에 대한 2009 ~ 2010년 분기별 노트북 판매량 리스트

![alt](/assets/images/post/ComputerStudy/125.png)

- 논리적 구조

![alt](/assets/images/post/ComputerStudy/126.png)

#### (1) 3차원 배열의 물리적 저장 방법

- 3차원 논리적 순서를 1차원 물리적 순서로 변환하는 방법을 사용

##### (1-1) 면 우선 순서 방법

- 3차원 배열의 첫 번째 인덱스인 면을 1차 기준으로 면 안에 있는 행을 먼저 저장  
  다시 행을 2차 기준으로 하여 같은 행 안에 있는 열을 저장하는 방법

##### (1-2) 열 우선 순서 방법

- 열을 1차 기준으로 열 안에 있는 행을 먼저 저장하고 다시 2차 기준으로 하여 같은 행에  
  대한 면을 저장

#### (2) C 프로그래밍

```c
#include <stdio.h>

void main()
{
  int i, n=0, *ptr;
  int sale[2][2][4] = {% raw %}{{{63,84,140,130},  // 면 0
                        {157,209,251,312}},
                        {{59,80,130,135},   // 면 1
                        {149,187,239,310}}
                        };{% endraw %}

  ptr = &sale[0][0][0];
  for(i = 0; i<16 ; i++){
    printf("\n address: %u sale %2d = %3d",ptr, i, *ptr);
    ptr++;
  }
  getchar();
}
```

- 실행 결과

```c
  address: 12344980 sale 0 = 63
  address: 12344984 sale 1 = 84
  address: 12344988 sale 2 = 140
  address: 12344992 sale 3 = 130
  address: 12344996 sale 4 = 157
  address: 12345000 sale 5 = 209
  address: 12345004 sale 6 = 251
  address: 12345008 sale 7 = 312
```

- C컴파일러가 면 우선 순서 방법으로 3원 배열을 저장함을 확인할 수 있다.
