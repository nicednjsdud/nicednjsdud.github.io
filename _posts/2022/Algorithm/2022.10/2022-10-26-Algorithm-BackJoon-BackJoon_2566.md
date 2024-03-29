---
published: true
title: BackJoon Algorithm 최댓값 2566 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 최댓값
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2566_1.png)
![alt](/assets/images/post/Algorithm/2566_2.png)

## 풀이

```java


import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Back_2566 {
    public static void main(String[] args) throws IOException {

        //     given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int max = 0;
        int arr[][] = new int[9][9];
        int row = 0;
        int col = 0;
        //    when
        for (int i = 0; i < 9; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 9; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                if (max < arr[i][j]) {
                    max = arr[i][j];
                    row = i;
                    col = j;
                }
            }
        }
        //    then
        System.out.println(max);
        System.out.println((row+1) + " " + (col+1));
        br.close();
    }
}

```
