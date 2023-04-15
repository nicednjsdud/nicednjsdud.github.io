---
published: true
title: BackJoon Algorithm 11724 연결요소의 개수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 11724 연결요소의 개수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-13 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11724.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11724 {

    static int arr[][];
    static boolean node[];
    static int N, count;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        arr = new int[N + 1][N + 1];
        node = new boolean[1001];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            arr[x][y] = 1;
            arr[y][x] = 1;
        }

        count = 0;
        for (int i = 1; i <= N; i++) {
            if (node[i] == false) {
                DFS(i);
                count++;
            }
        }
        System.out.println(count);
        br.close();
    }

    static void DFS(int value) {

        if (node[value] == true) {
            return;
        } else {
            node[value] = true;
            for (int i = 1; i <= N; i++) {
                if (arr[value][i] == 1) {
                    DFS(i);
                }
            }
        }
    }
}

```