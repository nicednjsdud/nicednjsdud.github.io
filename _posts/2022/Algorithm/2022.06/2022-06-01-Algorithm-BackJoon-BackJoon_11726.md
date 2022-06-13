---
published: true
title: BackJoon Algorithm 11726 2xn 타일링 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 2xn 타일링
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-01 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11726.png)


## 풀이

![alt](/assets/images/post/Algorithm/11726_1.png)

* 계속해서 만들다보면 일정한 규칙이 있는것을 알 수 있다.
* 점화식은 dp[n] = dp[n-2] + dp[n-1] 이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_11726 {

    // dp[n] = dp[n-2] + dp[n-1]
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        // given
        int N = Integer.parseInt(br.readLine());
        int dp[] = new int[N+2];
        dp[1] = 1;
        dp[2] = 2;
        // when
        for (int i = 3; i <= N; i++) {
            dp[i] += dp[i - 2] + dp[i - 1];
            dp[i] %= 10007; // 나머지 계산해주면서 반복
        }
        // then
        System.out.println(dp[N]%10007);
        br.close();
    }
}

```



