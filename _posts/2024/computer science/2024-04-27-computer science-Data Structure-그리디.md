---
title: (알고리즘) 바킹독의 실전 알고리즘 Ox11강 ( 그리디 )
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
last_modified_at: "2024-04-27 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x11강 ( 그리디 )

## 목차

- 0x00 알고리즘 설명
- 0x01 연습 문제 1 - 동전 O
- 0x02 연습 문제 2 - 회의실 배정
- 0x03 연습 문제 3 - 로프
- 0x04 연습 문제 4 - 보물
- 0x05 잘못된 그리디

## 1. 알고리즘 설명

- 지금 가장 최적인 답을 근시안적으로 택하는 알고리즘
- 관찰을 통해 탐색 범위를 줄이는 알고리즘

### 1) 이상적인 풀이 흐름

1. 관찰을 통해 탐색 범위를 줄이는 방법을 고안
2. 탐색 범위를 줄여도 올바른 결과를 낸다는 사실을 수학적으로 증명
3. 구현해서 문제를 통과

### 2) 현실적인 풀이 흐름

1. 관찰을 통해 탐색 범위를 줄이는 방법을 고안
2. 탐색 범위를 줄여도 올바른 결과를 낸다는 강한 믿음을 가짐
3. 믿음을 가지고 구현해서 문제를 통과

## 2. BOJ 11047번 : 동전 O

- `D[i] = ` 가치의 합을 i로 만들때 필요한 동전 개수의 최솟값
- `D[i] = min(D[i-A1], D[i-A2], ... , D[i-AN]) + 1` \
  - 시간 초과 발생

### 1) 보조정리 1

- 동전을 최소로 소모하면서 물건값을 지불하려면 10/100원 동전은 4개이 하
- 50원 동전은 1개 이하로 사용해야 한다.

### 2) 증명

- 10/100원 동전을 5개 이상 사용 -> 50/500원 동전으로 대체
- 50원 동전을 2개 이상 사용 -> 100원 동전으로 대체

### 3) 명제

- 동전을 최소로 소모하면서 물건값을 지불하려면 500원 동전을 최대한 많이 써야 한다.

### 4) 증명

- 10,50,100원 동전으로는 물건값을 최대 10x4 + 50x1 + 100x4 = 490원만 감당 가능
- 500원을 다 사용하지 않을 경우 10,50,100원 동전으로 500이상 감당해야함

### 5) C

```c
#include <bits/stdc++.h>
using namespace std;

int n, k;
int a[15];

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);

   int ans = 0;
   cin >> n >> k;

   for(int i = 0; i< n; i++) cin >> a[i];
   for(int i = n-1 i > =0; i++){
      ans += k / a[i];
      k %= a[i];
   }
   cout << ans;
}
```

## 3. BOJ 1931번 : 회의실 배정

### 1) O(2^N)

- 모든 가능한 배정 방법을 확인

### 2) O(N^2)

- 회의를 끝나는 시간이 빠른 순으로, 끝나는 시간이 같다면 시작 시간이 빠른 순으로 정렬
- `D[i] = i`번째 회의를 마지막으로 진행했을 때 최대 회의의 수
- `D[i] = max(D[j]) + 1` j번째 회의의 끝나는 시간이 i번째 회의의 시작 시간 이하인 모든 j

### 3) 명제

![alt](/assets/images/post/ComputerStudy/1128.png)

- 현재 시간이 t라고 할대 시작 시간이 t이상인 모든 회의 중에서 가장 먼저 끝나는 회의를 택하는 것이 최적해이다.

### 4) 증명

![alt](/assets/images/post/ComputerStudy/1129.png)

- 회의 A대신 회의 B를 택했을 때 더 많은 회의를 배정할 수 있다고 가정

### 5) 증명

![alt](/assets/images/post/ComputerStudy/1130.png)

- 회의 B대신 A를 사용해도 아무런 모순이 발생하지 않음

### 6) C

```c
#include <bits/stdc++.h>
using namespace std;

int n;
pair<int,int> s[1000005];

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   cin >> n;
   for(int i = 0; i< n; i++){
      cin >> s[i].second >> s[i].first;
   }
   sort(s, s+n);
   int ans = 0;
   int t = 0;
   for(int i = 0; i< n;i++){
      if(t > s[i].second) continue;
      ans ++;
      t = s[i].first;
   }
   cout << ans;
}
```

## 4. BOJ 2217번 : 로프

## 5. 잘못된 그리디

### 1) BOJ 1026번 : 보물

#### 1) C

```c
#include <bits/stdc++.h>
using namespace std;

int a[105], b[105];
int n;

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   cin >> n;
   for(int i = 0; i< n; i++) cin >> a[i];
   for(int i = 0; i< n; i++) cin >> b[i];
   sort(a, a+n);
   sort(b, b+n);
   int ans = 0;
   for(int i = 0; i< n; i++)
      ans += a[i] * b[n-1-i];
   cout << ans;
}
```

### 2) BOJ 12865번 : 평범한 배낭

### 3) BOJ 1477번 : 휴게소 세우기

## 출처

<a href="https://www.youtube.com/watch?v=5leTtB3PQu0&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=18">[바킹독의 실전 알고리즘] 0x11강 - 그리디</a>
