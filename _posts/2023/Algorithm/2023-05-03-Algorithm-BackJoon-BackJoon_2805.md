---
published: true
title: BackJoon Algorithm 2805 나무자르기  (Java)
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
last_modified_at: "2023-05-03 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2805.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_2805 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int arr[] = new int[N];
        long max = 0;

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            if (max < arr[i]) {
                max = arr[i];
            }
        }
        Arrays.sort(arr);
        max ++;

        long mid = 0;
        long min = 0;

        while (min < max) {

            mid = (max + min) / 2;

            long length = 0;
            for (int i = 0; i < N; i++) {
                if(arr[i] > mid){
                    length += arr[i] - mid;
                }
            }

            if(length < M){
                // 자른 길이가 자를려고 한 길이보다 작을때
                max = mid;
            }
            else{
                min = mid + 1;
            }
        }
        System.out.println(min - 1);
        br.close();
    }
}

```