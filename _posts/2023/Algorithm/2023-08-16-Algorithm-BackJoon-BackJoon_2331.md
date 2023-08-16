---
published: true
title: BackJoon Algorithm 반복수열 2331 (Java)
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
last_modified_at: "2023-08-16 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2331.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Back_2331 {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int A = Integer.parseInt(st.nextToken());
        int P = Integer.parseInt(st.nextToken());

        ArrayList<Integer> arr = new ArrayList<>();
        arr.add(A);

        while (true) {
            int num = arr.get(arr.size() - 1);
            int result = 0;
            while (num != 0) {
                result += (int) Math.pow(num % 10, P);
                num /= 10;
            }

            if(arr.contains(result)){
                int ans = arr.indexOf(result);
                System.out.println(ans);
                break;
            }
            arr.add(result);
        }
        br.close();
    }
}


```
