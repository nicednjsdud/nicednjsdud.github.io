---
published: true
title: BackJoon Algorithm 제로 10773 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 제로
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10773.png)

## 풀이

- 만약 입력받은 수가 0이면 전에 꺼를 꺼내야하기 때문에 stack[0] 을 먼저 대입한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Stack;

public class Back_10773 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        Stack<Integer> stack = new Stack<>();
        int K = Integer.parseInt(br.readLine());
        int num = Integer.parseInt(br.readLine());
        int sum = 0;

        // 최근거를 지워야하기때문에 stack[0]은 넣고시작
        stack.push(num);
        // when
        for (int i = 1; i < K; i++) {
            num = Integer.parseInt(br.readLine());
            if (num == 0) {
                stack.pop();
            } else {
                stack.push(num);
            }
        }
        for (int i = 0; i < stack.size(); i++) {
            sum += stack.get(i);
        }
        // then
        System.out.println(sum);
        br.close();
    }
}



```
