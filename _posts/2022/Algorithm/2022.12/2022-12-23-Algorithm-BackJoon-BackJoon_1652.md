---
published: true
title: BackJoon Algorithm 누울 자리를 찾아라 1652 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 누울 자리를 찾아라
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-12-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1652.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1652 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        String str[] = new String[N];
        int row = 0;
        int col = 0;
        for (int i = 0; i < N; i++) {
            str[i] = br.readLine();
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {

                if (str[i].charAt(j) == '.') {
                    // 가로로 누울 수 있는지 체크
                    // 두칸이 있는지 확인
                    if (j + 1 < N && str[i].charAt(j + 1) == '.') {
                        // 그다음에 벽이나 짐이있는지 있는지 확인한다.
                        if (j + 2 >= N || (j + 2 < N && str[i].charAt(j + 2) == 'X')) {
                            row++;
                        }
                    }

                    // 세로로 누울수 있는지 체크
                    // 두칸이 있는지 확인
                    if (i + 1 < N && str[i + 1].charAt(j) == '.') {
                        // 그다음에 (세로) 벽이나 짐이 있는지 확인한다.
                        if (i + 2 >= N || (i + 2 < N && str[i + 2].charAt(j) == 'X')) {
                            col++;
                        }
                    }
                }
            }
        }
        System.out.println(row + " " + col);
        br.close();
    }
}


```
