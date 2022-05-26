---
title: BackJoon Algorithm 11719 그대로 출력하기 2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 그대로 출력하기 2
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11719.png)


## 풀이

* 입력의 개수가 주어지지않았다.
* hasNexLine메서드를 써서 입력의 끝을 받고 그대로 출력하다.

```java
import java.util.Scanner;

public class Back_11719 {
    public static void main(String[] args) {

        // given
        Scanner sc = new Scanner(System.in);
        // when
        while(sc.hasNextLine()){
            String input=sc.nextLine();
            System.out.println(input);
        }

        // then
        sc.close();
    }
}


```



