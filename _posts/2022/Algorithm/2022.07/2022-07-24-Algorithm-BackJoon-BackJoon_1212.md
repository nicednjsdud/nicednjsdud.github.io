---
published: true
title: BackJoon Algorithm 1212 8진수 2진수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 8진수 2진수
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-24 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1212.png)

## 풀이

- 8진수에서 -> 10진수 ->2진수로 넘어가면 시간초과가 일어난다.
- 하나씩쪼개서 바로 2진수로 변환한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1212 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();
        StringBuilder sb = new StringBuilder();
        // when
        for (int i = 0; i < s.length(); i++) {
            int n = s.charAt(i) - '0';
            if (n >= 4) {
                sb.append(1);
                n -= 4;
            } else {
                sb.append(0);
            }
            if (n >= 2) {
                sb.append(1);
                n -= 2;
            } else {
                sb.append(0);
            }
            if (n == 1) {
                sb.append(1);
                n -= 1;
            }
            else{
                sb.append(0);
            }
        }
        if(s.charAt(0)=='1'){
            sb.delete(0,2);
        }
        else if(s.charAt(0)=='2'||s.charAt(0)=='3'){
            sb.delete(0,1);
        }
        else if(s.charAt(0)=='0'){
            sb.delete(0,2);
        }
        // then
        System.out.println(sb);
        br.close();
    }
}

```
