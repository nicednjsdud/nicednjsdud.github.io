---
published: true
title: BackJoon Algorithm 백설 공주와 일곱 난쟁이 3040 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 백설 공주와 일곱 난쟁이
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-11-24 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/3040.png)

## 풀이

- 9개의 입력의 합을 100으로 뺀다 // 가짜 2명의 합
- 이중 for문으로 두개의 합이 같은것을 -1로 바꿔준뒤 출력할 때 빼준다.

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_3040 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int capNum[] = new int[9];
        int sum = 0;
        int two_fake_sum = 0;
        for (int i = 0; i < capNum.length; i++) {
            capNum[i] = Integer.parseInt(br.readLine());
            sum += capNum[i];
        }
        two_fake_sum = sum - 100;       // 가짜 두명의 합
        // when
        for (int i = 0; i < capNum.length; i++) {
            for (int j = i + 1; j < capNum.length; j++) {

                if (capNum[i] >= two_fake_sum || capNum[j] >= two_fake_sum) {
                    continue;
                } else {
                    if (capNum[i] + capNum[j] == two_fake_sum) {
                        capNum[i] = -1;
                        capNum[j] = -1;
                        break;
                    }
                }
            }
        }
        // then
        for (int i : capNum) {
            if (i == -1) continue;
            System.out.println(i);
        }
        br.close();
    }
}


```
