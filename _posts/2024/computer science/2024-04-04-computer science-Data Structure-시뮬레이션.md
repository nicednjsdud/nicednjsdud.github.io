---
title: (알고리즘) 바킹독의 실전 알고리즘 0x0D강 ( 시뮬레이션 )
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
last_modified_at: "2024-04-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x0D강 ( 시뮬레이션 )

## 목차

- 0x00 연습 문제 1 - 감시
- 0x01 연습 문제 2 - 스티커 붙이기
- 0x02 연습 문제 3 - 2048 (Easy)
- 0x03 연습 문제 4 - 치킨 배달


## 1. 연습 문제 1 - 감시 BOJ 15683

1. 각 cctv의 방향 정하기
2. 정한 방향에 대해서 사각 지대의 크기를 구하기

### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;
#define X first
#define Y second

int dx[4] = {1,0,-1,0};
int dy[4] = {0,1,0,-1};
int n,m;
int board1[10][10];
int board2[10][10];
vector<pair<int,int>> cctv;

bool OOB(int a, int b){
  return a < 0 || a >= n || b < 0 || b >= m;
}

void upd(int x, int y, int dir){
  dir %= 4;
  while(1){
    x += dx[dir];
    y += dy[dir];
    if(OOB(x,y) || board2[x][y] == 6) return;
    if(board2[x][y] != 0) continue;
    board2[x][y] = 7;
  }
}

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  int mn = 0;
  for(int i = 0; i < n ; i++){
    for(int j = 0; j< m; j++){
      cin >> board1[i][j];
      if(board1[i][j] != 0 && board[i][j] != 6)
        cctv.push_back({i,j});
      if(board1[i][j] == 0) mn++;
    }
  }
  for(int tmp = 0; tmp < (1<<(2 * cctv.size())); tmp ++){

    for(int i = 0; i< n; i++)
      for(int j = 0; j< m ; j++)
        board2[i][j] = board1[i][j];
    int brute = tmp;
    for(int i = 0; i< cctv.size(); i++){
      int dir = brute % 4;
      brute /= 4;
      int x = cctv[i].X;
      int y = cctv[i].Y;
      if(board1[x][y] == 1){
        upd(x,y,dir);
      }
      else if(board1[x][y] == 2){
        upd(x,y,dir);
        upd(x,y,dir + 2);
      }
      else if(board1[x][y] == 3){
        upd(x,y,dir);
        upd(x,y,dir+1);
      }
      else if(board1[x][y] == 4){
        upd(x,y,dir);
        upd(x,y,dir+1);
        upd(x,y,dir+2);
      }
      else{
        upd(x,y,dir);
        upd(x,y,dir+1);
        upd(x,y,dir+2);
        upd(x,y,dir+3);
      }
    }
    int val = 0;
    for(int i = 0; i< n; i++)
      for(int j = 0; j< m ; j++)
          val += (board2[i][j] == 0);
    mn = min(mn,val);
  }
  cout << mn;
}
```

### 1-2) Java

* 업로드 예정

## 2. 연습문제 2 - 스티커 붙이기 BOJ 18808

