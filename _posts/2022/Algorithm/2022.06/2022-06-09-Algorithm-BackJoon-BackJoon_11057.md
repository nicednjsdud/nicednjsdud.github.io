---
published: true
title: BackJoon Algorithm 11057 오르막 수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 오르막 수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-09 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11057.png)


## 풀이


```java
import java.util.Scanner;

public class Back_11057 {

    static int dp[][];

    public static void main(String[] args) {


        // given
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        // when
        dp = new int[N + 1][10];
        for (int i = 0; i < 10; i++) {
            dp[1][i] = 1;
        }
        for (int i = 1; i < N + 1; i++) {
            for (int j = 0; j < 10; j++) {
                for (int k = j; k < 10; k++) {
                    dp[i][j] += dp[i - 1][k];
                    dp[i][j] %= 10007;
                }
            }
        }
        // then
        System.out.println(dp[N][0] % 10007);
    }
}





```



