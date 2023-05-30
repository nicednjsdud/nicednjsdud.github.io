---
published: true
title: BackJoon Algorithm 18111 마인크래프트 (Java)
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
last_modified_at: "2023-05-29 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/18111.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_18111 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());
        int arr[][] = new int[N][M];
        int max = 0;
        int min = 0;
        int height = 0;
        int time = 99999999;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                if (i == 0 && j == 0) {
                    min = arr[i][j];
                    max = arr[i][j];
                } else {
                    if (arr[i][j] > max) {
                        max = arr[i][j];
                    } else if (arr[i][j] < min) {
                        min = arr[i][j];
                    }
                }
            }
        }
        for (int k = max; k >= min; k--) {
            int current_time = 0;
            int item = B;

            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {

                    if (arr[i][j] > k) {
                        item += (arr[i][j] - k);
                        current_time += 2 * (arr[i][j] - k);
                    } else if (arr[i][j] < k) {
                        item -= (k - arr[i][j]);
                        current_time += (k - arr[i][j]);
                    }
                }
            }
            if (item >= 0 && time > current_time) {
                height = k;
                time = current_time;
            }
        }
        System.out.println(time + " " + height);
        br.close();
    }
}


```
