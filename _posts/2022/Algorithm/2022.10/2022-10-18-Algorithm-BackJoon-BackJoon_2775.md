---
published: true
title: BackJoon Algorithm 2775 부녀회장이 될테야 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 부녀회장이 될테야
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-18 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2775.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_2775 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int test_count = Integer.parseInt(br.readLine());
        // when
        for (int i = 0; i < test_count; i++) {
            int floor = Integer.parseInt(br.readLine());
            int room = Integer.parseInt(br.readLine());
            int count = 0;
            int apt[][] = new int[floor + 1][room + 2];
            int people_count = 1;
            // 0층 담아주기
            for (int k = 1; k <= room; k++) {
                apt[0][k] = people_count;
                people_count++;
            }
            if (floor != 0) {
                for (int j = 1; j <= floor; j++) {
                    people_count = 1;
                    for (int k = 1; k <= room; k++) {
                        apt[j][k] = people_count;
                        people_count = apt[j - 1][k + 1] + people_count;
                    }
                }
            }
            System.out.println(apt[floor][room]);
        }
        // then
        br.close();
    }
}



```
