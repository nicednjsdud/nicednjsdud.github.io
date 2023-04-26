---
published: true
title: BackJoon Algorithm 1822 차집합 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 10816 숫자 카드2
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-04-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1822.png)

## 풀이

1. 기본적인 이분탐색으로 풀어봤다 - 시간초과
2. HashSet을 이용하여 remove()를 사용해 중복을 제거했다 - 실패(?)
3. 구글을 찾아보니 HashSet을 쓰면 실패로떠서 TreeSet으로 푸신분을 보고 풀었다 - 성공
   - HashSet을 쓰면 왜 실패로 뜨는지 찾아봐야겠다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashSet;
import java.util.StringTokenizer;
import java.util.TreeSet;

public class Back_1822 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();

        int A = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());

        TreeSet<Integer> Aset = new TreeSet<>();

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < A; i++) {
            Aset.add(Integer.parseInt(st.nextToken()));
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i< B; i++){
            Aset.remove(Integer.parseInt(st.nextToken()));
        }
        if(Aset.size() == 0){
            System.out.println(0);
        }
        else{
            System.out.println(Aset.size());
            for (Integer integer : Aset) {
                System.out.print(integer + " ");
            }
        }
        br.close();

    }
}



```
