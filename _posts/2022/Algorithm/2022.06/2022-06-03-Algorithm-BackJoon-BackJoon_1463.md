---
published: true
title: BackJoon Algorithm 1463 1로 만들기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 1로만들기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-03 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1463.png)


## 풀이

* Stranger's LAB님의 블로그를 보고 계속 생각해봤다.
* 자세한 설명은 Stranger's LAB님의 블로그에 자세히 설명해 두셨다.
* 나도 언젠가는 저분처럼 성장할 것이다.


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
// 재귀 함수
public class Back_1463 {

    static Integer[] dp;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N =Integer.parseInt(br.readLine());

        dp = new Integer[N+1];
        dp[0] = dp[1] = 0;

        System.out.print(recur(N));
    }
    static int recur(int N) {
        if (dp[N] == null) {
            // 6으로 나눠지는 경우
            if (N % 6 == 0) {
                dp[N] = Math.min(recur(N - 1), Math.min(recur(N / 3), recur(N / 2))) + 1;
            }
            // 3으로만 나눠지는 경우
            else if (N % 3 == 0) {
                dp[N] = Math.min(recur(N / 3), recur(N - 1)) + 1;
            }
            // 2
            else if (N %2 ==0){
                dp[N] = Math.min(recur(N/2),recur(N-1))+1;
            }
            // 2와 3으로 나누어지지 않는 경우
            else {
                dp[N] = recur(N - 1) + 1;
            }
        }
        return dp[N];
    }
}



```

<a href="https://st-lab.tistory.com/133">참고 블로그</a>
