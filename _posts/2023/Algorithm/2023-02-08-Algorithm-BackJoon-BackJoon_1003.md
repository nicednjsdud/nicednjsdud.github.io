---
published: true
title: BackJoon Algorithm 피보나치 함수 1003 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 피보나치 함수 1003
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-02-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1003_2.png)
![alt](/assets/images/post/Algorithm/1003_1.png)

## 풀이

- 일반 예시 대로 풀면 시간초과가 나옵니다.
- 피보나치 함수을 나열하면 일정하게 나오는 숫자들이 있습니다.

![alt](/assets/images/post/Algorithm/1003_3.png)

- 이 규칙대로 풀어보면

```c
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1003 {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        int arr[] = new int[T];
        for(int i = 0; i< T;i++){
            arr[i] = Integer.parseInt(br.readLine());
        }
        // Fibonacci(n) 0 개수는 = Fibonacci(n-1) 1의개수
        // Fibonacci(n) 1 개수는 = Fibonacci(n-1) 0 + 1 의개수이다.

        for (int i = 0; i < T; i++) {
            int zero_count = 0;
            int first_count = 1;

            if(arr[i] == 0){
                zero_count = 1;
                first_count = 0;
                System.out.println(zero_count + " " + first_count);
            }
            else if(arr[i] == 1){
                System.out.println(zero_count + " " + first_count);
            }
            else{
                for (int j = 2; j <= arr[i]; j++) {
                    int temp = zero_count;
                    zero_count = first_count;
                    first_count = temp + first_count;
                }
                System.out.println(zero_count + " " + first_count);
            }

        }
        br.close();
    }



}

```
