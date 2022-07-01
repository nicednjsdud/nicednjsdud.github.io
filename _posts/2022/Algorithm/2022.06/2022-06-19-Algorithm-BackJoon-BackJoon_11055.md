---
published: true
title: BackJoon Algorithm 11055 가장 큰 증가 부분 수열 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 가장 큰 증가 부분 수열
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-19 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11055.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11055 {
    static int N;
    static int dp[], seq[];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        seq = new int[N+1];
        dp = new int[N+1];
        int max=0;
        StringTokenizer token = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            seq[i] = Integer.parseInt(token.nextToken());// 값입력
            dp[i] = seq[i];
        }

        // 값이 하나 주어질때를 대비
        int result = dp[1];

        for(int i=1;i<=N;i++){
            for(int j=0;j<i;j++){
                if(seq[j]<seq[i]){
                    dp[i] = Math.max(dp[j]+seq[i],dp[i]);
                    result=Math.max(result,dp[i]);
                }
            }
        }
        System.out.println(result);
        br.close();


    }


}

```



