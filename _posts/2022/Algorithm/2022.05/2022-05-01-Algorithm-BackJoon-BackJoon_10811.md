---
title: BackJoon Algorithm 10811 바구니 뒤집기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 바구니 뒤집기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-01 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10811.png)



## 풀이

* 역순 구하는 알고리즘을 구현한다.
* BufferReader 메서드를 활용

![alt](/assets/images/post/Algorithm/10811_1.png)
 
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10811 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(token.nextToken());  // 바구니 개수 입력
        int M = Integer.parseInt(token.nextToken());  // 역순 만들 횟수
        int arr[] = new int[N];                       // 바구니 배열
        int K=1;                                       // 바구니
        // when
        for(int i=0;i<N;i++){
            arr[i]=K;
            K++;                                     // 바구니 담기
        }

        for(int k=0;k<M;k++) {
            token = new StringTokenizer(br.readLine());
            int i = Integer.parseInt(token.nextToken());// i번째 바구니부터
            int j = Integer.parseInt(token.nextToken());// j번쨰 바구니까지
            for (int m = i - 1; m < j; m++) {
                int temp = 0;
                if (m == j - 1) {                       // j-i가 짝수일때
                    break;
                }
                if (j - m == 1) {                       // j-i가 홀수일때
                    break;
                }
                temp = arr[m];
                arr[m] = arr[j-1];
                arr[j - 1] = temp;           // 역순으로 끝에서부터 바꾸기
                j--;
            }

        }
        // then
        for(int i=0;i<N;i++){
            System.out.print(arr[i]+" ");
        }
        br.close();
    }

}


```


