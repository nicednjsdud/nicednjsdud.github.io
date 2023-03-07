---
published: true
title: BackJoon Algorithm 파도반 수열 9461 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 파도반 수열 9461
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-07 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9461.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_9461 {

    static Long arr[] = new Long[101];

    public static void main(String[] args) throws IOException {

        // 점화식 = func(N) = func(N-2) + func(N-3)
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            int N = Integer.parseInt(br.readLine());
            arr[0] = 0L;
            arr[1] = 1L;
            arr[2] = 1L;
            arr[3] = 1L;
            func(N);
            sb.append(func(N)).append("\n");
        }
        System.out.println(sb);
        br.close();
    }

    public static long func(int N){
        if(arr[N] == null){
            arr[N] = func(N-2) + func(N-3);
        }
        return arr[N];
    }
}


```
