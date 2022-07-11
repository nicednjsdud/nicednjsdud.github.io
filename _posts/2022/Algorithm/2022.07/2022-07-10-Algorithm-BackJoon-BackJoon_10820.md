---
published: true
title: BackJoon Algorithm 10820 문자열 분석 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 문자열 분석
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-10 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10820.png)

## 풀이

- 아스키 코드 숫자를 이용해 문제를 푼다.
- 알파벳 배열을 만들고 (26칸) 소문자는 -97을 해주면 0부터 26까지 나온다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10809 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        int Alphabet[] = new int[26];
        for (int i = 0; i < Alphabet.length; i++) {
            Alphabet[i] = -1;                     // 먼저 알파벳 배열에 모두 -1 주입
        }
        // when
        for (int i = 0; i < str.length(); i++) {
            int Alphabet_count = str.charAt(i) - 97;
            if (Alphabet[Alphabet_count] != -1) {   // 먼저 들어간 알파벳이 있다면 건너뛰기
                continue;
            } else {
                Alphabet[Alphabet_count] = i;
            }
        }
        // then
        for (int i : Alphabet) {
            System.out.print(i+" ");
        }
        br.close();
    }
}





```
