---
published: true
title: BackJoon Algorithm 10816 숫자 카드2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 10816 숫자 카드2
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10816.png)

## 풀이

1. 이분탐색으로 정렬된 배열에서 가장 빠른 같은 수를 찾는다.
2. else 로 같은 수를 거른다음 다른 수가 나오는 자리를 찾아 (다른수 - 같은수(처음)) 을 해준다.

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Back_10816 {
    public static void main(String[] args) throws IOException {

        Scanner sc = new Scanner(System.in);
        StringBuilder sb = new StringBuilder();
        int N = sc.nextInt();
        int arr[] = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = sc.nextInt();
        }
        Arrays.sort(arr);
        int M = sc.nextInt();

        for (int i = 0; i < M; i++) {
            int check = sc.nextInt();
            sb.append((lowerBinarySearch(arr, check) - upperBinarySearch(arr, check))).append(" ");
        }
        System.out.println(sb);
        sc.close();
    }

    private static int upperBinarySearch(int[] arr, int check) {
        int start = 0;
        int mid = 0;
        int end = arr.length;
        while (start < end) {
            mid = (end + start) / 2;
            if (arr[mid] >= check) {
                end = mid;
            } else {
                start = mid + 1;
            }
        }
        return start;
    }

    private static int lowerBinarySearch(int[] arr, int check) {
        int start = 0;
        int mid = 0;
        int end = arr.length;
        while (start < end) {
            mid = (end + start) / 2;
            if (arr[mid] > check) {
                end = mid;
            } else {
                start = mid + 1;
            }
        }
        return start;
    }
}


```
