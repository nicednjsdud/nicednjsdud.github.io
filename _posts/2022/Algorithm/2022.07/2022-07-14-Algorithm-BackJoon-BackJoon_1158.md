---
published: true
title: BackJoon Algorithm 1158 요세푸스 순열 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 요세푸스 순열
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1158.png)

## 풀이

- 요세푸스 순열이 뭐지? 하고 검색해봤다.

```
    7 , 3 이라고 하면

    (첫번째)    1 , 2 , 3(제거), 4 , 5 , 6 , 7

    (두번째)    4 , 5 , 6(제거), 7 , 1 , 2  (앞에 1,2를 뒤로 다시 넣기)

    (세번째)    7 , 1 , 2(제거), 4 , 5      (앞에 4,5를 뒤로 다시 넣기)

    (네번째)    4 , 5 , 7(제거), 1          (앞에 7,1를 뒤로 다시 넣기)

    (다섯번째)   1 , 4 , 5(제거)             (앞에 4,5를 뒤로 다시 넣기)

    (여섯번째)   1 , 4 , 1(제거)             (1 , 4 두개뿐이라 다시 1를 집어넣음)

    (일곱번째)   4 , 4 , 4(제거)             (4 한개뿐이라 4를 세번 집어넣음)

    < 3, 6, 2, 7, 5, 1, 4>
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Back_1158 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(token.nextToken());        // 사람수
        int K = Integer.parseInt(token.nextToken());        // 제거 될 순서
        sb.append("<");
        Queue<Integer> qu = new LinkedList<>();
        for(int i=0;i<N;i++){
            qu.add(i+1);
        }
        // when
        while(!qu.isEmpty()){           // 큐에 사람이 모두 빌때까지
            for(int j=0;j<K;j++){
                if(j==K-1){
                        sb.append(qu.poll() + ", ");   // k번째 제거

                }
                else{
                    qu.add(qu.poll());  // k번째가 아닐경우 맨뒤로 다시 넣어주기
                }
            }
        }
        // then
        br.close();
        System.out.println(sb.substring(0,sb.length()-2)+">");
    }
}
```
