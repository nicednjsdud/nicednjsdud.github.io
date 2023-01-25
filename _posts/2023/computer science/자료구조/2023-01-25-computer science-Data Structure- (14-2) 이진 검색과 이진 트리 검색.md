---
title: (자료구조) 14-2 이진 검색 방법과 알고리즘
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
last_modified_at: "2023-01-25 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 이진 검색 방법과 알고리즘

## 1. 이진 검색

- 자료의 가운데에 있는 항목을 키 값과 비교하여 다음 검색 위치를 결정하여 검색을 계속 하는 방법
- binary search, 이분 검색, 보간 검색

### 1) 찾는 키 값 > 원소의 키 값

- 오른쪽 부분에 대해서 검색 실행

### 2) 찾는 키 값 < 원소의 키 값

- 왼쪽 부분에 대해서 검색 실행

### 3)

- 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여가면서 더빠르게 검색
- 정복 기법을 이용한 검색 방법 : 검색 범위를 반으로 분할하는 작업과 검색 작업을 반복 수행
- **반드시 정렬되어있는 자료에 대해서 수행하는 검색 방법**

### 4) 수행 위치에 따른 분류

![alt](/assets/images/post/ComputerStudy/790.png)

## 2. 이진 검색 알고리즘

```c
  binarySearch(a[], low, high, key)
      middle <- (low + high) / 2;
      if(key = a[middle]) then return i;
      else if(key < a[middle]) then binarySearch(a[],low, middle-1, key);
      else if(key > a[middle]) then binarySearch(a[], middle + 1, high, key);
      else return -1;
  end binarySearch()
```

- 삽입이나 삭제가 발생했을 경우에 항상 배열의 상태를 정렬 상태로 유지하는 추가적인 작업 필요
- 시간 복잡도 : **O(log2n)**
