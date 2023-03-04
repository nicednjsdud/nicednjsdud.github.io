---
published: true
title: BackJoon Algorithm 계단 오르기 2579 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 계단 오르기 2579
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-04 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2643.png)

## 풀이

- dp

```java

import java.util.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2643 {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        List<int[]> list = new ArrayList<int[]>();

        int[][] arr = new int[N][2];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < 2; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
            // 폭 보다 길이가 더크면
            if (arr[i][1] > arr[i][0]) {
                list.add(new int[]{arr[i][1], arr[i][0]});
            } else {
                list.add(new int[]{arr[i][0], arr[i][1]});
            }
        }
        Collections.sort(list, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if (o1[0] == o2[0]) {
                    return o1[1] - o2[1];
                } else {
                    return o1[0] - o2[0];
                }
            }
        });
        int count = 0;
        int[] dp = new int[N];
        for (int i = 0; i < N; i++) {
            int cur[] = list.get(i);
            for (int j = 0; j < i; j++){
                int compare[] = list.get(j);
                //
                if(cur[0] >= compare[0] && cur[1] >= compare[1]){
                    dp[i] = Math.max(dp[i], dp[j]);
                }

            }
            dp[i]++;
            count = Math.max(count,dp[i]);
        }
        System.out.println(count);
    }
}


```
