---
published: true
title: BackJoon Algorithm 1316 그룹 단어 체커 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 그룹 단어 체커
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

![alt](/assets/images/post/Algorithm/1316.png)

## 풀이

- String result에 입력받은 문자중 뒤에 나온문자가 같으면 result에 담지않는다.
- 중복제거를 담은 result문을 이중 for문으로 중복이 있는지 체크한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1316 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int test_count = Integer.parseInt(br.readLine());
        int count = 0;
        // when
        for (int i = 0; i < test_count; i++) {
            String group_word = br.readLine();
            String result = "";
            for (int j = 0; j < group_word.length(); j++) {

                // 연속된 문자열 중복 제거
                if (j != group_word.length() - 1) {
                    if (group_word.charAt(j) == group_word.charAt(j + 1)) {
                        continue;
                    } else {
                        result += String.valueOf(group_word.charAt(j));
                    }
                } else {
                    result += String.valueOf(group_word.charAt(j));
                }
            }
            int result_count = 0;
            for (int j = 0; j < result.length(); j++) {
                for (int k = j + 1; k < result.length(); k++) {

                    // 중복 제거후 똑같은 문자가 있다면
                    if (result.charAt(j) == result.charAt(k)) {
                        result_count--;
                        break;
                    }
                }

            }
            if (result_count == 0) {
                count++;
            }
        }
        // then
        System.out.println(count);
        br.close();
    }
}


```
