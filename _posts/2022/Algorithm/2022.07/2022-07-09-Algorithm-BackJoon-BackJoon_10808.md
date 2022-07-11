---
published: true
title: BackJoon Algorithm 10808 알파벳 개수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 알파벳 개수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10808.png)

## 풀이

- 아스키 코드 숫자를 이용해 문제를 푼다.
- 알파벳 배열을 만들고 (26칸) 소문자는 -97을 해주면 0부터 26까지 나온다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10808 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
            int alphabet[]=new int[26];
        // when
        for(int i=0;i<str.length();i++){
            int alphabet_count=str.charAt(i)-97;
            alphabet[alphabet_count]++;
        }
        // then
        for (int i : alphabet) {
            System.out.print(i+" ");
        }
        br.close();
    }
}






```
