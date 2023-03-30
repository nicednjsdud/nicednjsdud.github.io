---
published: true
title: BackJoon Algorithm 삼각형과 세 변 5073 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 삼각형과 세 변 5073
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-03-26 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5073.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_5037 {
    public static void main(String[] args) throws IOException {


        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        boolean checkFlag = true;
        StringBuilder sb = new StringBuilder();
        while (checkFlag) {
           st = new StringTokenizer(br.readLine(), " ");

           int first_num = Integer.parseInt(st.nextToken());
           int second_num = Integer.parseInt(st.nextToken());
           int third_num = Integer.parseInt(st.nextToken());
           int max = Math.max(first_num,(Math.max(second_num,third_num)));
            if(first_num == 0 && second_num == 0 && third_num == 0){
                checkFlag = false;
            }
            else{
                if(max < (first_num + second_num + third_num - max)){
                    if(first_num == second_num){
                        if(second_num == third_num){
                            sb.append("Equilateral").append("\n");
                        }
                        else{
                            sb.append("Isosceles").append("\n");
                        }
                    }
                    else{
                        if(second_num == third_num){
                            sb.append("Isosceles").append("\n");
                        }
                        else if(first_num == third_num){
                            sb.append("Isosceles").append("\n");
                        }
                        else{
                            sb.append("Scalene").append("\n");
                        }
                    }
                }
                else{
                    sb.append("Invalid").append("\n");
                }
            }

        }
        System.out.println(sb);
        br.close();
    }
}



```
