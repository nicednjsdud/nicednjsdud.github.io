---
published: true
title: BackJoon Algorithm 올림픽 8979 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 올림픽
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-12-16 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/8979.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.StringTokenizer;

public class Back_8979 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        int rank = 1;
        int country[][] = new int[N][3];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            country[i][0] = Integer.parseInt(st.nextToken());

            // K는 등수를 알고 싶은 국가이다 그러므로 순서가 바뀔수도 있으므로 k=i로 잡는다.
            if(country[i][0] == K)
                K = i;

            for (int j = 0; j < 3; j++) {
                country[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        for (int i = 0; i < N; i++) {
            if(country[i][0] > country[K][0])
                rank ++;
            else if(country[i][0] == country[K][0] && country[i][1] > country[K][1])
                rank++;
            else if(country[i][0] == country[K][0] && country[i][1] == country[K][1] && country[i][2] > country[K][2])
                rank++;
        }
        System.out.println(rank);
        br.close();
    }
}



```
