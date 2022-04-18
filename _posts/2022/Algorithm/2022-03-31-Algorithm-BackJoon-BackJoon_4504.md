---
title: BackJoon Algorithm 4504 배수찾기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 다음수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-31 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4504.png)


## 풀이

* 처음 입력 받은 배수를 다음 입력받은수로 나머지를구하고 0이면 배수이다.

```java
import java.util.Scanner;

public class Back_4504 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int number=sc.nextInt();
        boolean run =true;
        while(run){
            int multiple_count=sc.nextInt();
            if(multiple_count==0){
                break;
            }
            if(multiple_count%number==0){
                System.out.println(multiple_count+" is a multiple of "+number+".");
            }
            else{
                System.out.println(multiple_count+" is NOT a multiple of "+number+".");
            }

        }
        sc.close();
    }
}

```

