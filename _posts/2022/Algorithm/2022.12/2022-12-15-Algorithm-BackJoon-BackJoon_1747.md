---
published: true
title: BackJoon Algorithm 소수&팰린드롬 1747 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 소수&팰린드롬 1747
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-12-15 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1747.png)

## 풀이

- 먼저 팰린드롬인지를 확인한 후 그 수에 대해 소수 인지도 확인한다.

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1747 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        boolean is_ok = true;
        // when
        while (true) {
            if(N == 1){
                System.out.println(2);
                break;
            }
            String temp_N = N + "";
                for (int i = 0; i <= temp_N.length() / 2; i++) {
                    if (temp_N.charAt(i) == temp_N.charAt(temp_N.length() - i -1))
                        is_ok = false;
                    else {
                        is_ok = true;
                        break;
                    }
                }
            if (!is_ok) {
                for (int i = 2; i <= (int) Math.sqrt(N); i++) {
                    if (N % i == 0) {
                        is_ok = true;
                        break;
                    }
                }
            }
            if (!is_ok) {
                // then
                System.out.println(N);
                System.exit(0);
            }
            N++;
        }
    }
}


```
