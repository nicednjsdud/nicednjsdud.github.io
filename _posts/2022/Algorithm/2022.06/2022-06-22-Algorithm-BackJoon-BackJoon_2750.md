---
published: true
title: BackJoon Algorithm 2750 수 정렬하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 수 정렬하기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-22 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2750.png)


## 풀이

* Arrays.sort 사용

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_2750 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        int arr[]=new int[N];
        // when
        for(int i=0;i<N;i++){
            arr[i]=Integer.parseInt(br.readLine());
        }
        Arrays.sort(arr);           // 오름차순 정렬
        // then
        for(Integer i: arr){
            sb.append(i);
            sb.append("\n");
        }
        System.out.println(sb);
    }
}

```



