---
published: true
title: BackJoon Algorithm 탑 2493 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 탑
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

![alt](/assets/images/post/Algorithm/2493.png)

## 풀이

- 첫번째 방법으로 Stack 과 Stack 끼리는 깊은 복사가 되지 않는다. (실패)
- 두번째 방법으로는 ArrayList에 담아서 반복문으로 stack을 초기화 시켜서 넣었다. (메모리 초과)
- 마지막 방법으로 stack에 int 배열을 넣어 비교했다. (성공)
- 골드 문제부터는 메모리 까지 신경써야 한다는 것을 알았다..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Stack;
import java.util.StringTokenizer;

public class Back_2493 {
    public static void main(String[] args) throws IOException {
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        Stack<int[]> stack = new Stack<>();
        StringTokenizer st = new StringTokenizer(br.readLine());

        // when
        for (int i = 1; i <= N; i++) {
            int num = Integer.parseInt(st.nextToken());
            while (!stack.isEmpty()) {
                if (stack.peek()[1] >= num) {
                    sb.append(stack.peek()[0] + " ");
                    break;
                }
                stack.pop();
            }
            if (stack.isEmpty()) {
                sb.append("0 ");
            }
            stack.push(new int[]{i, num});
        }
        // then
        br.close();
        System.out.println(sb);
    }
}

```
