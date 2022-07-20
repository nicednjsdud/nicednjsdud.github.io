---
published: true
title: BackJoon Algorithm 11005 진법 변환 2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 진법 변환 2
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11005.png)

## 풀이

- 진수 변환 문제이다.
- list에 담아 마지막부터 출력해준다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class Back_11005 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        long N = Long.parseLong(token.nextToken());
        int B = Integer.parseInt(token.nextToken());
        List<Character> list = new ArrayList<>();
        // when
        while (N > 0) {
            if (N % B < 10) {
                list.add((char) (N % B + '0'));
            } else {
                list.add((char) (N % B - 10 + 'A'));
            }
            N /= B;
        }
        for(int i=list.size()-1;i>=0;i--){
            System.out.print(list.get(i));
        }
        br.close();

        // then
    }
}




```
