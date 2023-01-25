---
title: (자료구조) 14-2 이진 트리 검색
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

# 자료 구조 - 이진 트리 검색

## 1. 이진 트리 검색

- 이진 탐색 트리를 사용한 검색 방법
- 이진 탐색 트리는 **루트 노드를 기준으로 왼쪽 서브 트리는 루트 노드보다 킷값이 작은 원소**들로 구성
- **오른쪽 서브 트리는 루트 노드보다 킷값이 큰 원소**들로 구성한 이진 트리

### 1) 정의

- 이진 탐색 트리의 특성을 이용하여 검색은 용이
- 원소의 삽입이나 삭제 연산에 대해서 **항상 이진 탐색 트리를 재구성하는 작업 필요**

### 2) 이진 탐색 트리의 검색 연산

#### (1) 루트에서 시작

#### (2) 탐색할 킷값 x를 루트 노드의 킷값과 비교함

- **(킷값 x = 루트 노드의 킷 값)**인 경우 : 원하는 원소를 찾았으므로 탐색연산 성공
- **(킷값 x < 루트 노드의 킷 값)**인 경우 : 루트노드의 왼쪽 서브트리에서 탐색연산 수행
- **(킷값 x > 루트 노드의 킷 값)**인 경우 : 루트노드의 오른쪽 서브트리에서 탐색연산 수행

### 3) 탐색 연산 알고리즘

```c
  searchBST(bsT, x)
      p <- bsT;
      if (p = null) then return null;
      if (x = p.key) then return p;
      if (x < p.key) then return searchBST(p.left, x);
      else return searchBST(p.right, x);
  end searchBST()
```

### 4) 탐색 연산 예제 - 원소 11 탐색하기

![alt](/assets/images/post/ComputerStudy/791.png)

#### (1) 찾는 킷 값 11을 루트노드의 킷값 8과 비교

- **(찾는 킷 값 11 > 노드의 킷 값 8)**이므로 오른쪽 서브트리를 탐ㅎ색

#### (2) (찾는 킷 값 11 > 노드의 킷 값 10) 이므로

- 다시 오른쪽 서브트리를 탐색

#### (3) (찾는 킷 값 11 < 노드의 킷값 14) 이므로

- 왼쪽 서브트리를 탐색

#### (4) (찾는 킷 값 11 = 노드의 킷 값 11) 이므로

- 탐색 성공
