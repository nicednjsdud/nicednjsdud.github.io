---
published: true
title: BackJoon Algorithm 가로수 2485 (Java)
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
last_modified_at: "2023-06-12 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1932.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1932 {

    static int arr[][];
    static Integer[][] dp;
    static int n;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        n = Integer.parseInt(br.readLine());
        arr = new int[n][n];
        dp = new Integer[n][n];
        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < i + 1; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());

                if (i == n -1) {
                    // dp 맨밑줄 초기화
                    dp[i][j] = arr[i][j];
                }
            }
        }
        System.out.println(find(0,0));
        br.close();
    }

    private static int find(int depth, int idx) {
        if(depth == n -1) return dp[depth][idx];

        if(dp[depth][idx] == null){
            dp[depth][idx] = Math.max(find(depth+1, idx), find(depth+1,idx+1)) + arr[depth][idx];
        }
        return dp[depth][idx];
    }
}



```
