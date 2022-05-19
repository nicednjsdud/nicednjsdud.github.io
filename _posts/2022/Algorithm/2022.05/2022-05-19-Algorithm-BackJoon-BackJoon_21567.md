---
title: BackJoon Algorithm 21567 숫자의 개수 2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 숫자의 개수 2 
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-19 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/21567_1.png)
![alt](/assets/images/post/Algorithm/21567_2.png)

## 풀이

* 숫자가 커져서 long형으로 받아야한다.
* long 배열을 만들어 문자열 하나씩 배열에 넣는다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_21567 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        long A = Integer.parseInt(br.readLine());    // A 입력
        long B = Integer.parseInt(br.readLine());    // B 입력
        long C = Integer.parseInt(br.readLine());    // C 입력
        long count[]= new long[10];                  // 배열 생성
        // when
        String sum = (A*B*C)+"";                    // 문자열로 변환

        for(int i=0;i<sum.length();i++){
            int ch = sum.charAt(i);
            count[ch-48]++;                         // char형을 인트배열에 담기
        }
        // then
        for(int i=0;i<count.length;i++) {
            System.out.println(count[i]);
        }
        br.close();
    }
}

```
