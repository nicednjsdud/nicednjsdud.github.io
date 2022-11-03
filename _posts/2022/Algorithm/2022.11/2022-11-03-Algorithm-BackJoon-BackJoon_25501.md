---
published: true
title: BackJoon Algorithm 재귀의 귀재 25501 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 재귀의 귀재
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-01 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10870.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_25501 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int T = Integer.parseInt(br.readLine());
        String str[] = new String[T];
        for (int i = 0; i < T; i++) {
            str[i] = br.readLine();
        }
        // when
        for (int i = 0; i < T; i++) {
            String result = isPalindrome(str[i]);
            sb.append(result).append("\n");
        }
        // then
        br.close();
        System.out.println(sb);
    }

    private static String isPalindrome(String s) {
        return recursion(s, 0, s.length() - 1, 1);
    }

    private static String recursion(String s, int i, int length, int count) {
        String result = "";
        if (i >= length) {
            result = 1 + " " + count;
            return result;
        } else if (s.charAt(i) != s.charAt(length)) {
            result = 0 + " " + count;
            return result;
        } else {
            count++;
            return recursion(s, i + 1, length - 1, count);
        }

    }

}

```
