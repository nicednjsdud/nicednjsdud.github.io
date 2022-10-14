---
published: true
title: BackJoon Algorithm 4344 평균은 넘겠지 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: OX퀴즈
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-10-14 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4344.png)

## 풀이

- DecimalFormat 함수를 사용하였다.
- "#0.000"은 일의자리수가 0이면 점뒤에 0 3개를 붙이는것이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.text.DecimalFormat;
import java.util.StringTokenizer;

public class Back_4344 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        DecimalFormat df = new DecimalFormat("#0.000");
        StringTokenizer st;
        int students = Integer.parseInt(br.readLine());

        for (int i = 0; i < students; i++){
            st = new StringTokenizer(br.readLine());
            int student_count = Integer.parseInt(st.nextToken());
            int scores[] = new int[student_count];
            int sum = 0;
            // when
            for(int j=0;j<student_count;j++){

                int score = Integer.parseInt(st.nextToken());
                scores[j] = score;
                sum += score;
            }
            int pass_count = 0;
            double avg = (double)(sum/student_count);
            for(int j=0;j<scores.length;j++){
                if(scores[j] > avg){
                    pass_count++;
                }
            }

            double d_sum = Math.round((double)pass_count/(double)student_count*100000) /1000.0;

            sb.append(df.format(d_sum)).append("%").append("\n");
        }
        // then
        System.out.println(sb);
        br.close();
    }
}


```
