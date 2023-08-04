---
title: (10분 테크톡) Index
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: Process vs Thread
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-08-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 목차

## 1. Index란

- 데이터베이스의 검색 속도를 향상 시키기 위한 자료 구조

![alt](/assets/images/post/ComputerStudy/1066.png)

## 2. B-tree

- Balanced tree

1. 균형 트리
2. 탐색 트리 (정렬)
3. 하나의 노드에 여러 정보 저장 기능
4. 두개 이상의 자식을 가질 수 있다.

### 1) 균형 트리

- 한쪽으로 치우쳐저 있지 않음

![alt](/assets/images/post/ComputerStudy/1067.png)

### 2) 탐색 트리

![alt](/assets/images/post/ComputerStudy/1068.png)

- 검색성의 최대한 끌어올리기 때문에 쓰기성능을 떨어짐

![alt](/assets/images/post/ComputerStudy/1069.png)

### 3) 하나의 노드에 여러 정보 저장 기능 , 두개 이상의 자식을 가질 수 있음

![alt](/assets/images/post/ComputerStudy/1070.png)

## 3. Index의 종류

1. Clustered Index
2. Non-clustered Index

### 1) Clustered Index ( = PK Index)

- Clustered : 무리, 군집

![alt](/assets/images/post/ComputerStudy/1071.png)

- 실제 데이터와 군집(강한 연관)을 이루는 인덱스
- 데이터가 테이블에 물리적으로 저장되는 순서를 정의
- PK로 설정하면, 자동으로 생성 or Unique and Not null 제약 조건을 생성

![alt](/assets/images/post/ComputerStudy/1072.png)

1. 데이터 정렬
2. Index의 리프 페이지가 실제 데이터
3. 테이블당 1개만 존재

### 2) Non-clustered Index

- Index 생성 SQL

```sql
  CREATE INDEX name_index ON restaurant(name)
```

- or Unique 제약 조건을 생성

![alt](/assets/images/post/ComputerStudy/1073.png)

1. 인덱스와 데이터 페이지가 따로 존재
2. 리프 페이지에선 데이터주소를 가짐
3. 데이터페이지가 정렬되지 않아도 된다.
4. 한 테이블에 여러개가 존재할 수 있다.

## 4. Clustered & Non-clustered

- PK column을 설정하여 테이블을 생성한 뒤 ( => Clustered Index)
- 자주 발생하는 조회 column에 대해 index를 추가하면 (=> Non-Clustered Index)
- 이런 케이스에선 어떻게 동작할까요

![alt](/assets/images/post/ComputerStudy/1074.png)

## Index는 어디에 ?

1. WHERE, JOIN 조건에 자주 발생하는 컬럼들
2. INSERT, UPDATE, DELETE 적게 발생하는 컬럼
3. 중복도가 낮은 컬럼
4. 범위 검색이 적은 컬럼
5. 데이터가 많은 테이블

## 출처

<a href="https://www.youtube.com/watch?v=ywYdEls88Sw&t=9s">로이스의 Index</a>
