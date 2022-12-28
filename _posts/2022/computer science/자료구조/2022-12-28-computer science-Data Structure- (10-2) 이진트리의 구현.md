---
title: (자료구조) 10-2 이진트리의 구현
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 이진트리의 구현
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-12-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 이진트리의 구현

## 1. 1차원 배열의 순차 자료구조 사용

- 높이가 h인 포화 이진 트리의 노드 번호를 배열을 인덱스로 사용
- 인덱스 0번 : 실제로 사용하지 않고 비워둠
- 인덱스 1번 : 루트 저장

### 1) 완전 이진 트리의 1차원 배열 표현

![alt](/assets/images/post/ComputerStudy/490.png)

### 2) 왼쪽 편향 이진 트리의 1차원 배열 표현

![alt](/assets/images/post/ComputerStudy/491.png)

### 3) 이진 트리의 1차원 배열에서의 인덱스 관계

![alt](/assets/images/post/ComputerStudy/492.png)

### 4) 이진 트리의 순차 자료구조 표현의 단점

- 편향 이진 트리의 경우에 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생
- 트리의 원소 삽입, 삭제에 대한 배열의 크기 변경 어려움

## 2. 연결자료구조를 이용한 이진트리의 구현

### 1) 단순 연결 리스트를 사용하여 구현

- 이진 트리의 모든 노드는 최대 2개의 자식 노드를 가지므로 일정한 구조의 단순 연결 리스트 노트를 사용하여 구현

![alt](/assets/images/post/ComputerStudy/493.png)

#### (1) 이진 트리의 노드 구조에 대한 C 구조체 정의

```c
  typedef struct treeNode{
        char data
        struct treeNode *left
        struct treeNode *right
  } treeNode
```

![alt](/assets/images/post/ComputerStudy/494.png)

## 3. 완전 이진 트리의 단순 연결 리스트 표현

![alt](/assets/images/post/ComputerStudy/495.png)

### 1) 왼쪽 편향 이진 트리의 단순 연결 리스트 표현

![alt](/assets/images/post/ComputerStudy/496.png)
