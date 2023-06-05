---
published: true
title: BackJoon Algorithm 5430 AC (Java)
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
last_modified_at: "2023-06-05 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5430.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Deque;
import java.util.LinkedList;

public class Back_5430 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for (int i = 0; i < T; i++) {
            String str = br.readLine();
            int n = Integer.parseInt(br.readLine());

            String arrStr = br.readLine();
            Deque<Integer> deq = new LinkedList<>();
            for (String s : arrStr.substring(1, arrStr.length() - 1).split(",")) {
                if (!s.equals("")) {
                    deq.add(Integer.valueOf(s));
                }
            }
            System.out.println(ac(deq, str));
        }

    }

    private static String ac(Deque<Integer> deq, String commands) {
        boolean reverse = false;

        for (char command : commands.toCharArray()) {
            if (command == 'R') {
                // 뒤집기
                reverse = !reverse;
            } else {
                if (deq.size() == 0) {
                    return "error";
                }
                if (reverse) {
                    deq.removeLast();
                } else {
                    deq.removeFirst();
                }
            }

        }
        StringBuilder sb = new StringBuilder("[");
        while (!deq.isEmpty()) {
            sb.append(reverse ? deq.removeLast() : deq.removeFirst());
            if (deq.size() != 0) {
                sb.append(",");
            }
        }
        sb.append("]");
        return sb.toString();

    }
}



```
