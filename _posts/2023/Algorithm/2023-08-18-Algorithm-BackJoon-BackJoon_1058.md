---
published: true
title: BackJoon Algorithm 친구 1058 (Java)
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
last_modified_at: "2023-08-18 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1058.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1058 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int arr[][] = new int[N][N];
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < N; i++) {
            String str = br.readLine();
            for (int j = 0; j < str.length(); j++) {
                if (str.charAt(j) == 'Y') {
                    arr[i][j] = 1;
                }
                else{
                    arr[i][j] = 9999;
                }
            }
        }
        // 경유지
        for (int k = 0; k < N; k++) {
            // 출발지
            for (int i = 0; i < N; i++) {
                // 도착지
                for (int j = 0; j < N; j++) {
                    if (arr[i][k] + arr[k][j] < arr[i][j]) {
                        arr[i][j] = arr[i][k] + arr[k][j];
                    }
                }
            }
        }

        for (int i = 0; i < N; i++) {
            int temp = 0;
            for (int j = 0; j < N; j++) {
                if (i == j) {
                    continue;
                } else {
                    if (arr[i][j] <= 2) {
                        temp++;
                    }
                }
            }
            max = Math.max(max, temp);
        }
        System.out.println(max);
    }

}


```
