---
published: true
title: BackJoon Algorithm 균형잡힌 세상 4949 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 균형잡힌 세상
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-12-19 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4949.png)

## 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Stack;

public class Back_4949 {
    public static void main(String[] args) throws IOException {


        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        while (true) {
            String str = br.readLine();

            if (str.equals(".")) break;

            String result = compare_str(str);
            sb.append(result).append("\n");
        }
        System.out.println(sb);
        br.close();
    }

    private static String compare_str(String str) {

        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < str.length(); i++) {

            // 여는 괄호가 대괄호 혹은 소괄호 일 경우
            if (str.charAt(i) == '(' || str.charAt(i) == '[') {
                stack.push(str.charAt(i));
            }
            // 닫는 괄호가 소괄호 일 경우
            else if (str.charAt(i) == ')') {

                // 스택이 비어있거나 여는 괄호가 ( 가 아닐경우
                if (stack.empty() || stack.peek() != '('){
                    return "no";
                }
                else stack.pop();
            }
            // 닫는 괄호가 대괄호 일 경우
            else if (str.charAt(i) == ']') {

                // 스택이 비어있거나 여는 괄호가 [ 가 아닐경우
                if (stack.empty() || stack.peek() != '['){
                    return "no";
                }
                else stack.pop();
            }

        }
        if(stack.empty()) return "yes";
        else return "no";
    }
}




```
