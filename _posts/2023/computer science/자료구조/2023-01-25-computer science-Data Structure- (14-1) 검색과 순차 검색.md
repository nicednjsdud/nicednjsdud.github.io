---
title: (자료구조) 14-1 검색과 순차 검색
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

# 자료 구조 - 검색과 순차 검색

## 1. 검색과 검색 방법

### 1) 검색

- 컴퓨터에 저장한 자료 중에서 원하는 항목을 찾는 작업
- 검색 성공 : 원하는 항목을 찾은 경우
- 검색 실패 : 원하는 항목을 찾지 못한 경우

#### (1) 탐색 키를 가진 항목을 찾는 것

- 탐색 키 (search key) : 자료를 구별하여 인식할 수 있는 키

#### (2) 삽입/ 삭제 작업에서의 검색

- 원소를 삽입하거나 삭제할 위치를 찾기 위해서 검색 연산 수행

### 2) 검색 방법

#### (1) 수행 위치에 따른 분류

##### (1-1) 내부 검색

- 메모리 내의 자료에 대해서 검색 수행

##### (1-2) 외부 검색

- 보조 기억 장치에 있는 자료에 대해서 검색 수행

#### (2) 검색 방식에 따른 분류

##### (2-1) 비교 검색 방식 (comparison search method)

- 검색 대상의 키를 비교하여 검색하는 방법
- 순차 검색, 이진 검색, 트리 검색

##### (2-2) 계산 검색 방식 (non-comparison method)

- 계수적인 성질을 이용한 계산으로 검색 하는 방법

#### (3) 검색 방식의 선택

- 자료 구조의 형태와 자료의 배열 상태에 따라 최적의 검색 방법 선택

## 2. 정렬, 비정렬 순차 검색

### 1) 순차 검색, 선형 검색

- 일렬로 된 자료를 처음부터 마지막가지 순서대로 검색하는 방법
- 가장 간단하고 직접적인 검색 방법
- 배열이나 연결 리스트로 구현된 순차 자료 구조에서 원하는 항목을 찾는 방법
- 검색 대상 자료가 많은 경우에 비효율적이지만 **알고리즘이 단순하여 구현이 용이**

### 2) 정렬 되지 않은 순차 자료구조에서의 순차 검색

#### (1) 검색 방법

- 첫 번째 원소부터 시작하여 마지막 원소까지 순서대로 키 값이 일치하는 원소가 있는지를 비교하여 찾음
- 키 값이 일치하는 원소를 찾으면 그 원소가 **몇 번째 원소인지를 반환**
- 마지막 원소까지 비교하여 키 값이 일치하는 원소가 없으면 찾는 원소가 없는 것이므로 **검색 실패**

##### (1-1) 순차 검색 성공의 경우

![alt](/assets/images/post/ComputerStudy/784.png)

##### (1-2) 순차 검색 실패의 경우

![alt](/assets/images/post/ComputerStudy/785.png)

#### (2) 검색 알고리즘

```c
  sequentialSearch1(a[], n, key)
        i <- 0;
        while(i<n and a[i] != key) do{
          i <- i + 1;
        }
        if(i<n) then return i;
        else return -1;
  end sequentialSearch1()
```

##### (2-1) 비교 횟수

- 찾고자 하는 원소의 위치에 따라 결정
- 찾는 원소가 첫 번째 원소라면 비교횟수는 1번
- 두번째 원소라면 비교횟수는 2번.. 찾는 원소가 i번째 원소이면 i번..
- 정렬 되지 않은 원소에서의 순차 검색의 평균 비교횟수 = **(n+1)/2**

##### (2-2) 평균 시간복잡도

- **O(n)**

### 3) 정렬되어 있는 순차 자료구조에서의 순차 검색

#### (1) 검색 방법

- 순서대로 검색하면서 키 값을 비교하여, 원소의 키 값이 찾는 키 값보다 크면 찾는 원소가 없는 것이므로  
  더이상 검색을 수행하지 않고 종료

##### (1-1) 검색 성공의 경우

![alt](/assets/images/post/ComputerStudy/786.png)

##### (1-2) 검색 실패의 경우

![alt](/assets/images/post/ComputerStudy/787.png)

#### (2) 정렬되어있는 자료에 대한 순차 검색 알고리즘

```c
  sequentialSearch2(a[], n, key)
      i <- 0;
      while(a[i]< key) do {
        i <- i + 1;
      }
      if(a[i] = key) then return i;
      else return -1;
  end sequentialSearch2()
```

##### (2-1) 비교 횟수

- 찾고자 하는 원소의 위치에 따라 결정
- 검색 실패의 경우에 평균 비교 횟수가 반으로 줄어듦
- 정렬되어잇는 원소에서의 순차 검색의 평균 비교 횟수 = **(n+1)/4**

##### (2-2) 평균 시간 복잡도

- **O(n)**
