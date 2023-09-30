---
published: true
title: BackJoon Algorithm 단어 퍼즐 9946 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 1654 랜선 자르기
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2023-09-30 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9946.png)

## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Back_9946 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int count = 1;
        while (true) {
            String complete_word = br.readLine();
            String collect_word = br.readLine();
            if (collect_word.equals("END") && complete_word.equals("END")) {
                break;
            }
            if(complete_word.length() == collect_word.length()){
                char comp_arr[] = new char[complete_word.length()];
                char col_arr[] = new char[collect_word.length()];
                for(int i = 0;i<complete_word.length();i++){
                    comp_arr[i] = complete_word.charAt(i);
                    col_arr[i] = collect_word.charAt(i);
                }
                Arrays.sort(comp_arr);
                Arrays.sort(col_arr);
                boolean check = true;
                for(int i = 0;i<complete_word.length();i++){
                    if(col_arr[i] != comp_arr[i]){
                        check = false;
                        break;
                    }
                }
                if(check){
                    sb.append("Case "+ count +": same");
                }
                else{
                    sb.append("Case "+ count +": different");
                }
            }
            else{
                sb.append("Case "+ count +": different");
            }
            count++;
            sb.append("\n");
        }
        System.out.println(sb);
        br.close();
    }
}

```
