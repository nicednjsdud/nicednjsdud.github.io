---
published: true
title: BackJoon Algorithm 18258 큐 2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 18258 큐 2 (Java)
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/18258.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Deque;
import java.util.LinkedList;
import java.util.StringTokenizer;

public class Back_18258 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        Deque<Integer> deque = new LinkedList<>();
        StringTokenizer st;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine()," ");
            String str = st.nextToken();
            if(str.equals("push")){
                int num = Integer.parseInt(st.nextToken());
                deque.offer(num);
            }
            else if(str.equals("front")){
                Integer peek = deque.peek();
                if(peek == null){
                    sb.append(-1).append("\n");
                }
                else{
                    sb.append(peek).append("\n");
                }
            }
            else if(str.equals("pop")){
                Integer poll = deque.poll();
                if(poll == null){
                    sb.append(-1).append("\n");
                }
                else{
                    sb.append(poll).append("\n");
                }
            }
            else if(str.equals("size")){
                int size = deque.size();
                sb.append(size).append("\n");
            }
            else if(str.equals("empty")){
                if(deque.isEmpty()) {
                    sb.append(1).append("\n");
                }
                else{
                    sb.append(0).append("\n");
                }
            }
            else if(str.equals("back")){
                Integer integer = deque.peekLast();
                if(integer == null){
                    sb.append(-1).append("\n");
                }
                else{
                    sb.append(integer).append("\n");
                }
            }

        }
        br.close();
        System.out.println(sb);
    }
}



```