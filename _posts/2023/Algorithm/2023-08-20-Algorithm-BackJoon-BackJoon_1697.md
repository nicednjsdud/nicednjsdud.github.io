---
published: true
title: BackJoon Algorithm 섬 4963 (Java)
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
last_modified_at: "2023-08-19 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4963.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_4963 {

    static int arr[][];
    static boolean visited[][];
    static int dirX[] = {0, 0, -1, 1, -1, 1, -1, 1};
    static int dirY[] = {-1, 1, 0, 0, 1, 1, -1, -1};

    static int width, height;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer st;

        while (true) {
            st = new StringTokenizer(br.readLine());
            width = Integer.parseInt(st.nextToken());
            height = Integer.parseInt(st.nextToken());
            if (width == 0 && height == 0) {
                break;
            } else {

                arr = new int[height][width];
                visited = new boolean[height][width];

                for (int i = 0; i < height; i++) {
                    st = new StringTokenizer(br.readLine());
                    for (int j = 0; j < width; j++) {
                        arr[i][j] = Integer.parseInt(st.nextToken());
                    }
                }

                int count = 0;

                for (int i = 0; i < height; i++) {
                    for (int j = 0; j < width; j++) {

                        if (!visited[i][j] && arr[i][j] == 1) {
                            count++;
                            dfs(i, j);
                        }
                    }
                }
                sb.append(count).append("\n");
            }
        }
        System.out.println(sb);
        br.close();
    }

    private static void dfs(int x, int y) {
        visited[x][y] = true;

        for (int i = 0; i < 8; i++) {
            int nowX = dirX[i] + x;
            int nowY = dirY[i] + y;

            if(nowX >=0 && nowY >=0 && nowX < height && nowY < width && !visited[nowX][nowY] && arr[nowX][nowY] == 1 ){
                dfs(nowX,nowY);
            }
        }
    }

}



```
