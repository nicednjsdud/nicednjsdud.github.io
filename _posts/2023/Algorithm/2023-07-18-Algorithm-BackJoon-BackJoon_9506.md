---
published: true
title: BackJoon Algorithm 약수들의 합 9506 (Java)
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
last_modified_at: "2023-07-18 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9506.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_9506 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        while (true) {
            int n = Integer.parseInt(br.readLine());

            if (n == -1) {
                break;
            } else {
                int arr[] = new int[n];
                int sum = 0;
                arr[0] = 0;
                for (int i = 1; i < n; i++) {
                    if (n % i == 0) {
                        sum += i;
                        arr[i] = 1;
                    } else {
                        arr[i] = 0;
                    }
                }
                if (sum == n) {
                    sb.append(n).append(" = ");
                    for (int i = 1; i < arr.length/2 + 1; i++) {
                        if(arr[i] == 1){
                            if(i + 1 == arr.length/2 + 1){
                                sb.append(i).append("\n");
                            }
                            else{
                                sb.append(i).append(" + ");
                            }
                        }
                    }
                }
                else{
                    sb.append(n).append(" is NOT perfect.").append("\n");
                }
            }
        }
        System.out.println(sb);
        br.close();
    }
}
```
