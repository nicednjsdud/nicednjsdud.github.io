---
title: BackJoon Algorithm 2490 윷놀이
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 윷놀이
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-14 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2490.png)




## 풀이

* if문 활용

```java
    import java.util.Scanner;
public class Back_2490 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // given
        int arr[]=new int[4];
        // when
        for(int j=0;j<3;j++) {
            int count=0;
            for (int i = 0; i < arr.length; i++) {
                arr[i] = sc.nextInt();
                if (arr[i] == 1) {
                    count++;
                }
            }
            //  then
            if (count == 4) {
                System.out.println("E");
            } else if (count == 3) {
                System.out.println("A");
            } else if (count == 2) {
                System.out.println("B");
            } else if (count == 1) {
                System.out.println("C");
            } else if(count==0){
                System.out.println("D");
            }

        }
    }
}

```


