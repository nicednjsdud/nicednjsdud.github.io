---
title: BackJoon Algorithm 2386 도비의 영어공부
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 도비의 영어공부
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-10 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2386.png)




## 풀이

* 배열로 받아 charAt()메서드를 활용하여 구별한다.

```java

import java.util.Scanner;

public class Back_2386 {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        while(true){
            int count=0;
            String str=sc.nextLine();
            if (str.equals("#")) {
                break;
            }
            for(int i=1;i<str.length();i++){
                    if(str.charAt(0)==str.charAt(i)||
                            str.charAt(0)== (str.charAt(i)+32)){
                        count++;
                    }

                }
            System.out.println(str.charAt(0)+ " " +count);
            }
            sc.close();
            }

    }
```


