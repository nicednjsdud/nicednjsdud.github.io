---
published: true
title: BackJoon Algorithm 2193 이친수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 이친수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-08 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2193.png)


## 풀이


```java
import java.util.Scanner;

public class Back_2193 {
    public static void main(String[] args) {

        // given
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long dp[]=new long [n+1];
        // dp[n] = n자리 이친수
        dp[0]=0;
        dp[1]=1;
        // when
        for(int i=2;i<=n;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        // then
        System.out.println(dp[n]);
    }
}

```



