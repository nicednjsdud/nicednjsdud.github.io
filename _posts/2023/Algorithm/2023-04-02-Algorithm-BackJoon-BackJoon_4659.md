---
published: true
title: BackJoon Algorithm 4659 비밀번호 발음하기 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 7287 등록
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-02 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4659.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_4659 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        boolean endFlag = false;
        while (!endFlag) {
            String password = br.readLine();
            if (password.equals("end")) {
                endFlag = true;
            } else {
                boolean checkFlag = false;
                boolean vowelFlag = false;      // 모음 체크
                int vowelCount = 0;             // 자음 카운트
                int consonantCount = 0;         // 모음 갯수
                if (password.charAt(0) == 'a' || password.charAt(0) == 'e' || password.charAt(0) == 'i' || password.charAt(0) == 'o' || password.charAt(0) == 'u') {
                    vowelFlag = true;
                    vowelCount++;
                } else {
                    consonantCount++;
                }
                for (int i = 1; i < password.length(); i++) {

                    if (password.charAt(i) == password.charAt(i - 1)) {
                        if (password.charAt(i) == 'e' || password.charAt(i) == 'o') {
                            continue;
                        } else {
                            checkFlag = true;   // ee , oo 허용
                        }
                    }
                    if (password.charAt(i) == 'a' || password.charAt(i) == 'e' ||
                     password.charAt(i) == 'i' || password.charAt(i) == 'o' ||      password.charAt(i) == 'u') {
                        vowelFlag = true;
                        consonantCount = 0;
                        vowelCount++;
                    } else {
                        consonantCount++;
                        vowelCount = 0;
                    }
                    if (vowelCount == 3 || consonantCount == 3) {
                        checkFlag = true;   // 자음 모음 연속 3개이상
                    }
                }
                if (checkFlag == true || vowelFlag == false) {
                    sb.append("<" + password + "> is not acceptable.").append("\n");
                } else {
                    sb.append("<" + password + "> is acceptable.").append("\n");
                }
            }
        }
        System.out.println(sb);
        br.close();
    }
}


```
