---
published: true
title: BackJoon Algorithm 11050 이항 계수 1(Java)
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
last_modified_at: "2023-05-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11050.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11050 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int mo_value = 1;
        int temp = 1;
        int de_value = 1;

        for (int i = 0; i < N; i++) {
            mo_value = mo_value * (N - i);
        }

        for (int i = 0; i < N - K; i++) {
            temp = temp * (N - K - i);
        }

        for (int i = 0; i < K; i++) {
            de_value = de_value * (K - i);
        }
        System.out.println(mo_value / (de_value * temp));
        br.close();
    }
}





```
