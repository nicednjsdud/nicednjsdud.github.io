---
published: true
title: BackJoon Algorithm 11655 ROT13 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: ROT13
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-11 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11655.png)

## 풀이

- 아스키 코드 숫자를 이용해 문제를 푼다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_11655 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String S = br.readLine();
        StringBuilder sb = new StringBuilder();
        // when
        for(int i=0;i<S.length();i++) {
            int password = S.charAt(i);

            if(password>=65 && password<=90){
                password+=13;           // 대문자 구별
                if(password>90){        // 대문자 Z (90) 보다 크다면
                    int shift = password-91;
                    password = 65 + shift;  // 다시 65부터 돌리기
                }
            }
            else if(password>=97 && password <= 122){
                password+=13;           // 소문자 구별
                if(password>122){       // 소문자 z (122)보다 크다면
                    int shift = password - 123;
                    password = 97 + shift;  // 97부터 다시 돌리기
                }
            }
            sb.append((char)password);
        }
        // then
        br.close();
        System.out.println(sb);
    }
}



```
