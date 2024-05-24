---
title: (알고리즘) 바킹독의 실전 알고리즘 0x0C강 ( 백트래킹 )
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
last_modified_at: "2024-03-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x0B강 ( 재귀 )

## 목차

- 0x00 알고리즘 설명
- 0x01 연습 문제 1 - N과 M
- 0x02 연습 문제 2 - N-Queen
- 0x03 연습 문제 3 - 부분수열의 합
- 0x04 STL next_permutation

## 1. 알고리즘 설명

- 현재 상태에서 모든 후보군을 따라 들어가며 탐색하는 알고리즘

## 2. 연습 문제

### 1) BOJ 15649번 : N과 M (1)

1. 첫 번째 원소로 1이 쓰였으니 두번째 원소로는 2,3,4가 가능
2. 먼저 2를 쓴다.
3. 1, 2가 채워진 상태까지 온거고 마지막 원소로는 일단 3을 넣음
4. 모든 칸이 찼으면 수열을 완성한거니 출력하고 여기서는 이전 상태로 되돌아가야 한다.

![alt](/assets/images/post/ComputerStudy/1114.png)

3. 되돌아가기 위해 마지막 원소를 빼고 다시 마지막 원소를 채워야하는데 지금 여기서는 3 혹은 4가 가능한 상황
4. 이미 3은 확인했으니 4을 넣은 상태로 이동하면 된다.
5. 이렇게 해서 1 2 4도 얻어냄

![alt](/assets/images/post/ComputerStudy/1115.png)

6. 마지막 칸으로 올수 있는 3과 4를 다 넣어봤으니 지금 할수 있는건 다 한 상태이므로 이전으로 되돌아감
7. 두번째 칸에 3을 넣은 상태로 감
8. 현재 아직 사용하지 않은 칸은 2와 4이므로 마지막칸에 2를 넣어보고 되돌아와 4을 넣음

![alt](/assets/images/post/ComputerStudy/1116.png)

#### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n,m;
int arr[10];
bool inused[10];

void func(int k){
  if(k == m)
    for(int i = 0; i< m; i++){
      cout << arr[i] << ' ';
    cout << '\n'
    return;
  }

  for(int i = 0; i<n; i++){
    if(!isused[i]){
      arr[k] = i;
      isused[i] = 1;
      func(k+1);
      isused[i] = 0;
    }
  }
}

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  func(0);
}
```

#### 1-2) Java

<a href=""></a>

### 2) BOJ 9663번 : N-Queen

![alt](/assets/images/post/ComputerStudy/1117.png)

#### 2-1) C

```c

#include <bits/stdc++.h>
using namespace std;
bool isused1[40];
bool isused2[40];
bool isused3[40];


int cnt = 0;
int n;
// cur번째 행에 말을 배치할 예정
void func(int cur){
  if(cur == n){
    cnt++;
    return;
  }
  for(int i = 0; i < n; i++){
      if( isused[i] || isused2[i + cur] || isused3[cur - i + n - 1]) continue;

      isused1[i] = 1;
      isused2[i+cur] = 1;
      isused3[cur-i+n-1] = 1;
      func(cur + 1);
      iisused1[i] = 0;
      isused2[i+cur] = 0;
      isused3[cur-i+n-1] = 0;
  }
}

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n
  func(0);
  cout << cnt;
}
```

#### 2-2) Java

- 풀 예정

### 3) BOJ 1182번 : 부분수열의 합

#### 3-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n, s;
int arr[30];
int cnt = 0;
void func(int cur, int tot){
  if(cur == n){
    if(tot == s) cnt ++;
    return;
  }
  func(cur+1, tot);
  func(cur+1, tot + arr[cur] );
}
int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> s;
  for(int i = 0; i < n ; i++)
    cin >> arr[i];
  func(0,0);
  if(s == 0) cnt--;
  cout << cnt;
}
```

#### 3-2) Java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_1182/">BackJoon Algorithm 1182 부분 수열의 합 (Java)
</a>

## 3. STL next_permutation

- 현재의 수열을 사전 순으로 생각했을 때의 다음 수열로 만들고 true를 반환하는 함수
- 현재가 **1 2 3** 이면 next_permutation을 실행한 후 **1 3 2** 가 되고, **1 3 2**에서 next_permutation을  
  실행하면 **2 1 3**이 된다.
- 다음 수열이 존재하지 않는다면 false 반환

```c
int a[3] = {1 , 2, 3};
do{
    for(int i = 0; i< 3; i++)
      count << a[i]
    cout << '\n';
}while(next_permutation(a, a + 3));

/*
123
132
213
231
312
321
*/
```

## 출처

<a href="https://www.youtube.com/watch?v=8vDDJm5EewM&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=12">[바킹독의 실전 알고리즘] 0x0C강 - 재귀</a>
