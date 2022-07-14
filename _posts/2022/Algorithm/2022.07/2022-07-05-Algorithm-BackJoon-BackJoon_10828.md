---
published: true
title: BackJoon Algorithm 10828 스택 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 스택
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-05 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10828.png)
![alt](/assets/images/post/Algorithm/10828_1.png)

## 풀이

- 스택의 자료구조이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10828 {
    public static int[] stack;
    public static int size = 0;

    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token;
        int order_count = Integer.parseInt(br.readLine());
        stack = new int[order_count];
        // when

        while (order_count-- > 0) {
            token = new StringTokenizer(br.readLine() + " ");
            switch (token.nextToken()) {

                case "push":
                    push(Integer.parseInt(token.nextToken()));
                    break;
                case "pop":
                    sb.append(pop()).append('\n');
                    break;
                case "size":
                    sb.append(size()).append('\n');
                    break;
                case "empty":
                    sb.append(empty()).append('\n');
                    break;
                case "top":
                    sb.append(top()).append('\n');
                    break;
            }
        }
        // then
        System.out.println(sb);
        br.close();
    }


    public static void push(int n) {          // push
        stack[size] = n;
        size++;
    }

    public static int pop() {                     // pop
        if (size == 0) {
            return -1;
        } else {
            int final_count = stack[size - 1];
            stack[size - 1] = 0;
            size--;
            return final_count;
        }
    }

    public static int size() {                          // size
        return size;
    }

    public static int empty() {                     // empty
        if (size == 0) {
            return 1;
        } else {
            return 0;
        }
    }

    public static int top() {                       // top
        if (size == 0) {
            return -1;
        } else {
            return stack[size - 1];
        }
    }


}


```
