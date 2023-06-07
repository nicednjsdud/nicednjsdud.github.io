---
published: true
title: BackJoon Algorithm 치킨 배달 15686 (Java)
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
last_modified_at: "2023-06-07 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/15686.png)

## 풀이

```java
import org.w3c.dom.Node;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;


public class Back_15686 {

    public static class Point {
        int x;
        int y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }

    }

    static int N;
    static int M;

    static int[][] board;
    static ArrayList<Point> person;
    static ArrayList<Point> chicken;

    static int ans;

    static boolean[] openCheck;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        board = new int[N][N];
        person = new ArrayList<>();
        chicken = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
                if (board[i][j] == 1) person.add(new Point(i, j));
                if (board[i][j] == 2) chicken.add(new Point(i, j));
            }
        }
        ans = Integer.MAX_VALUE;
        openCheck = new boolean[chicken.size()];
        dfs(0, 0);
        System.out.println(ans);
        br.close();
    }

    private static void dfs(int count, int depth) {
        if (depth == M) {
            int sum = 0;

            for (int i = 0; i < person.size(); i++) {
                int temp = Integer.MAX_VALUE;

                for (int j = 0; j < chicken.size(); j++) {
                    if (openCheck[j]) {
                        int dis = Math.abs(person.get(i).x - chicken.get(j).x)
                                + Math.abs(person.get(i).y - chicken.get(j).y);
                        temp = Math.min(temp, dis);
                    }

                }
                sum += temp;
            }
            ans = Math.min(ans, sum);
            return;
        }

        for (int i = count; i < chicken.size(); i++) {
            openCheck[i] = true;
            dfs(i + 1, depth + 1);
            openCheck[i] = false;
        }
    }
}


```
