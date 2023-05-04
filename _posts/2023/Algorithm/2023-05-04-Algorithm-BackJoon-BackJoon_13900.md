---
published: true
title: BackJoon Algorithm 13900 순서쌍의 곱의 합 (Java)
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
last_modified_at: "2023-05-04 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/13900.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_13900 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        long arr[] = new long[N + 1];
        long cumSum[] = new long[N + 1];
        StringTokenizer st = new StringTokenizer(br.readLine());

        arr[0] = 0L;
        cumSum[0] = 0L;
        for (int i = 1; i <= N; i++) {
            arr[i] = Long.parseLong(st.nextToken());
            cumSum[i] = arr[i] + cumSum[i - 1];
        }

        long sum = 0L;
        for (int i = 2; i <= N; i++) {
            sum += arr[i] * cumSum[i - 1];
        }
        System.out.println(sum);
        br.close();
    }
}

```
