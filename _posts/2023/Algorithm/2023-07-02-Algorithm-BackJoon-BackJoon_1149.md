---
published: true
title: BackJoon Algorithm RGB거리  11490 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-07-02 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1149.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1149 {

    final static int red = 0;
    final static int green = 1;
    final static int blue = 2;

    static int[][] cost;
    static int[][] dp;


    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        cost = new int[N][3];
        dp = new int[N][3];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i][red] = Integer.parseInt(st.nextToken());
            cost[i][green] = Integer.parseInt(st.nextToken());
            cost[i][blue] = Integer.parseInt(st.nextToken());
        }

        dp[0][red] = cost[0][red];
        dp[0][green] = cost[0][green];
        dp[0][blue] = cost[0][blue];

        System.out.println(Math.min(color_cost(N - 1, red), Math.min(color_cost(N - 1, green), color_cost(N - 1, blue))));
        br.close();
    }

    private static int color_cost(int N, int color) {

        if (dp[N][color] == 0) {
            if(color == red){
                dp[N][red] = Math.min(color_cost(N-1,green),color_cost(N-1,blue)) + cost[N][red];
            }
            else if(color == green){
                dp[N][green] = Math.min(color_cost(N-1,red),color_cost(N-1,blue)) + cost[N][green];
            }
            else{
                dp[N][blue] = Math.min(color_cost(N-1,red),color_cost(N-1,green)) + cost[N][blue];
            }
        }

        return dp[N][color];
    }
}


```
