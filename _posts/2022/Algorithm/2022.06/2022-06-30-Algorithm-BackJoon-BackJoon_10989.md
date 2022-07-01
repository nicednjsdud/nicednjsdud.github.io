---
published: true
title: BackJoon Algorithm 10989 수 정렬하기 3 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 수 정렬하기 3
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-30 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10989.png)


## 풀이


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10989 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int Test_count = Integer.parseInt(br.readLine());   // 테스트 개수
        int arr[] = new int[10001];                         // 배열 생성

        // when
        for (int i = 0; i < Test_count; i++) {
            arr[Integer.parseInt(br.readLine())]++;
        }
        // 0은 없으므로 1부터시작
        for (int i = 1; i < 10001; i++) {

            // 똑같은 수가 나올수 있을때를 대비
            while (arr[i] > 0) {
                sb.append(i).append('\n');
                arr[i]--;
            }
        }
        // then
        System.out.println(sb);
        br.close();

    }
}

```



