---
published: true
title: BackJoon Algorithm 베르트랑 공준 4948 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 베르트랑 공준
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4948.png)

- 전 문제랑 비슷한 소수찾기 문제이다!
- 에라토스테네스 체 알고리즘을 이용하면 쉽게 풀수있다.

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2581 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int M = Integer.parseInt(br.readLine());
        int N = Integer.parseInt(br.readLine());

        // N 배열 생성
        boolean prime[] = new boolean[N + 1];

        // 0하고 1은 소수가 아님
        prime[0] = true;
        prime[1] = true;

        // 에라토스테네스 체
        for (int i = 2; i <= Math.sqrt(prime.length); i++) {
            for (int j = i * i; j < prime.length; j += i) {
                prime[j] = true;
            }
        }
        int sum = 0;
        int small_count = 0;
        // when
        for (int i = M; i <= N; i++) {

            // i 가 소수이면
            if (prime[i] == false) {
                sum += i;

                // 첫 소수는 최소값
                if (small_count == 0) {
                    small_count = i;
                }
            }
        }

        // then
        if (sum == 0 && small_count == 0) {
            System.out.println(-1);
        } else {
            System.out.println(sum);
            System.out.println(small_count);
        }

        br.close();
    }
}


```
