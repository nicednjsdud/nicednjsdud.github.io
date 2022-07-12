---
published: true
title: BackJoon Algorithm 11656 접미사 배열 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 접미사 배열
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-12 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11656.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_11656 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String S = br.readLine();
        String[] str = new String[S.length()];
        // when
        for(int i=0;i<S.length();i++){
            String S_charAt="";
            for(int j=i;j<S.length();j++){
                S_charAt+=S.charAt(j);
            }
            str[i]=S_charAt;
        }
        Arrays.sort(str);
        // then
        br.close();
        for (String s : str) {
            System.out.println(s);
        }
    }
}
```
