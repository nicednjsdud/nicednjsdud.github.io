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

# 바킹독의 실전 알고리즘 0x0A강 ( DFS )

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

### 1) C

```c
#include <bits/stc++.h>
using namespace std;
#define X first
#define Y second
int board[502][502] = {...};
bool vis[502][502];
int n = 7, m = 10;
int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  stack<pair<int,int>> S;
  vis[0][0] = 1;
  S.push({0,0});

  while(!s.empty()){
    pair<int,int> cur = S.top(); S.pop();
    cout << '(' << cur.X << ", " << cur.Y << ") -> ";
    for(int dir = 0; dir < 4; dir ++){
      int nX = cur.X + dx[dir];
      int nY = cur.Y + dy[dir];

      if(nX < 0 || nY < 0 || nX >= n || nY >= m ) continue;
      if(vis[nX][nY] || board[nX][nY] != 1) continue;
      vis[nX][nY] = 1;
      S.push({nX,nY});
    }
  }
}
```

## 3. BFS vs DFS

### 1) BFS

- 냇가에 던진 돌로 인해 동심원이 생기 듯이 퍼지는 것 처럼 상하좌우로 퍼짐
- 거리 순으로 방문

![alt](/assets/images/post/ComputerStudy/1107.png)

### 2) DFS

- 한 방향으로 막힐 때까지 쭉 직진

![alt](/assets/images/post/ComputerStudy/1108.png)

### 3) 정리

![alt](/assets/images/post/ComputerStudy/1110.png)

- BFS에서 유용하게 썻던 "현재 보는 칸으로부터의 수가되는 인접한 칸은 거리가 현재 보는 칸보다 1만큼 더 떨어져있다"는 성질은  
  DFS에서는 성립하지 않음

- 거리를 계산할때는 DFS를 사용할 수 없음

1. 거리측정은 BFS
2. Flood Fill은 아무거나 써도 상관 없음
3. 그래프와 트리에서는 DFS를 씀

## 출처

<a href="https://www.youtube.com/watch?v=93jy2yUYfVE&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=11">[바킹독의 실전 알고리즘] 0x0A강 - DFS</a>
