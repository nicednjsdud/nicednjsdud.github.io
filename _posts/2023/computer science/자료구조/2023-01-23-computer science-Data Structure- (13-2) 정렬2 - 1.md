---
title: (자료구조) 13-2 정렬 2 (쉘 정렬)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 정렬 2
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-23 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 정렬 2 (쉘 정렬)

## 1. 쉘 정렬

- 일정한 간격으로 떨어져있는 자료들끼리 부분집합을 구성
- 각 부분집합에 있는 원소들에 대해서 삽입 정렬을 수행하는 작업을 반복
- 전체 원소들을 정렬하는 방법
- 전체 원소에 대해서 삽입 정렬을 수행하는 것보다 부분집합으로 나누어 정렬하게 되면 비교연산과 교환연산 감소

### 1) 개요

#### (1) 셀 정렬의 부분집합

- 부분집합의 기준이 되는 가격을 매개변수 h에 저장
- 한 단계가 수행될 때마다 h의 값을 감소시키고 셀 정렬을 순환 호출
- h가 1이 될때까지 반복

#### (2) 셀 정렬의 성능은 매개변수 h의 값에 따라 달라짐

- 정렬할 자료의 특성에 따라 매개변수 생성 함수를 사용
- 일반적으로 사용하는 h의 값은 원소 개수의 1/2을 사용하고 한 단계 수행 될때마다 h의 값을 반으로 감소시키면서 반복수행

### 2) 수행 과정

- 정렬되어 있지 않은 `{69,10,30,2,16,8,31,22}`의 자료들을 셸 정렬 방법으로 정렬하는 과정

#### (1) 원소의 개수가 8개이므로 매개변수 h는 4에서 시작

- `h = 4`이므로 간격이 4인 원소들을 같은 부분집합으로 만들면 4개의 부분집합이 만들어짐

![alt](/assets/images/post/ComputerStudy/749.png)

- 첫번째 부분집합 `{69,16]`에 대해서 삽입 정렬을 수행

- 수행 전

![alt](/assets/images/post/ComputerStudy/750.png)

- 수행 후

![alt](/assets/images/post/ComputerStudy/751.png)

#### (2) 두 번째 부분집합 `{10,8}`에 대해서 삽입 정렬 수행

- 수행 전

![alt](/assets/images/post/ComputerStudy/752.png)

- 수행 후

![alt](/assets/images/post/ComputerStudy/753.png)

#### (3) 세번째 부분집합 `{30,31}`에 대해서 삽입 정렬 수행

- (30 < 31)이므로 자리교환은 이루어지지 않음

![alt](/assets/images/post/ComputerStudy/754.png)

#### (4) 네번째 부분집합 `{2,22}`에 대해서 삽입 정렬 수행

- (2 < 22)이므로 자리 교환은 이루어지지 않음

![alt](/assets/images/post/ComputerStudy/755.png)

#### (5) 이제 h를 2로 변경하고 다시 셸 정렬 시작

- h = 2 이므로 간격이 2인 원소들을 같은 부분 집합으로 만들면 2개의 부분 집합이 만들어짐

![alt](/assets/images/post/ComputerStudy/756.png)

#### (6) 첫 번째 부분 집합 `{16,30,69,31}` 삽입 정렬 수행

![alt](/assets/images/post/ComputerStudy/757.png)

#### (7) 두 번째 부분 집합 `{8,2,10,22}`에 대해서 삽입 정렬 수행

![alt](/assets/images/post/ComputerStudy/758.png)

#### (8) 이제 h를 1로 변경하고 다시 셀 정렬 시작

- h = 1이므로 간격 1인 원소들을 같은 부분 집합으로 만들면 1개의 부분 집합이 만들어짐
- 즉, 전체 원소에 대해서 삽입 정렬을 수행하고 셀 정렬 완성

![alt](/assets/images/post/ComputerStudy/760.png)

### 3) 셀 정렬 알고리즘

```c
  shellSort(a[],n)
        interval <- n;
        while(interval >= 1) do {

              interval <-> interval/2;
              for( i <- 0; i< interval; i <- i + 1) do{

                  intervalSort(a[],i,n,interval);
              }
        }
  end shellSort()
```

#### (1) 메모리 사용공간

- n개의 원소에 대하여 n개의 메모리와 매개변수 h에 대한 저장공간 사용

#### (2) 연산 시간

- 비교횟수 : 처음 원소의 상태에 상관없이 매개변수 h에 의해 결정
- 일반적인 시간 복잡도 : `O(n(1.25승))`
- 셀 정렬은 삽입 정렬의 시간 복잡도 `O(n(2승))`보다 개선된 정렬 방법
