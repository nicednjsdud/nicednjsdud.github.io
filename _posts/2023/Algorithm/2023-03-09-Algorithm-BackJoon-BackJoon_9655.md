---
published: true
title: BackJoon Algorithm 돌게임 9655 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 집합 11723
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9655.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_9655 {
    public static void main(String[] args) throws IOException {

        // n = 1 이면 상근 1                    상근 승
        // n = 2 이면 상근 1 창영 1              창영 승
        // n = 3 이면 상근 3                    상근 승
        // n = 4 이면 상근 1 or3 창영 1 or 3     창영 승

        // 점화식 dp[n] = Math.min(dp[n-1], dp[n-3]) + 1
        // 홀수이면 상근 승 짝수이면 창영 승
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[] dp = new int[1001];
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 1;
        for (int i = 4; i <= N; i++) {
            dp[i] = Math.min(dp[i - 1], dp[i - 3]) - 1;
        }
        if(dp[N] % 2 == 0){
            System.out.println("CY");
        }
        else{
            System.out.println("SK");
        }
    }
}



```
