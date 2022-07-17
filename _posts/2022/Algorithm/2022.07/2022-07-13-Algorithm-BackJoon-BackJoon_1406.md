---
published: true
title: BackJoon Algorithm 1406 에디터 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: 에디터
tag: BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: "2022-07-13 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# BackJoon Algorithm - Java

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/11656.png)

## 풀이

- list에 담아 일반적으로 풀어봤다. 하지만 **시간초과**

```java
import java.io.*;
import java.util.LinkedList;

public class Back_1406 {
    public static void main(String[] args) throws IOException {
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String str = br.readLine();      // 문자열 입력
        int count = Integer.parseInt(br.readLine());    // 입력할 명령어의 개수
        LinkedList<Character> list = new LinkedList<>();


        for(int i=0;i<str.length();i++){
            list.add(str.charAt(i));
             // 리스트에 문자 하나씩 추가
        }
        int cursor = list.size();                // 커서 위치
        // when
        for (int i = 0; i < count; i++) {
            String command = br.readLine();
            char c = command.charAt(0);
            switch (c) {
                case 'L':
                    if (cursor != 0) {
                        cursor--;       // 명령어 L
                    }
                    break;
                case 'D':
                    if(cursor!=list.size()) {
                        cursor++;       // 명령어 D
                    }
                    break;
                case 'B':
                    if(cursor!=0) {
                        list.remove(cursor-1);
                        cursor--;   // 명령어 B
                    }
                    break;
                case 'P':
                    char ch = command.charAt(2);
                    list.add(cursor,ch);
                    cursor++;       // 명령어 P
                    break;
            }
        }
        // then
        br.close();
        for (Character character : list) {
            bw.write(character);
        }
        bw.flush();
        bw.close();
    }
}

```

- 계속 시간초과가 나오길래 구글 크롤링을 해봤다.

크롤링한 결과 결국 시간복잡도 차이였다. 그 인덱스에 바로 접근하는 것이 아니라 head와 tail을  
제외하곤 하나하나 살펴보며 찾아가서 처리하기 때문에 완전히 효율적이지 않다.

```
    그래서 시간 초과가 난거 같다.
```

O(N)의 시간 복잡도를 가지게 되었고 커서 기준 거리 1이내로 연산이 행해져야 하는 문제이기 때문에  
모든 연산이 O(1)이여야 한다.

## ListIterator의 사용

- Iterator를 상속하는 인터페이스이다.
- 양방향 탐색이 가능하다.
- 커서를 왔다갔다 하는 문제여서 굉장히 효율적이다.

```java
import java.io.*;
import java.util.LinkedList;
import java.util.ListIterator;

public class Back_1406 {
    public static void main(String[] args) throws IOException {
        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String str = br.readLine();             // 문자열 입력
        int count = Integer.parseInt(br.readLine());    // 입력할 명령어의 개수
        LinkedList<Character> list = new LinkedList<>();


        for (int i = 0; i < str.length(); i++) {
            list.add(str.charAt(i));                   // 리스트에 문자 하나씩 추가
        }
        ListIterator<Character> iter = list.listIterator();

        while (iter.hasNext()) {
            iter.next();        // 처음 커서는 맨뒤에 위치해줌
        }
        // when
        for (int i = 0; i < count; i++) {
            String command = br.readLine();
            char c = command.charAt(0);
            switch (c) {
                case 'L':
                    if (iter.hasPrevious()) {
                        iter.previous();       // 명령어 L
                    }
                    break;
                case 'D':
                    if (iter.hasNext()) {
                        iter.next();       // 명령어 D
                    }
                    break;
                case 'B':
                    if (iter.hasPrevious()) {
                        iter.previous();
                        iter.remove();   // 명령어 B
                    }
                    break;
                case 'P':
                    char ch = command.charAt(2);
                    iter.add(ch);// 명령어 P
                    break;
            }
        }
        // then
        br.close();
        for (Character character : list) {
            bw.write(character);
        }
        bw.flush();
        bw.close();
    }
}
```
