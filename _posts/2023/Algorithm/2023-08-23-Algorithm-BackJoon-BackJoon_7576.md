---
published: true
title: BackJoon Algorithm 토마토 7576 (Java)
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
last_modified_at: "2023-08-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/7576.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_7576 {

    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    static int n, m;
    static int[][] map;

    static Queue<int[]> q = new LinkedList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        map = new int[m][n];
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (map[i][j] == 1) {
                    q.add(new int[]{i, j});
                }
            }
        }
        System.out.println(bfs());
    }

    private static int bfs() {
        while (!q.isEmpty()) {
            int[] tomato = q.poll();
            int x = tomato[1];
            int y = tomato[0];
            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                if (map[ny][nx] == 0) {
                    map[ny][nx] = map[y][x] + 1;
                    q.add(new int[]{ny, nx});
                }
            }
        }

        int max = 0;
        if (checkZero()) {
            return -1;
        } else {
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    if(max < map[i][j]){
                        max = map[i][j];
                    }
                }
            }
            return max - 1;
        }
    }

    private static boolean checkZero() {
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (map[i][j] == 0) {
                    return true;
                }
            }
        }
        return false;
    }
}


```
