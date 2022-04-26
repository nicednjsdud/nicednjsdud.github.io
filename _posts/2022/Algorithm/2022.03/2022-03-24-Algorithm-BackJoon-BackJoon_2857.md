---
title: BackJoon Algorithm 2857 FBI
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: FBI
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-24 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2857.png)



## 풀이

* contains() 함수 활용 
* contains() 함수는 대상 문자열에 특정 문자열이 포함되어 있는지 확인하는 함수이다.


```java
import java.util.Scanner;

public class Back_2857 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int count=0;
        String str[]=new String[5];
        for(int i=0;i<5;i++){
            str[i]=sc.nextLine();
            if(str[i].contains("FBI")){
                count++;
                System.out.print((i+1)+" ");
            }
        }
        if(count==0){
            System.out.println("HE GOT AWAY!");
        }
        sc.close();
    }
}

```

