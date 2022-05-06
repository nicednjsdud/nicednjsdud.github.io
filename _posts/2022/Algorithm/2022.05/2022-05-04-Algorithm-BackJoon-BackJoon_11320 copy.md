---
title: BackJoon Algorithm 11320 삼각 무늬 - 1
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 삼각무늬 - 1
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-04 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11320.png)



## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11320 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());  // 테스트 갯수

        // when
        for(int i=0;i<T;i++) {
            StringTokenizer token = new StringTokenizer(br.readLine());
            int A = Integer.parseInt(token.nextToken());  // A의 변의길이
            int B = Integer.parseInt(token.nextToken());  // B의 변의길이
            int count =0;                                 // 갯수

            // then
            if (A % B == 0) {

                count = (A / B) * (A / B);
                System.out.println(count);         // 두삼각형이 똑같으면
            } else {
                count = (A / B + 1) * (A / B + 1);
                System.out.println(count);
            }
        }
        br.close();



    }
}




```


