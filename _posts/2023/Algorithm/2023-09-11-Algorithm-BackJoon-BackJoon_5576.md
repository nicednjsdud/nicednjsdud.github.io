---
published: true
title: BackJoon Algorithm 콘테스트 5576 (Java)
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
last_modified_at: "2023-09-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5576.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_5576 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int W[] = new int[10];
        int K[] = new int[10];
        for (int i = 0; i < 10; i++) {
            W[i] = Integer.parseInt(br.readLine());
        }
        for (int i = 0; i < 10; i++) {
            K[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(W);
        Arrays.sort(K);

        int wSum = W[7] + W[8] + W[9];
        int kSum = K[7] + K[8] + K[9];

        System.out.println(wSum + " " + kSum);
        br.close();
    }
}


```
