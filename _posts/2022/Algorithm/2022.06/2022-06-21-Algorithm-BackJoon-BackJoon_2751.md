---
published: true
title: BackJoon Algorithm 2751 수 정렬하기2 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 수 정렬하기2
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-21 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2751.png)


## 풀이

* 일반적인 Arrays.sort()를 사용하면 시간초과가 나온다.
* 구글링해본 결과.. Collections.sort를 사용하면 된다고 한다.
    * Collection.sort()에 대해 공부 <<

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;

// Collections.sort
public class Back_2751 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());

        ArrayList<Integer> list = new ArrayList<>();

        for(int i=0;i<N;i++){
            list.add(Integer.valueOf(br.readLine()));
        }
        // when
        Collections.sort(list);     // collections 오름차순 정렬

        // then
        for(Integer i : list){
            sb.append(i);
            sb.append("\n");
        }
        System.out.println(sb);
        br.close();
    }
}
```



