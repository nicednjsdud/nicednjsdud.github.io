---
published: true
title: BackJoon Algorithm 대회자리 5176 (Java)
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
last_modified_at: "2023-08-28 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5176.png)

## 풀이

```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Back_5176 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int K = Integer.parseInt(br.readLine());
        StringTokenizer st;

        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int P = Integer.parseInt(st.nextToken());
            int M = Integer.parseInt(st.nextToken());

            int[] arr = new int[M + 1];
            for (int j = 0; j < arr.length; j++) {
                arr[j] = 1;
            }
            int count = 0;
            for (int j = 0; j < P; j++) {
                int num = Integer.parseInt(br.readLine());
                if (arr[num] == 1) {
                    arr[num] = 0;
                }
                else{
                    count ++;
                }
            }
            sb.append(count).append("\n");
        }
        System.out.println(sb);
        br.close();
    }
}


```
