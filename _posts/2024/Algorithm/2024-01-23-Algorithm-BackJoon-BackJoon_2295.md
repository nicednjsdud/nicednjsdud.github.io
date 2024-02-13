---
published: true
title: BackJoon Algorithm 세수의 합 2295 (Java)
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
last_modified_at: "2024-01-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2295.png)

## 풀이

### 1. Collections.binarySearch 를 이용한 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;


/**
 * 이분탐색 ( 주의 이분탐색은 항상 정렬을 해야함 )
 * A + B 를 먼저 더해 집합 list를 만든뒤 (list)
 * C를 대입하여 이전 arr에 가장 큰수를 구한다.
 */
public class Back_2295_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int arr[] = new int[N];
        List<Integer> list = new ArrayList<>();
        int sum = 0;
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                list.add(arr[i] + arr[j]);
            }
        }
        Arrays.sort(arr);
        Collections.sort(list);
        for (int i = N - 1; i >= 0; i--) {
            for (int j = 0; j < N; j++) {
                int gap = arr[i] - arr[j];
                if(Collections.binarySearch(list,gap) >= 0){
                    System.out.println(arr[i]);
                    return;
                }
            }
        }
        br.close();
    }

}


```

### 2. 직접 BinarySearch를 구현하여 만든 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;


/**
 * 이분탐색 ( 주의 이분탐색은 항상 정렬을 해야함 )
 * A + B 를 먼저 더해 집합 list를 만든뒤 (list)
 * C를 대입하여 이전 arr에 가장 큰수를 구한다.
 */
public class Back_2295 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int arr[] = new int[N];
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                list.add(arr[i] + arr[j]);
            }
        }
        Arrays.sort(arr);
        Collections.sort(list);
        for (int i = N - 1; i >= 0; i--) {
            for (int j = 0; j < N; j++) {
                int gap = arr[i] - arr[j];
                if (binarySearch(list, gap)) {
                    System.out.println(arr[i]);
                    return;
                }
            }
        }
        br.close();
    }

    private static boolean binarySearch(List<Integer> list, int gap) {
        int min = 0;
        int max = list.size() - 1;

        while (min < max) {
            int mid = (max + min) / 2;
            if(list.get(mid) == gap) return true;
            else if(list.get(mid) > gap) max = mid -1;
            else min = mid + 1;
        }
        return false;
    }

}

```
