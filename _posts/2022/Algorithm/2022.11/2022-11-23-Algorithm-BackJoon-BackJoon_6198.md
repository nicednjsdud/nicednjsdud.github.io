---
published: true
title: BackJoon Algorithm 옥탑 정원 꾸미기 6198 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 백설 공주와 일곱 난쟁이
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/6198_1.png)
![alt](/assets/images/post/Algorithm/6198_2.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Stack;

public class Back_6198 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        Stack<Integer> stack = new Stack<>();
        long count = 0;
        // when
        for (int i = 0; i < N; i++) {
            int num = Integer.parseInt(br.readLine());
            while (!stack.isEmpty() && stack.peek() <= num) {
                stack.pop();
            }
            stack.push(num);
            count += stack.size() - 1;
        }
        // then
        br.close();
        System.out.println(count);
    }
}



```
