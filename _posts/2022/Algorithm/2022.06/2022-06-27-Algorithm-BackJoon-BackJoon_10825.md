---
published: true
title: BackJoon Algorithm 10825 국영수 (Java)
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
last_modified_at: '2022-06-27 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10825.png)


## 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Back_10825 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int student_count = Integer.parseInt(br.readLine());  // 테스트 카운트 입력
        Student student[] = new Student[student_count];  // 학생 객체 생성
        StringTokenizer token;
        // when
        for (int i = 0; i < student_count; i++) {
            token = new StringTokenizer(br.readLine() + " ");
            String name = token.nextToken();
            int kor = Integer.parseInt(token.nextToken());
            int eng = Integer.parseInt(token.nextToken());
            int math = Integer.parseInt(token.nextToken());

            student[i] = new Student(name, kor, eng, math); // student 객체 배열에 담기
        }
        Arrays.sort(student, (s1, s2) -> {
            // 국어 점수가 같으면
            if (s1.kor == s2.kor) {
                // 영어점수도 같으면
                if (s1.eng == s2.eng) {
                    // 모든 점수가 같으면
                    if (s1.math == s2.math) {
                        return s1.name.compareTo(s2.name);  // 이름 비교 내림
                    }
                    // 수학점수가 증가하는 순으로 오름
                    return s2.math - s1.math;
                }
                // 영어 점수가 증가하는 순으로 내림
                return s1.eng - s2.eng;
            }
            // 국어점수가 감소한는 순으로 오름
            return s2.kor - s1.kor;
        });
        StringBuilder sb = new StringBuilder();
        // then
        for (int i = 0; i < student_count; i++) {
            sb.append(student[i].name).append("\n");
        }
        System.out.println(sb);
        br.close();
    }

    static class Student {

        String name;
        int kor;
        int eng;
        int math;

        public Student(String name, int kor, int eng, int math) {

            this.name = name;
            this.kor = kor;
            this.eng = eng;
            this.math = math;
        }


    }
}


```



