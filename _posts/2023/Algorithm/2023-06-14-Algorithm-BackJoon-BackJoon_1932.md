---
published: true
title: BackJoon Algorithm 가로수 2485 (Java)
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
last_modified_at: "2023-06-12 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2485.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2485 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int arr[] = new int[N];

        for (int i = 0; i < arr.length; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        // 각 가로수간의 거리 구하기
        int dis[] = new int[N - 1];
        for (int i = 0; i < dis.length; i++) {
            dis[i] = arr[i + 1] - arr[i];
        }

        // 거리간의 최대 공약수 구하기
        int gcd = 0;
        gcd = gcd(dis[0], dis[1]);
        for (int i = 2; i < N - 2; i++) {
            gcd = gcd(gcd, dis[i]);
            if (gcd == 1) {
                break;
            }
        }
        // 각 거리/ 최대공약 -1값 모두 더하기
        int sum = 0;
        for (int i = 0; i < dis.length; i++) {
            sum += ((dis[i] / gcd) - 1);
        }
        System.out.println(sum);
        br.close();
    }

    private static int gcd(int a, int b) {
        while (b > 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;

    }
}


```
