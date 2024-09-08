---
title: (알고리즘) 바킹독의 실전 알고리즘 Ox14강 ( 투 포인터 )
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
last_modified_at: "2024-09-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x14강 ( 투 포인터 )

## 목차

- 0x00 알고리즘 설명
- 0x01 연습 문제 1 - 수 고르기
- 0x02 연습 문제 2 - 부분합

## 1. 알고리즘 설명

### 1) 투포인터

- 배열에서 원래 이중 for문으로 **O(N2)**에 처리되는 작업을 2개 포인터의 움직임으로 **O(N)**에 해결하는 알고리즘

## 2. 0x01 연습 문제 1 - 수 고르기

![alt](/assets/images/post/ComputerStudy/1131.png)

1. i가 증가함에 따라 `a[j] - a[i]`가 m 이상되는 최조의 지점 j 또한 증가
2. 각 i에 대해 `a[j] - a[i]`가 m이상 되는 최초의 지점 j를 찾은 이후에는 `a[j+1].a[j+2], ...`을 확인할 필요가 없다.

### 1) 풀이

#### 1-1)

- 먼저 변수 st, en을 0에 둔다.

M = 6
min = Infinity

![alt](/assets/images/post/ComputerStudy/1132.png)

#### 1-2)

- `a[en] - a [st]`가 M이상이 될때 까지 옮긴다.

![alt](/assets/images/post/ComputerStudy/1133.png)

- min = 7로 갱신

#### 1-3)

![alt](/assets/images/post/ComputerStudy/1134.png)

- 더이상 en을 늘릴필요가 없으니 st를 옮긴다.
- st = 1일때 `a[en] - a[st]`가 m 이상이 되는 최조의 지점 en을 찾아야 하는데  
  지금 en이 애초에 최초의 지점 이므로 min 갱신
- min = 6

#### 1-4)

- st =1 일때 해야할 것을 다했으니 다시 st를 오른쪽으로 이동

![alt](/assets/images/post/ComputerStudy/1135.png)

- `a[en] - a[st]`가 m보다 작기 때문에 en을 옮김

#### 1-5)

![alt](/assets/images/post/ComputerStudy/1136.png)

- `a[en] - a[st]`가 아직 m보다 작기 때문에 en을 한번더 옮김

#### 1-6)

![alt](/assets/images/post/ComputerStudy/1137.png)

- `a[en] - a[st]`이 m이상이 됨
- 하지만 `a[en] - a[st]`가 min보다 크기 때문에 **min**의 갱신을 일어나지 않음

### 2) C

```c
#include <bits/stdc++.h>
using namespace std;

int n, m;
int a[100005];
int mn = 0x7fffffff;

int main(){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  for(int i = 0; i < n; i++) cin >> a[i];
  sort(a, a+n);
  int en = 0;
  for(int st = 0; st < n; st++){
    while(en < n && a[en] - a[st] < m) en++;
    if(en == n) break;
    mn = min(mn, a[en] - a[st]);
  }
  cout << mn;
}
```

### 3) JAVA

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_2230/">BackJoon Algorithm 수고르기 2230 (Java)</a>

## 3. OxO2 연습 문제 2 - 부분합

### 1) C

```c
#include <bits/stdc++.h>
using namespace std;

int n, s, tot;
int a[100005];
int mn = 0x7fffffff;

int main(){
  ios::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> s;
  for(int i = 0; i< n; i++) cin >> a[i];
  tot = a[0];
  int en = 0;

  for(int st = 0; st < n; st++){
    while(en < n && tot < s){
      en++;
      if(en != n) tot += a[en];
    }
    if(en == n) break; // en이 범위를 벗어날 시 종료
    mn = min(mn, en - st + 1);
    tot -= a[st]
  }
  if(mn == 0x7fffffff) mn = 0;
  cout << mn;
}
```

### 2) JAVA

- 풀예정

## 출처

<a href="https://www.youtube.com/watch?v=I_0aAKzu0m8&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY">[바킹독의 실전 알고리즘] 0x14강 - 투 포인터 </a>
