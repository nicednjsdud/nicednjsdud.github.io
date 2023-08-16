---
published: true
title: BackJoon Algorithm 순열 사이클 10451 (Java)
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
last_modified_at: "2023-08-16 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10451.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10451 {

    static int map[];
    static boolean visited[];
    static int cycle;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer st;
        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            int N = Integer.parseInt(br.readLine());
            cycle = 0;
            map = new int[N + 1];
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j < N + 1; j++) {
                map[j] = Integer.parseInt(st.nextToken());
            }
            visited = new boolean[N + 1];
            for (int k = 1; k < N + 1; k++) {
                if(!visited[k]){
                    dfs(k);
                    cycle++;
                }
            }
            sb.append(cycle).append("\n");
        }
        System.out.println(sb);
        br.close();

    }

    private static void dfs(int start) {
        visited[start] = true;

        int next = map[start];
        if(!visited[next]){
            dfs(map[start]);
        }
    }
}

```
