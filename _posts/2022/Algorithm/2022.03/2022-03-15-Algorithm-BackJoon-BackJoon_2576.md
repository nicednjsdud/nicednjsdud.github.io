---
title: BackJoon Algorithm 2576 홀수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 홀수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-15 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2576.png)



## 풀이

* 2로 나눴을때 나머지가 0이면 짝수 아니면 홀수

```java
import java.util.Scanner;

public class Back_2576 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // given
        int min=100;
        int sum=0;
        int count=0;
        // when
        for(int i=0;i<7;i++){
            int number=sc.nextInt();
            if(number%2!=0){
                count++;
                sum+=number;
                if(number<min){
                    min=number;
                }
            }

        }
        sc.close();
        // then
        if(count==0){
            System.out.println(-1);
        }
        else {
            System.out.println(sum);
            System.out.println(min);
        }
    }
}
```


