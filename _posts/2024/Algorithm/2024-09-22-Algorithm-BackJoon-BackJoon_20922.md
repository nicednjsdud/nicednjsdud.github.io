---
published: true
title: BackJoon 소수의 연속합 1644 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 소수의 연속합 1644
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2024-09-20 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1644.png)

## 풀이

..

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;

public class Back_1644 {

    static int n;  // 입력 값 n
    static boolean[] isPrime;  // 소수 여부를 저장하는 배열
    static List<Integer> list;  // 소수 리스트를 저장하는 리스트

    public static void main(String[] args) throws IOException {
        // 입력을 받기 위한 BufferedReader 객체 생성
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());  // n값 입력 받기

        makePrime();  // n 이하의 소수를 구하는 메서드 호출

        // 소수들을 담을 리스트 생성
        list = new ArrayList<>();

        // 2부터 n까지 소수인 숫자만 리스트에 추가
        for(int i = 2; i <= n; i++){
            if(!isPrime[i]) list.add(i);  // isPrime[i]가 false면 소수이므로 리스트에 추가
        }

        int count = 0;  // n을 소수의 연속된 합으로 나타낼 수 있는 경우의 수를 저장할 변수

        // 투 포인터 방식으로 소수의 연속된 합을 구함
        for(int st = 0; st < list.size(); st++){  // 시작 포인터 st
            int sum = 0;  // 연속된 소수의 합을 저장할 변수
            int en = st;  // 끝 포인터 en을 st와 동일한 위치에서 시작

            // 연속된 소수들의 합이 n보다 작을 때까지 en을 증가시킴
            while(en < list.size() && sum < n){
                sum += list.get(en);  // 현재 소수를 sum에 더함
                en++;  // 끝 포인터를 한 칸 이동
            }

            // 만약 sum이 n과 같으면 count 증가
            if(sum == n) count++;
        }

        // n을 연속된 소수의 합으로 나타낼 수 있는 경우의 수 출력
        System.out.println(count);
    }

    // 에라토스테네스의 체 알고리즘으로 n 이하의 소수를 구하는 메서드
    static void makePrime() {
        isPrime = new boolean[n+1];  // 소수 여부를 저장할 배열. 인덱스는 0부터 n까지.
        isPrime[0] = isPrime[1] = true;  // 0과 1은 소수가 아니므로 true로 설정

        // 2부터 √n까지의 수들에 대해 소수 여부를 판별
        for (int i = 2; i * i <= n; i++) {
            if (isPrime[i]) continue;  // 이미 소수가 아니라고 판명된 수는 건너뜀

            // i의 배수들을 모두 소수에서 제외 (true로 설정)
            for (int j = i * i; j <= n; j += i) {
                isPrime[j] = true;  // j는 소수가 아님을 표시
            }
        }
    }
}


```
