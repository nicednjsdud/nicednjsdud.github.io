---
title: BackJoon Algorithm 2754 학점계산
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 학점계산
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

![alt](/assets/images/post/Algorithm/2754.png)



## 풀이

* switch 문 활용

```java
import java.util.*;
public class Back_2754 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        String grade=sc.next();
        //when
        switch(grade){
                case "A+":
                System.out.println(4.3);
                break;
                case "A0":
                System.out.println(4.0);
                break;
                case "A-":
                System.out.println(3.7);
                break;
                case "B+":
                System.out.println(3.3);
                break;
                case "B0":
                System.out.println(3.0);
                break;
                case "B-":
                System.out.println(2.7);
                break;
                case "C+":
                System.out.println(2.3);
                break;
                case "C0":
                System.out.println(2.0);
                break;
                case "C-":
                System.out.println(1.7);
                break;
                case "D+":
                System.out.println(1.3);
                break;
                case "D0":
                System.out.println(1.0);
                break;
                case "D-":
                System.out.println(0.7);
                break;
                case "F":
                System.out.println(0.0);
                break;
        }
    }
}
```


