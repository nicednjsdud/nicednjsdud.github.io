---
title: (자료구조) 12-2 그래프 순회, 그래프 탐색 (너비 우선 탐색 BFS)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 그래프 순회, 그래프 탐색
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-12 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 그래프 순회, 그래프 탐색 (너비 우선 탐색 BFS)

## 1. 너비 우선 탐색 (Breadth First Search : BFS)

### 1) 순회 방법

- 시작 정점으로부터 **인접한 정점들을 모두 차례로 방문**하고 나서, **방문했던 정점을 시작**으로 하여 다시 인접한  
  정점들을 차례로 방문하는 방식
- 가까운 정점들을 먼저 방문하고 멀리 있는 정점들은 나중에 방문하는 순회방법
- 인접한 정점들에 대해서 차례로 다시 너비 우선 탐색을 반복해야 하므로 **선입선출의 구조를 갖는 큐**를 사용

### 2) 너비 우선 탐색 알고리즘

```c
  BFS(v)
      for(i <- 0; i<n; i <- i+1) do{
            visited[i] <- false;
      }
      Q <- createQueue();
      visited[v] <- true;
      v 방문;
      while(not isEmpty(Q)) do{
          while(visited[v의 인접 정점 w] = false) do{
                visitied[w] <- true;
                w 방문;
                enQueue(Q,w);
          }
          v <- deQueue(Q);
      }
  end BFS()
```

### 3) 너비 우선 탐색 예

#### (1) 초기상태 : 배열 visited를 False로 초기화하고, 공백 큐를 생성

![alt](/assets/images/post/ComputerStudy/648.png)

#### (2) 정점 A를 시작으로 너비 우선 탐색을 시작함

```c
  visited[A] <- true;
  A 방문;
```

![alt](/assets/images/post/ComputerStudy/649.png)

#### (3) 정점 A의 방문 안한 모든 인접정점 B,C 방문

- 정점 A의 방문 안 한 모든 인접 정점 B,C를 방문하고, 큐에 enQueue함
- `visited[(A의 방문 안한 인접정점 B와 C)]` <- true;
- (A의 방문 안한 인접정점 B와 C) 방문
- enQueue(Q, (A의 방문 안한 인접 정점 B와 C));

![alt](/assets/images/post/ComputerStudy/650.png)

#### (4) 정점 A에 대한 인접정점들을 처리했으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 B를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/651.png)

#### (5) 정점 B의 방문 안한 모든 인접정점 D,E 방문

- 정점 B의 방문 안 한 모든 인접 정점 D,E를 방문하고, 큐에 enQueue함
- `visited[(B의 방문 안한 인접정점 D와 E)]` <- true;
- (B의 방문 안한 인접정점 D와 E) 방문
- enQueue(Q, (B의 방문 안한 인접 정점 D와 E));

![alt](/assets/images/post/ComputerStudy/652.png)

#### (6) 정점 B에 대한 인접정점들을 처리했으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 C를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/653.png)

#### (7) 정점 C에는 방문 안한 인접정점이 없으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 D를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/654.png)

#### (8) 정점 D의 방문 안한 모든 인접정점 G 방문

- 정점 D의 방문 안 한 모든 인접 정점 G를 방문하고, 큐에 enQueue함
- `visited[(D의 방문 안한 인접정점 G)]` <- true;
- (D의 방문 안한 인접정점 G) 방문
- enQueue(Q, (D의 방문 안한 인접 정점 G));

![alt](/assets/images/post/ComputerStudy/655.png)

#### (9) 정점 D에 대한 인접정점들을 처리했으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 D를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/656.png)

#### (10) 정점 E에는 방문 안한 인접정점이 없으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 G를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/657.png)

#### (11) 정점 G의 방문 안한 모든 인접정점 F 방문

- 정점 G의 방문 안 한 모든 인접 정점 F를 방문하고, 큐에 enQueue함
- `visited[(G의 방문 안한 인접정점 F)]` <- true;
- (G의 방문 안한 인접정점 F) 방문
- enQueue(Q, (G의 방문 안한 인접 정점 F));

![alt](/assets/images/post/ComputerStudy/658.png)

#### (12) 정점 G에 대한 인접정점들을 처리했으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue하여 정점 F를 구함

```c
  v <- deQueue(Q);
```

![alt](/assets/images/post/ComputerStudy/659.png)

#### (13) 정점 F에는 방문 안한 인접정점이 없으므로

- 너비 우선 탐색을 계속할 다음 정점을 찾기 위해 큐를 deQueue해야 하는데
- 큐가 공백이므로 너비 우선 탐색을 종료함

![alt](/assets/images/post/ComputerStudy/660.png)
