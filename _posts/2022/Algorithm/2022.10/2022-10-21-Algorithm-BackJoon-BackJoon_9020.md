---
published: true
title: BackJoon Algorithm 골드바흐의 추측 9020 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 골드바흐의 추측
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9020.png)

- 에라토스테네스 체 알고리즘을 이용하면 쉽게 풀수있다.
- 입력받은 수 /2 에 가장 근접한 수가 가장 차이가 작은수 이므로 `prime / 2` 부터 돌려본다.

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_9020 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int test_count = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < test_count; i++) {

            int num = Integer.parseInt(br.readLine());
            boolean prime[] = new boolean[num + 1];

            // 0하고 1은 소수가 아니다.
            prime[0] = true;
            prime[1] = true;

            // 에라토스테네스 체
            for (int j = 2; j < Math.sqrt(prime.length); j++) {
                for (int k = j * j; k < prime.length; k += j) {
                    prime[k] = true;
                }
            }

            for(int j = prime.length/2; j<= prime.length ; j++){

                // 소수일때
                if (prime[j] == false){

                    int prime_count = num - j;

                    // 뺀수도 정수일때 가장 근접한 수가 차가 가장적다.
                    if( prime[prime_count] == false){
                        int first_count = prime_count;
                        int last_count = j;
                        sb.append(first_count).append(" ").append(last_count).append("\n");
                        break;
                    }
                }
            }

        }
        // then
        System.out.println(sb);
        br.close();
    }
}




```
