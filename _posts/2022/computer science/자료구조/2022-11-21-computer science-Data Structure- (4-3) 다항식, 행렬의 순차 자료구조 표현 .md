---
title: (자료구조) 4-3 다항식, 행렬의 순차 자료구조 표현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 다항식, 행렬의 순차 자료구조 표현
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-21 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 다항식, 행렬의 순차 자료구조 표현

## 1. 다항식의 1차원 배열을 이용한 구현

### 1) 다항식이란

#### (1) aX(e) 형식의 항들의 합으로 구성된 식

- a : 계수 (coefficient)
- X : 변수 (varable)
- e : 지수 (exponent)

#### (2) 다항식의 특징

- 지수에 따라 내림차순으로 항을 나열
- 다항식의 차수 : 가장 큰 지수
- 다항식 항의 최대 개수 = (차수 +1)개

### 2) 다항식의 추상 자료형

- ADT Polynomial

![alt](/assets/images/post/ComputerStudy/127.png)
![alt](/assets/images/post/ComputerStudy/128.png)

### 3) 다항식의 표현

#### (1) 각 항의 지수와 계수의 쌍에 대한 선형리스트

- 지수 ()로 표현
- 예) A(x) = 4x(3) + 3x(2) + 2 => p1 = (3,4, 2,3, 0,2)

#### (2) 1차원 배열을 이용한 순차 자료구조 표현

- 차수가 n인 다항식을 (n+1)개의 원소를 가지는 1차원 배열로 표현
- 배열 인덱스 i : 지수(n-1)을 의미
- 배열 인덱스 i의 원소 : 지수 (n-1)항의 계수
  - 다항식에 포함되지 않은 지수의 항에 대한 원소에 0을 저장

![alt](/assets/images/post/ComputerStudy/129.png)

#### (3) 희소 다항식에 대한 1차원 배열 저장

- ex) B(x) = 3x(1000 지수) + x + 4
- 차수가 1000이므로 크기가 1001인 배열을 사용하는데 항이 단 3개로 배열의 원소 중에서 3개만이  
  사용되어 메모리 공간 낭비

## 2. 다항식의 2차원 배열을 이용한 구현

### 1) 2차원 배열을 이용한 순차 자료구조 표현

#### (1) 다항식의 각 항에 대한 <지수,차수>쌍을 2차원 배열에 저장

- 2차원 배열의 행의 개수 : 다항식의 항의 개수
- 2차원 배열의 열의 개수 : 2
- ex) B(x) = 3x(1000 지수) + x + 4의 2차원 열 표현

* 1차원 배열을 사용하는 방법보다 메모리 사용 공간량 감소

![alt](/assets/images/post/ComputerStudy/130.png)

### 2) 다항식의 덧셈 알고리즘 : A(x) + B(x) = C(x)

- AddPoly(A,B)

![alt](/assets/images/post/ComputerStudy/131.png)

## 3. 행렬의 순차자료구조 표현

### 1) 행렬이란

- 행과 열로 구성된 자료구조

#### 예) m x n 행렬은

- m : 행의 개수
- n : 열의 개수
- 원소의 개수 : (m x n) 개

### 2) 전치 행렬

- 행렬의 행과 열을 서로 교환하여 구성한 행렬
- 행렬 A의 모든 원소의 위치(i,j)를 (j,i)로 교환
- m X n 행렬을 n X m 행렬로 변환한 행렬 A'은 행렬 A의 전치행렬

![alt](/assets/images/post/ComputerStudy/132.png)

#### 예)

![alt](/assets/images/post/ComputerStudy/133.png)

### 3) 행렬의 순차 자료구조 표현

#### (1) 2차원 배열 사용

- m X n 행렬을 m행 n열의 2차원 배열로 변환

![alt](/assets/images/post/ComputerStudy/134.png)

#### (2) 희소행렬에 대한 2차원 배열 표현

- 그림 두번째와 같이 배열의 원소 56개 중에서 실제 사용하는 것은 10개로  
  메모리 공간 활용도가 떨어지는 배열을 희소행렬이라고 함.
- 0이 아닌 원소만 추출하여 `<행 번호,열 번호, 원소>` 쌍으로 배열에 저장
- 추출한 순서쌍을 2차원 배열의 행으로 저장

![alt](/assets/images/post/ComputerStudy/135.png)

- 원래의 행렬에 대한 정보를 순서쌍으로 작성하여 0번 행에 저장
- <전체 행의 개수, 전체 열의 개수, 0이 아닌 원소의 개수>

![alt](/assets/images/post/ComputerStudy/136.png)

### 4) 희소행렬의 추상 자료형

- ADT Sparse_Matrix

![alt](/assets/images/post/ComputerStudy/137.png)
