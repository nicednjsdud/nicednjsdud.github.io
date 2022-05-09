---
title: BackJoon Algorithm 14581 팬들에게 둘러싸인 홍준
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 팬들에게 둘러싸인 홍준
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-09 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/14581.png)



## 풀이

* 그대로 입력받아서 출력하면 되는 문제이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_14581 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();                 // 문자열입력

        // then
        System.out.println(":fan::fan::fan:");
        System.out.println(":fan::"+str+"::fan:");
        System.out.println(":fan::fan::fan:");

        br.close();
    }
}


```


