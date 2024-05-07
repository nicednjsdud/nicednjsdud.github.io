---
title: (알고리즘) 바킹독의 실전 알고리즘 0x10강 ( 다이나믹 프로그래밍 )
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
last_modified_at: "2024-04-12 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 바킹독의 실전 알고리즘 0x0F강 ( 정렬 II )

## 목차

- 0x00 알고리즘 설명
- 0x01 연습 문제
- 0x02 경로 추적

## 1. 알고리즘 설명

### 1) 다이나믹 프로그래밍 (Dynamic Programming, DP)

- 여러개의 하위 문제를 먼저 푼 후 그 결과를 쌓아 올려 주어진 문제를 해결하는 알고리즘

### 2) DP를 푸는 과정

1. 테이블 정의하기
2. 점화식 찾기
3. 초기값 정하기

## 2. 연습 문제

### 1) BOJ 1463번 : 1로 만들기

1. 테이블 정의하기
   - `D[i] = [i]`를 1로 만들기 위해 필요한 연산 사용 횟수의 최솟값
2. 점화식 찾기

   - `D[k] = ?`

   * 3으로 나누어지면 3으로 나누거나 `(D[k] = D[k/3] + 1)`
   * 2로 나누어지면 2로 나누거나 `(D[k] = D[k/2] + 1)`
   * 1을 빼거나 `(D[k] = D[k-1] + 1)`, 이들 중에서 최솟값

3. 초기값 정의하기

```c
   D[1] = 0
```

#### 1-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int d[1000005];
int n;

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   cin >> n;
   d[1] = 0;
   for(int i = 2; i <= n; i++){
      d[i] = d[i-1] + 1;
      if(i%2 == 0) d[i] = min(d[i],d[i/2] + 1);
      if(i%3 == 0) d[i] = min(d[i],d[i/3] + 1);
   }
   cout << d[n];
}
```

#### 1-2) Java

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1463_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int dp[] = new int[1000001];
        int N = Integer.parseInt(br.readLine());
        dp[1] = 0;
        for (int i = 2; i <= N; i++) {
            dp[i] = dp[i - 1] + 1;
            if (i % 2 == 0) dp[i] = Math.min(dp[i], dp[i / 2] + 1);
            if (i % 3 == 0) dp[i] = Math.min(dp[i], dp[i / 3] + 1);
        }
        System.out.println(dp[N]);
    }
}

```

### 2) BOJ 9095번 : 1,2,3 더하기

1. 테이블 정의하기
   - `D[i] = i`를 1,2,3의 합으로 나타내는 방법의 수
2. 점화식 찾기

   - `D[4] = ?`
   - 1+1+1+1, 3+1, 2+1+1, 1+2+1 (3을 1,2,3의 합으로 나타내는 방법) + 1, `D[3]`
   - 1+1+2, 2+2 (2를 1,2,3의 합으로 나타내는 방법) + 2, `D[2]`
   - 1+3 (3을 1,2,3의 합으로 나타내는 방법) + 3, `D[1]`
   - `D[4] = D[1] + D[2] + D[3]`
   - `D[i] = D[i-1] + D[i-2] + D[i-3]`

3. 초기값 정하기
   - `D[1] = 1, D[2] = 2, D[3] = 4`
   - `D[i] = D[i-1] + D[i-2] + D[i-3]`이니 초기값이 최소 3개는 주어져야 함

#### 2-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int d[20];
int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   d[1] = 1; d[2] = 2; d[3] = 4;
   for(int i = 4; i< 11;i++){
      d[i] = d[i-1] + d[i-2] + d[i-3];
   }
   int t;
   cin >> t;

   while(t--){
      int n;
      cin >> n;
      cout << d[n] << '\n';
   }
}
```

#### 2-2) Java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_9095/">BackJoon Algorithm 9095 1, 2, 3 더하기 (Java)
</a>

### 3) BOJ 2579번 : 계단 오르기

1. 테이블 정의하기
   - `D[i][j] = ` 혀ㄴ재까지 j개의 계단은 연속해서 밟고 i번째 계단까지 올라섰을 때 점수 합의 최댓값, 단 i번째 계단은 반드시 밟아야 함
2. 점화식 찾기

   - `D[k][1] = max(D[k-2][1], D[k-2][2]) + S[k]`
   - `D[k][2] = D[k-1][1] + S[k]`

3. 초기 값 정하기
   - `D[1][1] = S[1], D[1][2] = 0,`.
     `D[2][1] = S[2], D[2][2] = S[1] + S[2]`

#### 3-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int s[305];
int n;
int d[305][3];

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   cin >> n;
   for(int i = 0; i<=n; i++) cin >> s[i];
   if(n == 1){
      cout << s[1];
      return 0;
   }

   d[1][1] = s[1];
   d[1][2] = 0;
   d[2][1] = s[2];
   d[2][2] = s[1] + s[2];

   for(int = 3; i<=n; i++){
      d[i][1] = max(d[i-2][1],d[i-2][2]) + s[i];
      d[i][2] = d[i-1][1] + s[i];
   }
   cout << max(d[n][1],d[n][2]);
}
```

### 4) BOJ 1149번 : RGB 거리

1. 테이블 정의하기

   - `D[i][0] = i`번째 집까지 칠할 때 비용의 최솟값, 단 i번째 집은 **빨강**
   - `D[i][1] = i`번째 집까지 칠할 때 비용의 최솟값, 단 i번째 집은 **초록**
   - `D[i][2] = i`번째 집까지 칠할 때 비용의 최솟값, 단 i번째 집은 **파랑**

2. 점화식 찾기

   - `D[k][0] = min(D[k-1][1], D[k-1][2]) + R[k]`
   - `D[k][1] = min(D[k-1][0], D[k-1][2]) + G[k]`
   - `D[k][2] = min(D[k-1][0], D[k-1][1]) + B[k]`

3. 초기값 정하기
   - `D[1][0] = R[1]`
   - `D[1][1] = G[1]`
   - `D[1][2] = B[1]`

#### 4-1) C

```c
#include <bits/stdc++.h>
using namespace std;

int d[1005][3];
int r[1005], g[1005], b[1005];

int main(void){
   ios::sync_with_stdio(0);
   cin.tie(0);
   int n;
   cin >> n;

   for(int i = 1; i<=n; i++){
      cin >> r[i] >> g[i] >> b[i];
   }
   d[1][0] = r[1];
   d[1][1] = g[1];
   d[1][2] = b[1];

   for(int i = 2; i<=n ; i++){
      d[i][0] = min(d[i-1][1], d[i-1][2]) + r[i];
      d[i][1] = min(d[i-1][0], d[i-1][2]) + g[i];
      d[i][2] = min(d[i-1][0], d[i-1][1]) + b[i];
   }
   cout << *min_element(d[n], d[n] + 3)
}
```

#### 4-2) Java

<a href="https://nicednjsdud.github.io/algorithm/Algorithm-BackJoon-BackJoon_1149/">BackJoon Algorithm RGB거리 11490 (Java)
</a>

## 출처

<a href="https://www.youtube.com/watch?v=5leTtB3PQu0&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=17">[바킹독의 실전 알고리즘] 0x10강 - 다이나믹 프로그래밍</a>
