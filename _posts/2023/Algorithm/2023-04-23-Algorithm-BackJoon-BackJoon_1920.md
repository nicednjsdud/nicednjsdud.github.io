---
published: true
title: BackJoon Algorithm 1920 수 찾기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 18406 럭키 스트레이트 (Java)
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-22 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1920.png)

## 풀이

1. 순차 탐색으로 풀면 시간 초과가 나온다.
2. 이분탐색으로 풀어야한다.

```java

import java.io.IOException;
import java.util.Arrays;
import java.util.Scanner;

public class Back_1920 {
    public static void main(String[] args) throws IOException {

        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();

        int[] arr = new int[N];
        for (int i = 0; i < N; i++) {
            arr[i] = sc.nextInt();
        }
        Arrays.sort(arr);

        int M = sc.nextInt();
        int[] check = new int[M];
        for (int i = 0; i < M; i++) {
            check[i] = sc.nextInt();
        }

        for (int i = 0; i < M; i++) {
            System.out.println(binarySearch(arr, check[i]));
        }
    }

    private static int binarySearch(int[] arr, int check) {
        int low = 0;
        int high = arr.length - 1;
        int mid = 0;

        while (low <= high) {
            mid = (low + high) / 2;
            if (arr[mid] == check) return 1;
            else if (arr[mid] > check) high = mid - 1;
            else if (arr[mid] < check) low = mid + 1;
        }
        return 0;
    }
}



```
