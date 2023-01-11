---
title: (자료구조) 12-2 그래프 순회, 그래프 탐색 (깊이 우선 탐색 DFS)
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

# 자료 구조 - 그래프 순회, 그래프 탐색

## 1. 그래프 순회, 그래프 탐색

### 1) 가장 일반적인 자료구조 형태

- 전기회로의 소자 간 연결 상태
- 운영체제의 프로세스와 자원 관계
- 지도에서 도시들의 연결 상태

### 2) 그래프 순회

- 그래프의 가장 기본적인 연산
- 하나의 정점에서 시작하여 그래프에 있는 모든 정점을 한번씩 방문하여 처리하는 연산

#### (1) 그래프 탐색으로 해결 가능한 문제

- 도로망에서 특정 도시에서 다른 도시로 갈 수 있는지 여부
- 전자회로에서 특정 단자와 다른 단자가 서로 연결되어 있는지 여부

![alt](/assets/images/post/ComputerStudy/636.png)

#### (2) 그래프 탐색 방법

- 깊이 우선 탐색 (Depth First Search : DFS)
- 너비 우선 탐색 (Breadth First Search : BFS)

### 3) 그래프 순회 예제

#### (1) 깊이 우선 탐색 DFS

- 한 지점을 골라서 팔수 있을 때까지 계속해서 깊게 파다가 아무리 땅을 파도 물이 나오지 않으면, 밖으로 나와  
  다른 지점을 골라서 다시 깊게 땅을 파는 방법

#### (2) 너비 우선 탐색 BFS

- 여러 지점을 고르게 파보고 물이 나오지 않으면, 파놓은 구덩이들을 다시 좀 더 깊게 파는 방법

## 2. 깊이 우선 순회

### 1) 깊이 우선 탐색

- **시작 정점**의 한 방향으로 **갈 수있는경로가 있는 곳까지** 깊이 탐색해가다가 더이상 갈 곳이 없게 되면,
- 가장 **마지막에 만났던 갈림길 간선**이 있는 정점으로 되돌아와서 다른 방향의 간선으로 탐색을 계속 반복
- **결국 모든 정점을 방문하는 순회방법**
- **가장 마지막에 만났던 갈림길 간선의 정점으로 가장 먼저 되돌아**가서 다시 깊이 우선탐색 반복
- 후입선출 구조의 **스택** 사용

#### (1) 수행 순서

##### (1-1) 시작 정점 v를 결정하여 방문

##### (1-2) 정점v에 인접한 정점 중에서

- 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문하며, w를 v로 하여 다시 반복
- 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로하여  
  다시 반복

#### (2) 깊이 우선 탐색 알고리즘

```c
  DFS(v)
      for (i <- 0; i < n; i <- i+1) do{
          visited[i] <- false;
      }
      stack <- createStack();
      visited[v] = true;
      v 방문;
      while (not isEmpty(stack)) do{

          if (visited[v의 인접 정점 w] = false) then {
            push(stack,v);
            visited[w] <- true;
            w 방문;
            v <- w;
          }
          else v <- pop(stack);
      }
  end DFS()
```

### 2) 깊이 우선 탐색 예

#### (1) 초기상태

- 배열 visited를 False로 초기화, 공백스택 생성

![alt](/assets/images/post/ComputerStudy/637.png)

#### (2) 정점 A를 시작으로 깊이 우선 탐색 시작

- `visited[A]` <- true

![alt](/assets/images/post/ComputerStudy/638.png)

#### (3) 정점 A에 방문하지 않은 정점 B,C가 있으므로

- A를 스택에 push하고, 인접정점 B와 C중에서 오름차순에 따라 B를 선택하여 탐색을 계속함

```c
  push(stack, A);
  visited[B] <- true;
  B 방문;
```

![alt](/assets/images/post/ComputerStudy/639.png)

#### (4) 정점 B에 방문하지 않은 정점 D,E가 있으므로

- B를 스택에 push하고, 인접정점 D와 E 중에서 오름차순에 따라 D를 선택하여 탐색을 계속함

```c
  push(stack,B);
  visited[D] <- true;
  D 방문;
```

![alt](/assets/images/post/ComputerStudy/640.png)

#### (5) 정점 D에 방문하지 않은 정점 G가 있으므로

- D를 스택에 push하고, 인접정점 G를 선택하여 탐색을 계속함

```c
  push(stack, D);
  visited[G] <- true;
  G 방문;
```

![alt](/assets/images/post/ComputerStudy/641.png)

#### (6) 정점 G에 방문하지 않은 정점 E,F가 있으므로

- G를 스택에 push 하고, 인접정점 E와 F중에서 오름차순에 따라 E를 선택하여 탐색을 계속함

```c
  push(stack, G);
  visited[E] <- true;
  E 방문;
```

![alt](/assets/images/post/ComputerStudy/642.png)

#### (6) 정점 E에 방문하지 않은 정점 C가 있으므로

- E를 스택에 push 하고, 인접정점 C를 선택하여 탐색을 계속함

```c
  push(stack, E);
  visited[C] <- true;
  C 방문;
```

![alt](/assets/images/post/ComputerStudy/643.png)

#### (7) 정점 C에서 방문하지 않은 인접정점이 없으므로

- 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 E에 대해서 방문하지 않은 인접정점이 있는지 확인

```c
  pop(stack);
```

![alt](/assets/images/post/ComputerStudy/644.png)

#### (8) 정점 E에서 방문하지 않은 인접정점이 없으므로

- 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 G에 대해서 방문하지 않은 인접정점이 있는지 확인

```c
  pop(stack);
```

![alt](/assets/images/post/ComputerStudy/645.png)

#### (9) 정점 G에 방문하지 않은 정점 F가 있으므로

- G를 스택에 push 하고, 인접정점 F를 선택하여 탐색을 계속함

```c
  push(stack, G);
  visited[F] <- true;
  F 방문;
```

![alt](/assets/images/post/ComputerStudy/646.png)

#### (10,11,12,13) 방문하지 않은 인접 정점이 없으므로

- 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 G에 대해서 방문하지 않은 인접정점이 있는지 확인

```c
  pop(stack);
```

#### (14) 현재 정점 A에서 방문하지 않은 인접 정점이 없으므로

- 마지막 정점으로 돌아가기위해 스택을 pop하는데, 스택이 공백이므로 깊이 우선 탐색 종료

![alt](/assets/images/post/ComputerStudy/647.png)
