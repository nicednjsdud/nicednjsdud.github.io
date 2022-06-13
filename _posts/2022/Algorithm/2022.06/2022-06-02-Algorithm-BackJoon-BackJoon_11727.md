---
published: true
title: BackJoon Algorithm 11727 2xn 타일링2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 2xn 타일링2
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-02 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11727.png)


## 풀이

![alt](/assets/images/post/Algorithm/11727_1.png)

* 앞선 11726번 문제와 비슷한문제다 
* 2x2 타일도 가능하게 되면서 n-2번째 x2가 된다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

// dp[n]= dp[n-1]+(2*dp[n-2]
public class Back_11727 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        // when
        int dp[] = new int[n + 2];

        dp[1] = 1;
        dp[2] = 3;
        for(int i=3;i<=n;i++){
            dp[i]+=dp[i-1]+(2*dp[i-2]);
            dp[i] %=10007;
        }
        // then
        System.out.println(dp[n]%10007);
        br.close();
    }
}


```



