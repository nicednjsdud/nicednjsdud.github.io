---
published: true
title: BackJoon Algorithm 음계 2920 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 음계 2920
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-02-25 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2920.png)

## 풀이

```java
import java.util.Scanner;

public class Back_2920 {
    public static void main(String[] args)  {

        Scanner sc = new Scanner(System.in);

        int count = 0;
        boolean upDown = false;
        String msg = "";
        for(int i = 0 ; i< 8; i++){
            int scale = sc.nextInt();
            if(i == 0){
                count = scale;
                if(count == 1){
                    upDown = true;
                }
            }
            else{
                if(upDown){
                    count ++ ;
                }
                else{
                    count -- ;
                }
            }
            if(scale == count){
                continue;
            }
            else{
                msg = "mixed";
            }
        }
        if(msg == ""){
            if(upDown){
                msg = "ascending";
            }
            else{
                msg = "descending";
            }
        }
        System.out.println(msg);
    }
}


```
