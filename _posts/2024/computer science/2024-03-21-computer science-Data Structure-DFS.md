---
title: (알고리즘) 바킹독의 실전 알고리즘 0x0A강 ( DFS )
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 바킹독의 실전 알고리즘
tag: BackJoon
article_tag1: BackJoon
article_section: BackJoon
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2024-03-21 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x09강 ( DFS )

## 목차

- 0x00 알고리즘 설명
- 0x01 예시
- 0x02 BFS vs DFS

## 1. 알고리즘 설명

### 1) DFS (Depth First Search)

- 다차원 배열에서 각 칸을 방문할 때 깊이를 우선으로 방문하는 알고리즘

### 2) BFS (Breadth First Search)

- 다차원 배열에서 각 칸을 방문할 때 너비를 우선으로 방문하는 알고리즘

## 2. 예시

1. 시작하는 칸을 스택에 넣고 방문했다는 표시를 남김
2. 스택에서 원소를 꺼내어 그 칸과 상하좌우로 인접한 칸에 대해 3번을 진행
3. 해당 칸을 이전에 방문했다면 아무 것도 하지 않고, 처음으로 방문했다면 방문했다는 표시를 남기고 해당 칸을 스택에 삽입
4. 스택에 이 빌 때 까지 2번을 반복

- 모든 칸이 스택에 1번씩 들어가므로 시간복잡도는 칸이 N개 일때 **O(N)**
