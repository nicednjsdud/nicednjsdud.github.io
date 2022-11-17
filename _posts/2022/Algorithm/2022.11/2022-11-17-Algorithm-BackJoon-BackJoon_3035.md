---
published: true
title: BackJoon Algorithm 스캐너 3035 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 스캐너
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/3035.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.StringTokenizer;


public class Back_3035 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        int R = Integer.parseInt(st.nextToken());
        int C = Integer.parseInt(st.nextToken());
        int ZR = Integer.parseInt(st.nextToken());
        int ZC = Integer.parseInt(st.nextToken());
        String[] str = new String[R];
        for (int i = 0; i < R; i++) {
            str[i] = br.readLine();
        }
        // when
        // 먼저 좌우 확대부터 확대하기
        if (ZC > 1) {
            for (int i = 0; i < R; i++) {
                String temp = "";
                for (int j = 0; j < C; j++) {
                    for (int k = 0; k < ZC; k++) {
                        temp += str[i].charAt(j);
                    }
                }
                str[i] = temp;
            }
        }
        // 위아래 확대하기
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < ZR; j++) {
                sb.append(str[i]).append("\n");
            }
        }
        // then
        System.out.println(sb);
        br.close();
    }
}
```
