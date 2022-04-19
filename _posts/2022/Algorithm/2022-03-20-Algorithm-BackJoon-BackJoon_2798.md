---
title: BackJoon Algorithm 2789 유학 금지
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 유학 금지
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2789.png)



## 풀이

* replaceAll() 메서드 활용
* replaceAll() 함수는 대상 문자열을 원하는 문자값으로 변환하는 함수이다.
* CAMBRIFGE 문자를 ""로 변경하면 지워진다.

```java
import java.util.*;
public class Back_2789 {
    public static void main(String[] args) {


        Scanner sc = new Scanner(System.in);
        //given
        String str = sc.next();
        // then
        System.out.println(str.replaceAll("[CAMBRIDGE]",""));
    }
}
```


