---
title: BackJoon Algorithm 16171 나는 친구가 적다 (Small) (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나는 친구가 적다 (Small) (Java)
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-12 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/16171.png)



## 풀이

* replaceAll 함수로 숫자를 제거하다.
* contains함수로 찾을 키워드가 있는지 확인하다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_16171 {
    public static void main(String[] args) throws IOException {
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();  // 교과서 내용필기
        String str2 = br.readLine(); // 찾을 키워드
        String replace = str.replaceAll("[0-9]","");
        // 0-9숫자는 ""로 재정의

        // then
        if(replace.contains(str2)){ // str2 문자열이 있으면 1출력
            System.out.println(1);  
        }
        else{
            System.out.println(0);
        }
    }
}

```


