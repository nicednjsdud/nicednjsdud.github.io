---
title: (알고리즘) 바킹독의 실전 알고리즘 0x09강 ( BFS )
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
last_modified_at: "2024-03-16 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x09강 ( BFS )

## 목차

- 0x00 알고리즘 설명
- 0x01 예시
- 0x02 응용 1 - 거리측정
- 0x03 응용 2 - 시작점이 여러개 일 때
- 0x04 응용 3 - 시작점이 두 종류일 때
- 0x05 응용 4 - 1차원에서의 BFS

## 1. 알고리즘 설명

- 그림에서 처럼 물고기에 색깔을 바꿀수 있다.
- 페인트 기능은 외부 윤곽선을 따라서 구분되는 영역의 색을 한꺼번에 바꾸는 것
- 이런걸 **Flood Fill**이라고 부른다.

![alt](/assets/images/post/ComputerStudy/1099.png)

### 1) Flood Fill을 어떻게 구현할까?

1. 클릭한 칸의 상하좌우를 보며 나와 색이 같은지 확인한다.
2. 같은 칸의 대해서 또 상하좌우를 확인

### 2) BFS(Breadth First Search)

- **다차원 배열에서 각 칸을 방문할때 너비를 우선으로 방문하는 알고리즘**

![alt](/assets/images/post/ComputerStudy/1100.png)

- 정확한 정의는 정점과 간선으로 이루어진 자료구조

## 2. 예시

1. BFS 알고리즘에서는 좌표를 담을 큐가 필요
2. 우선 (0,0)에 방문했다는 표시를 남기고 해당 칸을 큐에 넣는다.

![alt](/assets/images/post/ComputerStudy/1101.png)

3. 초기 세팅이 끝난후에는 큐가 빌 때까지 계속 큐의 front를 빼고 해당 좌표의 상하좌우를 살펴보면서  
   큐에 넣어주는 작업을 반복

4. 지금 세팅에서 (0,0)이고 pop을 하고 상하좌우를 살펴봄
   1. 우리는 파란색 칸이면서 아직 방문하지 않은 칸을 찾음

![alt](/assets/images/post/ComputerStudy/1102.png)

5. (0.1), (1.0)은 아직 방문하지 않은 칸이므로 , 방문했다는 표시를 남기고 큐에 넣음

![alt](/assets/images/post/ComputerStudy/1103.png)

6. 현재 (0.1)에 위치하며 pop을 함

![alt](/assets/images/post/ComputerStudy/1104.png)

7. 다음 방문할 위치를 찾음
   1. (0.0)은 파란칸이지만 이미 **방문**을 했음
   2. (1,1)은 빨간 칸임
   3. 유일하게 (0.2)만 방문하지 않고 파란칸임 (표시 남기기)

![alt](/assets/images/post/ComputerStudy/1105.png)

### 1) 설명

1. 시작하는 칸을 큐에 넣고 방문했다는 표시를 남김
2. 큐에서 원소를 꺼내어 그 칸에 상하좌우로 인접하는 칸에 대해 3번을 진행
3. 해당 칸을 이전에 방문 했다면 아무것도 하지않고, 처음으로 방문했다면 방문했다는 표시를 남김
4. 큐가 빌 때까지 2번을 반복

- 모든 칸이 큐에 1번씩 들어가므로 시간복잡도는 칸이 N개 일때 **O(N)**

### 2) 코드

```c
#include <bits/stc++.h>
using namespace std;
#define X first
#define Y second

int board[502][502] = {...};      // 1이면 파란칸 0이면 빨간칸
bool vis[502][502];               // 방문 여부 저장할 변수
int n = 7, m = 10;                // 행과 열의 갯수
int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};           // dx, dy는 상하좌우를 영리하게 처리하기 위한 변수

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  queue<pair<int,int>> Q;
  vis[0][0] = 1;                  // (0,0) 방문처리
  Q.push({0,0});

  while(!Q.empty()){              // Q가 빌때까지 상하좌우의 칸을 추가하는걸 반복
    pair<int,int> cur = Q.front(); Q.pop();   // 큐의 front를 cur에 저장하고 pop을함
    cout << '(' << cur.X << ', ' << cur.Y << ') -> ';
    for(int dir = 0; dir<4; dir ++){
        int nx = cur.X + dx[dir];          //
        int ny = cur.Y + dy[dir];

        if(nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
        if(vis[nx][ny] || board[nx][ny] != 1) continue;
        vis[nx][ny] = 1;
        Q.push({nx,ny});
    }
  }
}
```

### 3) 실수하는 점

#### 3-1) 시작점에 방문했다는 표시를 남기지 않는다.

- 이렇게 하면 시작점을 두 번 방문할 수 있다.

#### 3-2) 큐에 넣을 때 방문했다는 표시를 하는 대신 큐에서 빼낼때 방문했다는 표시를 남겼다.

- 이렇게 되면 같은 칸이 큐에 여러번 들어가게 되어서 시간 초과나 메모리 초과가 나올 수 있다.

#### 3-3) 이웃한 원소가 범위를 벗어났는지에 대한 체크를 잘못했다.

- 위에 코드에서 있던 nx, ny가 배열 바깥으로 벗어났는지에 대한 루틴을 아예 빼먹거나, 이상하게 구현 했을 때

### 4) BOJ

#### 4-1) BOJ 1926번 : 그림

1. 상하좌우로 연결된 그림의 크기 알아내기
2. 도화지에 있는 모든 그림을 찾아내기

- java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_1926/">BackJoon Algorithm 그림 1926 (Java)</a>

- c

```c
#include <bits/stc++.h>
using namespace std;
#define X first
#define Y second

int board[502][502] = {...};      // 1이면 파란칸 0이면 빨간칸
bool vis[502][502];               // 방문 여부 저장할 변수
int n, m;                // 행과 열의 갯수
int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};           // dx, dy는 상하좌우를 영리하게 처리하기 위한 변수

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  for(int i = 0; i< n; i++)
    for(int j = 0; j< m; j++)
        cin >> board[i][j]
  int mx = 0;     // 그림의 최댓값
  int num = 0;    // 그림의 수

  for(int i =0; i<n;i++){
    for(int j = 0; j< m ; j++){
        if(board[i][j] == 0 || vis[i][j]) continue;
        num ++;
        queue<pair<int,int>> Q;
        vis[i][j] = 1;
        Q.push({i,j});
        int area = 0;
        while(!Q.empty()){
          area ++;
          pair<int,int> cur = Q.front(); Q.pop();
          for(int dir = 0; dir <4 ; dir ++){
            int nX = cur.X + dx[dir];
            int nY = cur.Y + dy[dir];

            if(nX < 0 || nY < 0 || nX >= n || nY >= m) continue;
            if(vis[nX][nY] || board[nX][nY] != 1) continue;
            vis[nX][nY] = 1;
            Q.push({nX,nY});
          }
        }
        mx = max(mx, area);
    }
  }
  cout << num << '\n' << mx;
}
```

#### 4-2) BOJ 2178번 : 미로 탐색

![alt](/assets/images/post/ComputerStudy/1106.png)

- 방문 했다는 표시 대신 각 칸들에 (0,0) 까지의 거리를 적어놨음

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_2178/">BackJoon Algorithm 미로탐색 2178 (Java)
</a>

#### 4-3) BOJ 7576 : 토마토

- 입력을 받으면서 익은 토마토는 큐에 넣고, 익지 않은 토마토는 dist값을 -1로 둠

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_7576/">BackJoon Algorithm 토마토 7576 (Java)
</a>

#### 4-4) BOJ 4179 : 불 !

<a href="">풀예정</a>

#### 4-5) BOJ 1697번 : 숨바꼭질

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_1697/">BackJoon Algorithm 숨바꼭질 1697 (Java)
</a>

## 출처

<a href="https://www.youtube.com/watch?v=ftOmGdm95XI&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=10">[바킹독의 실전 알고리즘] 0x08강 - 스택의 활용</a>
