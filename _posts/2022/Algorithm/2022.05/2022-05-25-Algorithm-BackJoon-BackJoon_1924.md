---
title: BackJoon Algorithm 1924 2007년 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 2007년
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1924.png)


## 풀이

* 배열로 날짜들과 각 요일을 담는다.
* for문으로 total날짜를 합산하여 7로 나누면 각 요일이 나온다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_1924 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());

        int month = Integer.parseInt(token.nextToken());    // 달입력
        int day = Integer.parseInt(token.nextToken());      // 일입력

        int Days[] = {31,28,31,30,31,30,31,31,30,31,30,31};
        String[] week = {"SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"};
        int total =day;
        for(int i=0;i<month-1;i++){         // 전달까지의 일수 합하기
            total +=Days[i];
        }
        System.out.println(week[total%7]);
    }
}


```
