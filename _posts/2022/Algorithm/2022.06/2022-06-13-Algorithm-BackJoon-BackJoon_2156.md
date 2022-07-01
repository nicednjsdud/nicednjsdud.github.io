---
published: true
title: BackJoon Algorithm 2156 포도주 시식 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 포도주 시식
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-13 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2156.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2156 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());    // 포도주 잔의 개수
        int dp[] = new int[n];
        int glass[] = new int[n];                     // 포도주 잔
        // when
        for (int i = 0; i < n; i++) {
            StringTokenizer token = new StringTokenizer(br.readLine());
            glass[i] = Integer.parseInt(token.nextToken());  // 입력
        }


        if (n == 1) {
            System.out.println(glass[0]);
        } else if (n == 2) {
            System.out.println(glass[0] + glass[1]);
        } else {
            dp[0] = glass[0];
            dp[1] = dp[0] + glass[1];
            dp[2] = Math.max(dp[1], Math.max(glass[0] + glass[2], glass[1] + glass[2]));

            for (int j = 3; j < n; j++) {
                dp[j] = Math.max(dp[j - 3] + glass[j] + glass[j - 1], dp[j - 2] + glass[j]);
                dp[j] = Math.max(dp[j - 1], dp[j]);
            }
            System.out.println(dp[n - 1]);

        }

        // then

        br.close();
    }
}



```



