---
published: true
title: BackJoon Algorithm 10867 중복 빼고 정렬하기 (Java)
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
last_modified_at: "2023-05-30 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10867.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Back_10867 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        HashSet<Integer> hashSet = new HashSet<>();
        for (int i = 0; i < N; i++) {
            hashSet.add(Integer.parseInt(st.nextToken()));
        }

        ArrayList<Integer> arr = new ArrayList<>(hashSet);
        Collections.sort(arr);

        for (Integer integer : arr) {
            sb.append(integer).append(" ");
        }
        System.out.println(sb);
        br.close();
    }
}



```
