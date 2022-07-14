---
published: true
title: BackJoon Algorithm 11004 K번째 수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: K번째 수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-04 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11104.png)

## 풀이

- Collection.sort() 이용해 오름차순으로 정렬한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.StringTokenizer;

public class Back_11004 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int Test_count = Integer.parseInt(token.nextToken());
        int Counting_num = Integer.parseInt(token.nextToken());

        ArrayList<Integer> arr = new ArrayList<>();
        token = new StringTokenizer(br.readLine());
        for (int i = 0; i < Test_count; i++) {
            arr.add(Integer.parseInt(token.nextToken()));
        }
        // when
        // 오름차순 정렬
        Collections.sort(arr);

        // then
        System.out.println(arr.get(Counting_num-1));
    }
}


```
