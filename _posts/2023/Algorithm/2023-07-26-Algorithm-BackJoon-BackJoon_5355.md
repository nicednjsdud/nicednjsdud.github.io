---
published: true
title: BackJoon Algorithm 화성 수학 5355 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-07-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5355.png)

## 풀이

```java
import java.io.BufferedReader;
import java.util.Scanner;

public class Back_5355 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StringBuilder sb = new StringBuilder();
        int T = Integer.parseInt(sc.nextLine());
        for (int i = 0; i < T; i++) {
            String str = sc.nextLine();
            String[] arr = str.split(" ");
            double num = Double.parseDouble(arr[0]);
            for (int j = 1; j < arr.length; j++) {
                if (arr[j].equals("@")) num *= 3;
                else if (arr[j].equals("%")) num += 5;
                else if (arr[j].equals("#")) num -= 7;
            }
            sb.append(String.format("%.2f", num)).append("\n");
        }
        System.out.println(sb);
        sc.close();
    }
}


```
