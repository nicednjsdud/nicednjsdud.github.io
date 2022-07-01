---
published: true
title: BackJoon Algorithm 11650 좌표 정렬하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 좌표 정렬하기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-24 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11650.png)


## 풀이

* 2차원 배열은 Array.sort()를 쓸수없기때문에 람다식으로 풀면된다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_11650 {

    public static void main(String[] args) throws IOException {


        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        int arr[][] = new int[N][2];
        // when
        StringTokenizer token;
        for (int i = 0; i < N; i++) {
            token = new StringTokenizer(br.readLine());
            arr[i][0] = Integer.parseInt(token.nextToken());
            arr[i][1] = Integer.parseInt(token.nextToken());
        }
        Arrays.sort(arr, (s1, s2) -> {
            if (s1[0] == s2[0]) {
                return s1[1] - s2[1];
            } else {
                return s1[0] - s2[0];
            }
        });
        // then
        for (int i = 0; i < N; i++) {
            sb.append(arr[i][0]).append(" ").append(arr[i][1]).append('\n');
        }
        System.out.println(sb);
        br.close();
    }

}




```



