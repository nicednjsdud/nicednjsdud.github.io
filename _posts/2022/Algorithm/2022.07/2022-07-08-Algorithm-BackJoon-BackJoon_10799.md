---
published: true
title: BackJoon Algorithm 10799 쇠막대기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 쇠막대기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-08 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10799.png)
![alt](/assets/images/post/Algorithm/10799_1.png)

## 풀이

![alt](/assets/images/post/Algorithm/stack.png)

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Stack;

public class Back_10799 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();       // 공백 값 입
        Stack<Character> stack = new Stack<>();
        int result = 0;
        // when
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == '(') {  // ( 막대기 추가
                stack.push('(');
                continue;
            }
            if (str.charAt(i) == ')') {
                stack.pop();    // ) pop 실행

                if (str.charAt(i - 1) == '(') {   // 그 전 괄호가 열린 괄호면 레이저의미
                    result += stack.size();
                }else{
                    result ++;
                }
            }
        }

        // then
        System.out.println(result);
        br.close();
    }
}
```
