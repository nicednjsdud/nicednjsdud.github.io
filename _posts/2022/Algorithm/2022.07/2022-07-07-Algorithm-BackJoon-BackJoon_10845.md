---
published: true
title: BackJoon Algorithm 10845 큐 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 큐
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-07 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10845.png)
![alt](/assets/images/post/Algorithm/10845_1.png)

## 풀이

- 큐의 자료구조 구현이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10845 {

    public static int[] queue;

    public static int size = 0;

    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token;
        int order_count = Integer.parseInt(br.readLine());
        queue = new int[order_count];
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
                case "front":
                    sb.append(front()).append('\n');
                    break;
                case "back":
                    sb.append(back()).append('\n');
            }
        }
        // then
        System.out.println(sb);
        br.close();
    }

    public static void push(int n) {
        queue[size] = n;
        size++;
    }

    public static int pop() {
        if (size == 0) {
            return -1;
        }
        int first_count = queue[0];
        if (size == 1) {
            size = 0;
        } else {
            for (int i = 1; i < size; i++) {
                queue[i-1]=queue[i];
            }
            size--;
        }
        return first_count;
    }
    public static int empty(){
        if(size==0){
            return 1;
        }
        else{
            return 0;
        }
    }
    public static int size(){
        return size;
    }
    public static int front(){
        if(size==0){
            return -1;
        }
        int number = queue[0];
        return number;
    }
    public static int back(){
        if(size==0){
            return -1;
        }
        int number = queue[size-1];
        return number;
    }

}

```
