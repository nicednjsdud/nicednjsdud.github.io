---
published: true
title: BackJoon Algorithm 토마토 7569 (Java)
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
last_modified_at: "2023-09-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/7569.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

class pointXYZ {
    int height;
    int row;
    int col;

    public pointXYZ(int height, int row, int col) {
        this.height = height;
        this.row = row;
        this.col = col;
    }
}

public class Back_7569 {

    static int rowArr[] = {-1, 0, 1, 0, 0, 0};
    static int colArr[] = {0, 1, 0, -1, 0, 0};
    static int heightArr[] = {0, 0, 0, 0, 1, -1};
    static int M, N, H;
    static int arr[][][];
    static Queue<pointXYZ> q = new LinkedList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        arr = new int[H + 1][N + 1][M + 1];

        for (int i = 1; i <= H; i++) {
            for (int j = 1; j <= N; j++) {
                st = new StringTokenizer(br.readLine());
                for (int k = 1; k <= M; k++) {
                    arr[i][j][k] = Integer.parseInt(st.nextToken());
                    if (arr[i][j][k] == 1) q.add(new pointXYZ(i, j, k));
                }
            }
        }
        System.out.println(bfs());
    }

    private static int bfs() {
        while (!q.isEmpty()) {
            pointXYZ point = q.poll();

            int height = point.height;
            int row = point.row;
            int col = point.col;

            for (int i = 0; i < 6; i++) {
                int newHeight = height + heightArr[i];
                int newRow = row + rowArr[i];
                int newCol = col + colArr[i];

                if (checkPoint(newHeight,newRow,newCol)) {
                    q.add(new pointXYZ(newHeight, newRow, newCol));
                    arr[newHeight][newRow][newCol] = arr[height][row][col] + 1;
                }
            }
        }

        int result = Integer.MIN_VALUE;

        for (int i = 1; i <= H; i++) {
            for (int j = 1; j <= N; j++) {
                for (int k = 1; k <= M; k++) {
                    if (arr[i][j][k] == 0) return -1;

                    result = Math.max(result, arr[i][j][k]);
                }
            }
        }
        if (result == 1) return 0;
        else return (result - 1);
    }

    private static boolean checkPoint(int height, int row, int col){
        // 주어진 범위 밖인지 검사
        if(height < 1 || height > H || row < 1 || row > N || col < 1 || col > M) return false;
        // 아직 익지 않은 토마토라면 true 반환
        if(arr[height][row][col] == 0) return true;
            // 이미 익어있거나 빈 자리라면 false 반한
        else return false;
    }
}


```
