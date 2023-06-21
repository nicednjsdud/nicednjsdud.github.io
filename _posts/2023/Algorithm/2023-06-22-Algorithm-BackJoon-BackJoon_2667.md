---
published: true
title: BackJoon Algorithm 단지번호 붙이기  2667 (Java)
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
last_modified_at: "2023-06-22 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2667.png)

## 풀이

```java
import java.awt.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Back_2667 {

    static int arr[][];
    static boolean visited[][];
    static int dirX[] = {0, 0, -1, 1};
    static int dirY[] = {-1, 1, 0, 0};
    static int count = 0;
    static int number = 0;
    static int nowX, nowY, N;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        List<Integer> list = new ArrayList<>();

        N = Integer.parseInt(br.readLine());
        arr = new int[N][N];
        visited = new boolean[N][N];

        for (int i = 0; i < N; i++) {
            String str = br.readLine();

            for (int j = 0; j < N; j++) {
                arr[i][j] = Character.getNumericValue(str.charAt(j));
                visited[i][j] = false;
            }
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {

                if (visited[i][j] == false && arr[i][j] == 1) {
                    count = 0;
                    number++;
                    DFS(i, j);
                    list.add(count);
                }
            }

        }
        Collections.sort(list);
        System.out.println(number);
        for (Integer integer : list) {
            System.out.println(integer);
        }
        br.close();
    }

    private static void DFS(int x, int y) {
        visited[x][y] = true;
        arr[x][y] = number;
        count++;

        for (int i = 0; i < 4; i++) {
            nowX = dirX[i] + x;
            nowY = dirY[i] + y;

            if (nowX >= 0 && nowX < N && nowY >= 0 && nowY < N && visited[nowX][nowY] == false && arr[nowX][nowY] == 1) {
                DFS(nowX, nowY);
            }
        }
    }
}

```
