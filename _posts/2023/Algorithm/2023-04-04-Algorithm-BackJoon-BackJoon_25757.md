---
published: true
title: BackJoon Algorithm 25757 임스와 함께하는 미니게임 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 7287 등록
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-04 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/25757.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Back_25757 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());
        String game = st.nextToken();
        HashSet<String> hs = new HashSet<>();
        int count = 0;
        while (N-- > 0) {
            String user = br.readLine();
            count += hs.contains(user) ? 0 : 1;
            hs.add(user);
        }
        if (game.equals("Y")) {
            System.out.println(count);
        } else if (game.equals("F")) {
            System.out.println(count / 2);
        } else {
            System.out.println(count / 3);
        }
        br.close();
    }
}

```
