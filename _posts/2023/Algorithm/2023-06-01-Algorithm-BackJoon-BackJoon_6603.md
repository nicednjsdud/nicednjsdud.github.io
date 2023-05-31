---
published: true
title: BackJoon Algorithm 6603 로또 (Java)
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
last_modified_at: "2023-06-01 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/6603.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_6603 {

    static int arr[];
    static boolean check[];

    static int T;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        while (true) {
            st = new StringTokenizer(br.readLine());
            T = Integer.parseInt(st.nextToken());
            if (T == 0) {
                break;
            }
            arr = new int[T];
            check = new boolean[T];
            for (int i = 0; i < T; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
                check[i] = false;
            }
            dfs(0, 0);
            System.out.println();
        }
    }

    private static void dfs(int depth, int start) {
        if (depth == 6) {
            for (int i = 0; i < T; i++) {
                if (check[i]) {
                    System.out.print(arr[i] + " ");
                }
            }
            System.out.println();
        }
        for (int i = start; i < T; i++) {
            check[i] = true;
            dfs(depth + 1, i + 1);
            check[i] = false;
        }
    }
}




```
