---
title: (자료구조) 4-1 선형자료 구조
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 선형자료 구조
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-21 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 선형자료 구조

## 1. 선형자료구조 리스트

### 1) 리스트

- 자료를 나열한 목록
- 예)

![alt](/assets/images/post/ComputerStudy/111.png)

### 2) 선형리스트 (Linear List)

- 나열한 원소들 간에 순서를 가지고 있는 리스트
- 순서 리스트(Ordered List)라고도 불림

### 3) 리스트 표현 형식

- 리스트 이름 = (원소1, 원소2, ... , 원소 n)
- 선형 리스트에서 원소를 나열한 순서는 원소들의 순서임
- 예) 동창 = (상원,승의,수영,철이)

![alt](/assets/images/post/ComputerStudy/112.png)

#### (1) 공백리스트

- 원소가 하나도 없는 리스트
- 빈 괄호를 사용하여 표현 : 공백리스트 이름 = ()

## 2. 선형리스트의 저장과 원소 삽입

### 1) 선형 리스트의 저장

- 원소들 간의 논리적인 순서와 동일한 순서로 메모리에 저장

#### (1) 순차 자료구조

- 원소들이 논리적 순서대로 메모리에 연속적으로 저장

##### 동창 리스트가 실제 저장된 물리적 구조

![alt](/assets/images/post/ComputerStudy/113.png)

#### (2) 순차 자료구조의 원소 위치 계산

- 선형 리스트가 저장된 시작 위치 a
- 원소의 크기 l
- i번째 원소의 위치 = a + (i -1) X l

### 2) 선형리스트에서의 원소의 삽입

- 선형리스트 중간에 원소를 삽입하려면 삽입할 위치 이후의 원소들을 모두 한자리씩 뒤로 밀어야 함.

![alt](/assets/images/post/ComputerStudy/114.png)

#### (1) 원소 삽입 방법

- 원소를 삽입할 빈 자리 만들기
  - 삽입할 자리 이후의 원소들을 한자리씩 뒤로 자리 이동
- 준비한 빈 자리에 원소 삽입

![alt](/assets/images/post/ComputerStudy/115.png)

#### (2) 삽입할 자리를 만들기 위한 이동 횟수

- (n+1)개의 원소로 이루어진 선형리스트에서 k번 자리에 원소를 삽입할 경우
  - : k번 원소부터 마지막 인덱스 n번까지 (n-k+1)개의 원소를 이동
- n-k+1 = 마지막 원소의 인덱스 - 삽입할 자리의 인덱스 + 1

## 3. 선형리스트 삭제

- 선형리스트 중간에서 원소를 삭제하려면 삭제한 위치 이후의 원소들을 모두 한자리씩 앞으로 이동

![alt](/assets/images/post/ComputerStudy/116.png)

### 1) 원소 삭제 방법 - 삽입 역순

- 원소 삭제
- 삭제한 빈 자리 채우기 (삭제한 자리 이후 원소들은 한자리씩 앞으로 이동)

![alt](/assets/images/post/ComputerStudy/117.png)

### 2) 삭제한 후 자리를 채우기 위한 이동 횟수

- (n+1)개의 원소로 이루어진 선형리스트에서 k번 자리의 원소를 삭제한 경우
  - : (k+1)번 원소부터 마지막 n번 원소까지 n-(k+1) + 1 개의 원소를 이동
- n-(k+1)+1 = n-k = 마지막 원소의 인덱스 - 삭제한 자리의 인덱스
