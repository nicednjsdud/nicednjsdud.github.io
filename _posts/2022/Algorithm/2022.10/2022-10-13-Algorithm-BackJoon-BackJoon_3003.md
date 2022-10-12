---
published: true
title: BackJoon Algorithm 3003 킹,퀸,룩,나이트,폰 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 킹,퀸,룩,나이트,폰
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-13 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/3003.png)

## 풀이

- 맨처음 배열에 원래의 수를 담아놓은 후 입력받을때 계산한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_3003 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int chess[] = {1, 1, 2, 2, 2, 8};
        // when
        for (int i = 0; i < 6; i++) {
            int inputCount = Integer.parseInt(token.nextToken());
            if (chess[i] != inputCount) {
                chess[i] = chess[i] - inputCount;
            } else
                chess[i] = 0;
        }
        // then
        for (int i = 0; i < chess.length; i++) {
            System.out.print(chess[i] + " ");
        }
        br.close();
    }
}



```
