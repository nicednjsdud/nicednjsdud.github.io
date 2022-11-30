---
title: (컴퓨터 개론) 6-3 알고리즘의 소개
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 알고리즘의 소개
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2022-11-30 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 알고리즘의 소개

## 1. 정렬 알고리즘

- 정보를 처리하기 위해서는 어떤 기준에 따라 순서가 정해져야 처리 속도가 빨라진다

### 1) 정렬(Sorting) 알고리즘

- 모든 자료를 처리할 때 꼭 사용하는 방식
- 정렬 방식은 키(Key)를 중심으로 오름차순 또는 내림차순으로 정렬
- 정렬 대상 데이터의 유형은 숫자, 문자, 이미지와 같은 멀티미디어 자료 등
- 정렬에는 내부정렬(알고리즘)과 외부정렬(보조기억장치)

### 2) 비교 정렬 알고리즘

#### (1) 버블 정렬 (Bubble Sort)

- 이웃하는 숫자를 비교하여(오름차순의 경우) 큰 수를 오른쪽으로 이동시켜 나가는 방식
- 시간복잡도 : 평균 경우 O(N2), 최악의 경우 O(N2)

![alt](/assets/images/post/ComputerStudy/327.png)

#### (2) 삽입 정렬 (Insertion Sort)

- 정렬이 된 왼쪽 부분과 정렬이 안된 오른쪽 부분으로 나누고 오른쪽 부분의 맨 왼쪽 요소를 정렬된 부분의  
  적절한 위치에 삽입하는 방식
- 시간복잡도 : 평균 경우 O(N2), 최악의 경우 O(N2)

![alt](/assets/images/post/ComputerStudy/328.png)

#### (3) 합병 정렬 (Merge Sort)

- 정렬한 데이터 수가 N일 때 이것을 1/2N으로 분할하여 정렬 한 후, 다시 1/4N으로 된 파일을 비교 정렬
- 파일크기가 2일 때까지 반복하는 방식
- 시간복잡도 : 평균 경우 O(N logN), 최악의 경우 O(N logN)

![alt](/assets/images/post/ComputerStudy/329.png)

- 피봇(Pivot)보다 더 큰 요소는 오른편으로, 피봇보다 작은 요소는 왼편으로 위치하도록 분할
- 피봇을 그사이에 놓는 방식을 반복적으로 수행
- 분할 정복 알고리즘(Divide and Conquer Algorithm)

#### (4) 퀵 정렬 (Quick Sort)

- 피봇(Pivot)이라 불리는 요소를 중심으로 피봇보다 작은 요소는 왼편으로, 피봇보다 큰 요소는 오른편으로  
  위치하도록 분할하고 피봇을 그사이에 놓는 방법을 반복하여 정렬하는 방식(Divide and Conquer 알고리즘)
- 시간 복잡도 : 평균 경우 O(N logN), 최악의 경우 O(N2)
- 일반적으로 지금까지 알려진 알고리즘 중 평균적으로 가장 빠른 고속 알고리즘

![alt](/assets/images/post/ComputerStudy/330.png)

### 3) 버블 , 삽입, 퀵정렬 처리시간 비교

![alt](/assets/images/post/ComputerStudy/331.png)

## 2. 탐색 알고리즘과 문제 해결

- 대형 문고에서 원하는 책을 빠르게 선택하기 위해서는 책장 내 책들이 탐색하기 쉽게 배열되어 있다.

### 1) 탐색(Searching) 알고리즘

- 수많은 데이터 중 어떤 조건을 만족시키는 데이터를 찾아내는 과정
- 탐색 알고리즘은 정렬 알고리즘과 관련성이 높음
- 주어진 상황과 가정에 따라(=정렬 여부에 따라) 적용할 수 있는 탐색 알고리즘이 달라짐
- 예) 웹 정보검색, 데이터베이스 SQL 질의어등

### 2) 탐색 알고리즘 종류

#### (1) 순차 탐색(Sequential Search)

- 임의의 데이터 모임에서 원하는 데이터를 찾기 위해 처음부터 하나씩 비교해 나가는 방식
- **데이터가 정렬되지 않는 경우에 사용**
- 시간복잡도 : 평균 경우 O(N), 최악의 경우 O(N)

![alt](/assets/images/post/ComputerStudy/332.png)

#### (2) 이진 탐색(Binary Search)

- 원래 데이터가 순서에 따라 정렬되어 있는 경우에 사용할 수 있는 알고리즘
- 정렬된 데이터의 중간을 중심으로 반으로 나누어 중앙 위치에 데이터를 비교, 나누어진 데이터를 다시 반으로  
  나누어 비교하는 방식
- 시간복잡도 : 평균 경우 O(logN), 최악의 경우 O(logN)

![alt](/assets/images/post/ComputerStudy/333.png)

### 3) 문제해결 방식

#### (1) 다항식 시간 복잡도

- P(Polynomial) 문제 = 다항식 문제
- 컴퓨터로 해결할 수 있는문제

#### (2) NP-완전(NP-Complete)문제

1. P문제보다 큰 시간 복잡도를 가진 알고리즘으로 제한 점을 주어 P문제로 변형해야 해결
2. 대표적인 것이 시간 복잡도가 지수 시간을 가지는 경우 : 예를 들면 O(2(n))
3. 어느 하나의 NP-완전 문제에 대하여 다항식 시간 복잡도의 알고리즘을 찾으면 모든 다른 NP-완전 문제도  
   다항식 시간에 해를 찾을 수 있음
   - = 컴퓨터로 해결 할 수 있는 문제화

#### (3) 분할 정복(Divide-and-Conquer) 알고리즘

- 주어진 문제의 입력을 분할하여 문제를 해결(정복)하는 방식
- 분할된 입력에 대해서 동일한 알고리즘을 적용해 해를 계산
- 이들의 해를 취합하여 원래의 문제의 해를 구하는 방식
- 이용 : 퀵 정렬

![alt](/assets/images/post/ComputerStudy/334.png)

#### (4) 그리디(Greedy) 알고리즘

- **최적화**(Optimization)문제에서 해를 찾을 때 항상 '욕심 내어'최소값 또는 최대값을 찾아가는  
  알고리즘(가능한 해들 중에서 가장 좋은 해를 찾는 문제)
- 탐욕, 욕심쟁이 알고리즘이라 불림
- 최소 스패닝 트리(Minimum Spanning Tree)

![alt](/assets/images/post/ComputerStudy/335.png)

#### (5) 동적 계획(Dynamic Programming) 알고리즘

- 최적화 문제해결 방법으로 입력 크기가 작은 부분문제들을 모두 해결한 후
- 그 해를 이용해서 점차적으로 큰 문제를 해결하는 방식
- 예) 피보나치 수열

#### (6) 근사(Approximation)

- NP-완전 문제를 해결하기 위하여 최적 해에 가까운 근사 해를 구하는 방식

#### (7) 백트래킹(Backtracking) 알고리즘

- 해를 찾는 도중에 '막히면'(즉, 해가 아니면) 되돌아가서 다시 해를 찾아가는 방식으로, 최적화 문제와 결정  
  문제를 해결하는 기법
- 예) 8퀸 문제

#### (8) 분기 한정(Brance-and-Bound) 알고리즘

- 백트래킹의 단점을 보완하는 탐색 기법으로
- 문제의 조건에 따라 해를 깊이 우선 탐색할 때 특정한 값(한정 값)에 따라 가지치기를 하는 방식

![alt](/assets/images/post/ComputerStudy/336.png)
