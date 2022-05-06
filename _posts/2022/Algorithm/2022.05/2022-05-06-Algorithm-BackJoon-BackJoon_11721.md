---
title: BackJoon Algorithm 11721 열 개씩 끊어 출력하기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 열 개씩 끊어 출력하기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-06 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11721.png)



## 풀이

* 10개마다 if문을 써 %로 끊어준다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_11721 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();             // 입력받기

        for(int i=0;i<str.length();i++){
            System.out.print(str.charAt(i));
            if(i%10==9){                        // 10개마다 끊어주기
                System.out.println();
            }
        }
    }
}

```


