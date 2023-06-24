---
published: true
title: BackJoon Algorithm 촌수  2644 (Java)
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
last_modified_at: "2023-06-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2644.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_2644 {

    static int n, p1, p2;
    static int[][] map;
    static int[] arr;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        p1 = Integer.parseInt(st.nextToken());
        p2 = Integer.parseInt(st.nextToken());

        map = new int[n + 1][n + 1];
        int m = Integer.parseInt(br.readLine());
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            map[x][y] = 1;
            map[y][x] = 1;
        }
        arr = new int[n + 1];

        BFS(p1, p2);
        if (arr[p2] == 0) {
            System.out.println(-1);
        } else {
            System.out.println(arr[p2]);
        }
        br.close();
    }

    private static void BFS(int start, int end) {
        Queue<Integer> qu = new LinkedList<>();
        qu.add(start);
        while (!qu.isEmpty()) {

            int v = qu.poll();
            if (v == end) {
                break;
            }
            for (int i = 1; i <= n; i++) {
                if (map[v][i] == 1 && arr[i] == 0) {
                    arr[i] = arr[v] + 1;
                    qu.add(i);
                }
            }
        }
    }
}

```
