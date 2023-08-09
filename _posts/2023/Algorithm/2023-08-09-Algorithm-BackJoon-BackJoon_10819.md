---
published: true
title: BackJoon Algorithm 차이를 최대로 10819 (Java)
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
last_modified_at: "2023-08-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10819.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Back_10819 {

    static int[] arr;
    static boolean[] visited;

    static int[] result;
    static int N;

    static int max = Integer.MIN_VALUE;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        arr = new int[N];
        visited = new boolean[N];
        result = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        back(0);
        System.out.println(max);
        br.close();
    }

    private static void back(int depth) {
        if (N == depth) {
            int sum = 0;
            for (int i = 0; i < N - 1; i++) {
                sum += Math.abs(result[i] - result[i +1]);
            }
            max = Math.max(sum,max);
            return;
        }
        for (int i = 0; i < N; i++) {
            if (!visited[i]) {
                visited[i] = true;
                result[depth] = arr[i];
                back(depth + 1);
                visited[i] = false;
            }
        }
    }
}
```
