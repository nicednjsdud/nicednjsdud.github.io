---
published: true
title: BackJoon Algorithm 행렬 덧셈 2738 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 행렬 덧셈
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2738.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_2738 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        // 행
        int N = Integer.parseInt(st.nextToken());
        // 열
        int M = Integer.parseInt(st.nextToken());
        int A[][] = new int[N][M];
        int B[][] = new int[N][M];
        int sum[][] = new int[N][M];    // 0,1,2 행열의 합 (A+B)
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                A[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                B[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        // when
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                sum[i][j] = A[i][j] + B[i][j];
            }
        }
        // then
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                System.out.print(sum[i][j]+" ");
            }
            System.out.println();
        }
        br.close();
    }
}


```
