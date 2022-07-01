---
published: true
title: BackJoon Algorithm 11652 카드 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 쉬운 계단 수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-28 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11652.png)


## 풀이

* 오름차순 정렬로 똑같은 수들을 모은 후 for문을 돌리면서 갯수를 센다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_11652 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int Test_count = Integer.parseInt(br.readLine());// 테스트 개수 입력
        long arr[] = new long[Test_count];
        for (int i = 0; i < Test_count; i++) {
            arr[i] = Long.parseLong(br.readLine());   // 배열 입력
        }
        // when
        Arrays.sort(arr);                            // 오름차순 정렬


        int max = 1;                            // 출력할 수의 최대 카운트
        int num=0;                             // 출력할 수
        int count = 1;
        for(int i=1;i<Test_count;i++){
            if(arr[i]==arr[i-1]){   // 만약 전의 수가 같으면 count ++
                count++;
            }
            else {
                count = 1;          // 아니면 count = 1 (초기화)
            }

            if(count>max){
                max=count;
                num=i;
            }
        }
        // then
        System.out.println(arr[num]);       // arr[num] 번째의 값 출력
        br.close();

    }
}

```



