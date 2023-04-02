---
published: true
title: BackJoon Algorithm 2747 피보나치 수 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 7287 등록
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-31 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2747.png)

## 풀이

- 재귀함수로 풀면 시간 초과가 나온다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2747 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        System.out.println(pinbonacci(n));
        br.close();
    }

    private static int pinbonacci(int n) {

        if(n <= 1){
            return 1;
        }
        return pinbonacci(n - 1) + pinbonacci(n - 2);
    }
}


```

- 반복문으로 하나씩 구해서 하면 된다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2747 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int n1 = 0;
        int n2 = 0;
        int temp_1 = 0;
        int temp_2 = 0;

        for(int i = 0 ;i< n;i++){
            if(i == 0 || i == 1){
                n1 = 1;
                n2 = 1;
            }
            else{
                temp_1 = n1;
                temp_2 = n2;
                n1 = temp_2;
                n2 = temp_1 + temp_2;
            }
        }
        System.out.println(n2);
        br.close();
    }
}

```
