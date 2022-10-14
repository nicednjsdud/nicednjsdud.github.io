---
published: true
title: BackJoon Algorithm 8958 OX퀴즈 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: OX퀴즈
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/8958.png)

## 풀이

- String 타입으로 문자열을 받고 받음과 동시에 for문으로 문자하나씩 비교해본다.
- 맨처음 charAt(0)이 'O'이면 합과 카운트를 1씩 증가시켜서 시작하는 if문을 둔다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_8958 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuffer sb = new StringBuffer();
        int total = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < total; i++) {
            String str = br.readLine();
            int count = 0;
            int sum = 0;
            if (str.charAt(0) == 'O') {
                count = 1;
                sum = 1;
            }
            for (int j = 1; j < str.length(); j++) {
                if (str.charAt(j) == 'O') {
                    count++;
                    sum += count;
                } else {
                    count = 0;

                }
            }
            sb.append(sum).append("\n");
        }
        // then
        System.out.println(sb);
        br.close();
    }
}

```
