---
published: true
title: BackJoon Algorithm 역원소 정렬 5648 (Java)
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
last_modified_at: "2024-02-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5648.png)

## 풀이

..

### 1. hasMoreTokens을 이용해 다음 토큰이 있는지 확인한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_5648 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        long arr[] = new long[n];

        while (n > 0) {
            while (st.hasMoreTokens()) {
                n--;
                String str = st.nextToken();
                StringBuilder temp = new StringBuilder();
                for (int i = str.length() - 1; i >= 0; i--) {
                    temp.append(str.charAt(i));
                }
                arr[n] = Long.parseLong(temp.toString());
            }

            if (n > 0) st = new StringTokenizer(br.readLine());
        }
        Arrays.sort(arr);
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
        br.close();
    }
}


```
