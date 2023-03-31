---
published: true
title: BackJoon Algorithm 수 이어 쓰기 1515 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 수 이어 쓰기 1515
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-23 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1515.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1515 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        int pointer = 0;
        int count = 0;

        while(count++ <= 30000){
            String temp = String.valueOf(count);
            for(int i = 0 ; i< temp.length(); i++){
                if(temp.charAt(i) == str.charAt(pointer)){
                    pointer ++;
                }
                if(pointer == str.length()){
                    System.out.println(count);
                    return;
                }
            }
        }
        br.close();
    }
}


```
