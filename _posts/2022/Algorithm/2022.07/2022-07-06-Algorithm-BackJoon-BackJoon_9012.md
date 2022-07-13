---
published: true
title: BackJoon Algorithm 9012 괄호 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 괄호
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-06 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9012.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_9012 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int test_count = Integer.parseInt(br.readLine());
        String str = "";
        int check = 0;
        // when
        for (int i = 0; i < test_count; i++) {
            str = br.readLine();
            if (str.charAt(0) == ')' || str.length() % 2 != 0) {
                // 첫시작이 ) 이거나 홀수이면
                check = -1;
            } else {
                check = 1;      // yes or no check 첫 단어가 (로 시작했으니 1부터시작
                for (int j = 1; j < str.length(); j++) {
                     // ( 이면 체크 ++ )이면 체크 --
                    if (check >= 0) {
                        if (str.charAt(j) == '(') {
                            check++;
                        } else if (str.charAt(j) == ')') {
                            check--;
                        }
                    } else {
                        break;
                    }
                }

            }
            if (check == 0) {
                sb.append("YES").append("\n");
            } else {
                sb.append("NO").append("\n");
            }
        }

        // then
        System.out.println(sb);
        br.close();
    }
}


```
