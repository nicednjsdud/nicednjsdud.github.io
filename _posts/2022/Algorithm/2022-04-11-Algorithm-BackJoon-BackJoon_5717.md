---
title: BackJoon Algorithm 5717
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 상근이의 친구들
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-11 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5717.png)


```java
    import java.util.Scanner;

public class Back_5717 {
    public static void main(String[] args) {

        // 입력
        Scanner sc = new Scanner(System.in);

        while(true){
            int boy=sc.nextInt();
            int girl= sc.nextInt();
            if(boy==0 && girl==0){
                break;
            }
            int sum=boy+girl;
            System.out.println(sum);
        }
    }
}

```

