---
published: true
title: BackJoon Algorithm 9095 1, 2, 3 더하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 1, 2, 3 더하기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-04 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9095.png)


## 풀이

* 6까지 만들어보니 규칙이 있었습니다.
* 점화식 dp[n] = dp[n-3]+dp[n-2]+dp[n-1]


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
// 점화식 dp[n]= dp[n-3]+dp[n-2]+dp[n-1}
public class Back_9095 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        int dp[]= new int [11];
        int out[]= new int[T];
        dp[1]= 1;
        dp[2]= 2;
        dp[3]= 4;
        // when
        for(int i=4;i<=10;i++){
            dp[i]=dp[i-3]+dp[i-2]+dp[i-1];
        }

        // then
        for(int i=0;i<T;i++){
            int num = Integer.parseInt(br.readLine());
            out[i]=dp[num];
            System.out.println(out[i]);
        }
        br.close();
    }
}


```


