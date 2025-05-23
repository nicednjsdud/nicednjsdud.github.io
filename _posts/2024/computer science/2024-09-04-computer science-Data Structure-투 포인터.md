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
last_modified_at: "2025-05-23 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x14강 ( 투 포인터 )

## 📌 목차

- [0x00 알고리즘 설명](#0x00-알고리즘-설명)
- [0x01 연습 문제 1 - 수 고르기](#0x01-연습-문제-1---수-고르기)
- [0x02 연습 문제 2 - 부분합](#0x02-연습-문제-2---부분합)

## 🔍 0x00 알고리즘 설명

### 🧠 투 포인터란?

> **O(N²)** 복잡도를 가지는 문제를 **O(N)**으로 줄이는 대표적인 테크닉!

- 배열의 두 지점을 가리키는 **start**, **end** 포인터를 사용해 슬라이딩 윈도우를 구성
- 조건을 만족할 때까지 포인터를 움직이며 해를 구하는 방식

## 🧪 0x01 연습 문제 1 - 수 고르기 ([백준 2230번](https://www.acmicpc.net/problem/2230))

![수 고르기 흐름](/assets/images/post/ComputerStudy/1131.png)

### 🚩 핵심 아이디어

- 배열 정렬 후, `a[en] - a[st]`가 M 이상이 되는 **최초의 지점 en**을 찾는다.
- 이 이후부터는 더 확인할 필요 없음!

### 🎯 시각적 풀이 과정

#### ✅ 초기 상태

```plaintext
M = 6
min = INF
st = 0, en = 0
```

![1132](/assets/images/post/ComputerStudy/1132.png)

#### ➡️ en 이동

`a[en] - a[st] < M`이므로 `en++`

![1133](/assets/images/post/ComputerStudy/1133.png)

#### ✅ 갱신

- 차이가 M 이상이 되었으므로 `min = 7`

![1134](/assets/images/post/ComputerStudy/1134.png)

#### ⏩ st 이동

- 현재 en이 최초 지점이라 `min = 6`으로 갱신

![1135](/assets/images/post/ComputerStudy/1135.png)

#### 🔁 다시 en 이동

- 차이가 M보다 작으면 en 계속 증가

![1136](/assets/images/post/ComputerStudy/1136.png)  
![1137](/assets/images/post/ComputerStudy/1137.png)

### 🧾 C++ 코드

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
int a[100005];
int mn = 0x7fffffff;

int main(){
  ios::sync_with_stdio(0); cin.tie(0);
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

### ☕ Java 풀이 블로그

🔗 [BackJoon 2230 수 고르기 (Java)](https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_2230/)

## 💡 0x02 연습 문제 2 - 부분합 ([백준 1806번](https://www.acmicpc.net/problem/1806))

### ✅ 핵심 아이디어

- 누적합을 투 포인터로 유지하면서 합이 S 이상인 최소 구간 찾기

### 🧾 C++ 코드

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, s, tot;
int a[100005];
int mn = 0x7fffffff;

int main(){
  ios::sync_with_stdio(0); cin.tie(0);
  cin >> n >> s;
  for(int i = 0; i < n; i++) cin >> a[i];

  tot = a[0];
  int en = 0;

  for(int st = 0; st < n; st++){
    while(en < n && tot < s){
      en++;
      if(en != n) tot += a[en];
    }
    if(en == n) break;
    mn = min(mn, en - st + 1);
    tot -= a[st];
  }
  if(mn == 0x7fffffff) mn = 0;
  cout << mn;
}
```

### ☕ Java 풀이 블로그

🔗 [BackJoon 1806 부분합 (Java)](https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_1806/)

## 🎓 참고 출처

- 🎥 [바킹독의 실전 알고리즘 - 투 포인터](https://www.youtube.com/watch?v=I_0aAKzu0m8&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY)

## ✅ 요약

| 항목 | 수 고르기 (2230) | 부분합 (1806) |
|------|------------------|----------------|
| 목표 | 차이가 M 이상인 수들의 최소 차이 | 합이 S 이상인 부분 배열 길이 |
| 방식 | 정렬 후 최소 차이 탐색 | 누적합 + 최소 길이 탐색 |
| 시간복잡도 | O(N) | O(N) |

