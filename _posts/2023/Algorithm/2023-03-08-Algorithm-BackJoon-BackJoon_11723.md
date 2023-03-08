---
published: true
title: BackJoon Algorithm 집합 11723 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 집합 11723
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-07 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11723.png)

## 풀이

- 비트 연산자를 이용한 비트마스크를 써야한다.
- 안쓰고 그냥 풀면 시간초과가 나온다..

### 1) 맞은 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_11723 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();
        int M = Integer.parseInt(br.readLine());
        int S = 0;
        while (M-- > 0) {
            st = new StringTokenizer(br.readLine());
            String oper = st.nextToken();
            if (oper.equals("all")) S = (1 << 21) - 1;
            else if (oper.equals("empty")) S = 0;
            else {
                int num = Integer.parseInt(st.nextToken());
                if (oper.equals("add")) {
                    S |= (1 << num);
                } else if (oper.equals("remove")) {
                    S &= ~(1 << num);
                } else if (oper.equals("check")) {
                    sb.append((S & (1 << num)) != 0 ? 1 : 0).append("\n");
                } else if (oper.equals("toggle")) {
                    S ^= (1 << num);
                }
            }
        }
        System.out.println(sb);
        br.close();
    }
}


```

### 2) 틀린 풀이 (시간 초과)

```java

```
