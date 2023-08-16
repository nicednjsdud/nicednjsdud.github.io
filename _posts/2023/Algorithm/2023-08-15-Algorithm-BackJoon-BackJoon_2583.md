---
published: true
title: BackJoon Algorithm 영역구하기 2583 (Java)
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
last_modified_at: "2023-08-15 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2583.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.StringTokenizer;

public class Back_2583 {

    static int dx[] = {-1, 0, 0, 1};
    static int dy[] = {0, 1, -1, 0};
    static int M, N, K;
    static int map[][];

    static int count;


    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer st = new StringTokenizer(br.readLine());
        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        map = new int[M][N];

        for (int i = 0; i < K; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());

            for (int y = y1; y < y2; y++) {
                for (int x = x1; x < x2; x++) {
                    map[y][x] = 1;
                }
            }
        }

        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 0) {
                    count = 0;
                    dfs(i, j);
                    list.add(count);
                }

            }
        }
        Collections.sort(list);
        sb.append(list.size()).append("\n");
        for (Integer integer : list) {
            sb.append(integer + " ");
        }
        System.out.println(sb);
    }

    private static void dfs(int x, int y) {
        map[x][y] = 1;
        count++;

        for (int k = 0; k < 4; k++) {
            int newX = x + dx[k];
            int newY = y + dy[k];

            if (newX >= 0 && newX < M && newY >= 0 && newY < N) {
                if (map[newX][newY] == 0) {
                    dfs(newX, newY);
                }
            }
        }
    }
}

```
