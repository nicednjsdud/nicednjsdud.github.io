---
published: true
title: BackJoon Algorithm 적록색약 10026 (Java)
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
last_modified_at: "2023-08-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10026.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10026 {

    static int N;
    static String s;
    static char map[][];
    static boolean visited[][];
    static int dx[] = {-1, 0, 0, 1};
    static int dy[] = {0, 1, -1, 0};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        map = new char[N + 1][N + 1];
        visited = new boolean[N + 1][N + 1];

        for (int i = 0; i < N; i++) {
            s = br.readLine();
            for (int j = 0; j < N; j++) {
                map[i][j] = s.charAt(j);
            }
        }

        // normal
        int normalCnt = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (!visited[i][j]) {
                    dfs(i, j);
                    normalCnt++;
                }
            }
        }


        // dltonism
        int cnt = 0;
        visited = new boolean[N + 1][N + 1];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[i][j] == 'G') {
                    map[i][j] = 'R';
                }
            }
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (!visited[i][j]) {
                    dfs(i, j);
                    cnt++;
                }
            }
        }
        System.out.println(normalCnt+ " " + cnt);
        br.close();
    }

    private static void dfs(int x, int y) {
        visited[x][y] = true;
        char temp = map[x][y];
        for (int i = 0; i < 4; i++) {
            int newX = x + dx[i];
            int newY = y + dy[i];

            if (newX < 0 || newY < 0 || newX > N || newY > N) {
                continue;
            }
            if (!visited[newX][newY] && map[newX][newY] == temp) {
                dfs(newX, newY);
            }
        }
    }
}

```
