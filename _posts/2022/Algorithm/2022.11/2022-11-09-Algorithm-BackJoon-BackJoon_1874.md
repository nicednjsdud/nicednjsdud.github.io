---
published: true
title: BackJoon Algorithm 스택 수열 1874 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 재귀의 귀재
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1874_1.png)
![alt](/assets/images/post/Algorithm/1874_2.png)

## 풀이

- 스택(Last In First Out)의 구조이다.
- 스택의 push하는 순서는 반드시 오름차순을 지키도록 하여야 해서 start를 초기화 변수로 둔다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Stack;

public class Back_1874 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        Stack<Integer> stack = new Stack<>();
        int n = Integer.parseInt(br.readLine());
        int start = 0; // 초기화 용
        // when
        while (n-- > 0) {

            int num = Integer.parseInt(br.readLine());

            if (num > start) {
                for (int i = start + 1; i <= num; i++) {
                    stack.push(i);
                    sb.append("+").append("\n");
                }
                start = num;
            }
            // TOP이 num(입력받은 수) 이랑 같지 않다면
            else if (num != stack.peek()) {
                System.out.println("NO");
                System.exit(0);
            }
            stack.pop();
            sb.append("-").append("\n");
        }
        // then
        br.close();
        System.out.println(sb);
    }
}


```
