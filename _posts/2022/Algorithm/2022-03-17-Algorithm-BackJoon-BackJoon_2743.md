---
title: BackJoon Algorithm 2743 단위길이 재기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 단위길이 재기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-17 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2743.png)



## 풀이

* String타입으로 받아 length() 메서드 활용

```java
import java.util.Scanner;

public class Back_2743 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        String str =sc.next();
        System.out.println(str.length());

    }
}
```


