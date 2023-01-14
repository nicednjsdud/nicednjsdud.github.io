---
title: (자료구조) 12-3 신장트리와 최소비용 신장트리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 신장트리와 최소비용 신장트리
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-14 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 신장트리와 최소비용 신장트리

## 1. 신장트리와 최소비용 신장트리의 개요

### 1) 신장트리 (Spanning tree)

- n개의 정점으로 이루어진 무방향 그래프 G에서 n개의 모든 정점과 n-1개의 간선으로 만들어진 트리

#### (1) 그래프 G1과 신장트리의 예

![alt](/assets/images/post/ComputerStudy/661.png)

#### (2) 깊이 우선 신장 트리

- depth first spanning
- 깊이 우선 탐색을 이용하여 생성된 신장 트리

#### (3) 너비 우선 신장 트리

- breadth first spanning
- 너비 우선 탐색을 이용하여 생성된 신장 트리

#### (4) 깊이 우선 신장 트리와 너비 우선 신장 트리

![alt](/assets/images/post/ComputerStudy/662.png)

#### (5) 신장 트리

- 신장 트리는 결국 최소의 간선을 이용하여 모든 정점을 연결하는 그래프
- 최소의 도로를 사용하여 모든 도시를 연결해야 하는 도로망 건설이나 최소의 네트워크 선을 사용하여 시스템을 연결해야  
  하는 통신망 설계 등의 여러분야에 응용됨

### 2) 최소 비용 신장 트리 (minimum cost spanning tree)

- 무방향 가중치 그래프에서 신장 트리에 구성하는 간선들의 가중치 합이 최소인 신장 트리
- 가중치 그래프의 간선에 주어진 가중치 : 비용, 거리, 시간을 의미하는 값

#### (1) 최소 비용 신장 트리를 만드는 알고리즘

- Kruskal 알고리즘
- Prime 알고리즘
