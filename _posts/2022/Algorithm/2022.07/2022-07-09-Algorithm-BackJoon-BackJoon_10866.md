---
published: true
title: BackJoon Algorithm 10866 덱 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 덱
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10866.png)
![alt](/assets/images/post/Algorithm/10866_1.png)
![alt](/assets/images/post/Algorithm/10866_2.png)

## 풀이

![alt](/assets/images/post/Algorithm/deck.png)

- 덱의 자료구조를 이해하면 쉽게 접근할수 있는 문제 였던 것 같다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.StringTokenizer;

public class Back_10866 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token;
        Deque<Integer> deque = new ArrayDeque<>();
        int order_count = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < order_count; i++) {
            token = new StringTokenizer(br.readLine(), " ");

            switch (token.nextToken()) {
                case "push_front":
                    deque.addFirst(Integer.parseInt(token.nextToken()));
                    break;
                case "push_back":
                    deque.addLast(Integer.parseInt(token.nextToken()));
                    break;
                case "pop_front":
                    if (deque.size() == 0) {
                        sb.append(-1).append('\n');
                    } else {
                        sb.append(deque.pollFirst()).append('\n');
                    }
                    break;
                case "pop_back":
                    if (deque.size() == 0) {
                        sb.append(-1).append('\n');
                    } else {
                        sb.append(deque.pollLast()).append('\n');
                    }
                    break;
                case "size":
                    sb.append(deque.size()).append('\n');
                    break;
                case "empty":
                    if (deque.isEmpty()) {
                        sb.append(1).append('\n');
                    } else {
                        sb.append(0).append('\n');
                    }
                    break;
                case "front":
                    if (deque.size() == 0) {
                        sb.append(-1).append('\n');
                    } else {
                        sb.append(deque.peekFirst()).append('\n');
                    }
                    break;
                case "back":
                    if (deque.size() == 0) {
                        sb.append(-1).append('\n');
                    } else {
                        sb.append(deque.peekLast()).append('\n');
                    }
                    break;
            }
        }
        // then
        br.close();
        System.out.println(sb);
    }

}






```
