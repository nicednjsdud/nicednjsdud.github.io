---
published: true
title: BackJoon Algorithm 2941 크로아티아 알파벳 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 크로아티아 알파벳
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2941.png)

## 풀이

- contains 함수를 사용하여 입력 받은 str을 검사한다.
- 포함되있으면 크로아티아 알파벳을 @로 재정의헤서 개수를 센다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2941 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        String cro_alphabet[] = {"c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="};
        // when
        for(int i=0;i <cro_alphabet.length;i++){
            if(str.contains(cro_alphabet[i])){
                str = str.replace(cro_alphabet[i], "@");
            }
        }

        // then
        System.out.println(str.length());
        br.close();
    }
}

```
