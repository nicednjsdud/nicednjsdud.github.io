---
title: BackJoon Algorithm 4458 줄번호
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 줄번호
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-29 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4470.png)


## 풀이


```java
import java.util.Scanner;

public class Back_4470 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int num=sc.nextInt();
        sc.nextLine();
        String str[]=new String[num];
        for(int i=0;i<num;i++){
            str[i]=sc.nextLine();
        }
        for(int i=0;i<num;i++){
            System.out.println((i+1)+". "+str[i]);
        }
    }
}


```

