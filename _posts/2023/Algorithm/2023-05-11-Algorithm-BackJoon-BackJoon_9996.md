---
published: true
title: BackJoon Algorithm 9996 한국이 그리울 땐 서버에 접속하지  (Java)
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
last_modified_at: "2023-05-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9996.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_9996 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());

        String pattern = br.readLine();
        int sIndex = pattern.indexOf("*");

        String pStart = pattern.substring(0, sIndex);
        String pEnd = pattern.substring(sIndex + 1);

        int sLength = pStart.length();
        int eLength = pEnd.length();

        // * 뺀 길이
        int pLength = pattern.length() - 1;

        for (int i = 0; i < N; i++) {

            String str = br.readLine();
            if (str.length() < pLength) {
                sb.append("NE").append("\n");
            }
            else{
                String sStart = str.substring(0,sLength);
                String sEnd = str.substring(str.length() - eLength);

                if(sStart.equals(pStart) && sEnd.equals(pEnd)){
                    sb.append("DA").append("\n");
                }
                else{
                    sb.append("NE").append("\n");
                }
            }
        }
        System.out.println(sb);
        br.close();
    }
}


```
