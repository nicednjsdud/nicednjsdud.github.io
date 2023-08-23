---
published: true
title: BackJoon Algorithm 숨바꼭질 1697 (Java)
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
last_modified_at: "2023-08-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1697.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_1697 {

    static int N, K;
    static int arr[];
    static Queue<Integer> queue = new LinkedList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());
        if (N >= K) {
            System.out.println(N - K);
        } else {
            System.out.println(bfs());
        }
    }

    private static int bfs() {
        arr = new int[100001];
        queue.add(N);
        arr[N] = 1;
        while (!queue.isEmpty()) {
            int x = queue.poll();
            for (int i = 0; i < 3; i++) {
                int nx;
                if (i == 0) {
                    nx = x + 1;
                } else if (i == 1) {
                    nx = x - 1;
                } else {
                    nx = x * 2;
                }
                if (nx == K) {
                    return arr[x];
                }
                if (nx >= 0 && nx < arr.length && arr[nx] == 0) {
                    arr[nx] = arr[x] + 1;
                    queue.add(nx);
                }
            }
        }
        return 0;
    }
}

```