---
title: CS50 3-2강 문법
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 문법
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-11 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

문법
===

## C언어의 문법

* C 언어는 프로그램을 작성하는 데 사용되는 프로그래밍 언어이다.
* C와 같은 프로그래밍 언어는 굉장히 구체적인 문법(Syntax)을 사용하여 프로그램을  
  작성할 것을 요구합니다.
* 여기서 구체적인 문법이란 완벽한 프로그램으로 동작하는 문장들을 작성하기 위해 필요한  
  단어와 기호들(소괄호,중괄호 등)을 어떻게 배열할 것인지에 대한 규칙이다.

```c
    #include <stdio.h>

    int main(void) 
    {
	printf("hello world\n");
    }
```

### 1행

* 1행에서, #include<stdio.h>는 이프로그램이 stdio.h라는 파일안에 들어 있는  
  미리 작성된 함수들에 접근할 수 있도록 한다.
* 여기에서 함수는 특정기능을 수행하기 위한 문장들을 모아놓은 것을 말한다.
* stdio.h를 포함 함으로써, 프로그램은 다른 사람들이 이전에 미리 작성해 둔 함수에  
  접근할 수 있다.
* 이로인해 화면에 문자를 보여주는 역할을 하는 printf라는 함수를 가져다 사용할 수 있다.

### 3행

* 3행의 in main(void)는 스크래치 엔트리에서 "초록 깃발을 클릭했을 때" 혹은  
  "시작하기 버튼을 클릭했을 때"의 기능과 같은 기능으로, 프로그램의 시작점을 정의한다.

### 4행~6행

* 4행~6행 중괄호는 main 함수의 코드를 묶어주는 역할을 한다. 중괄호 안의 내용이 어더한 것이든  
  main함수의 한 부분이 된다.

![alt](/assets/images/post/computer science/CS50/1/27.png)

## 컴파일하여 프로그램 실행하기

* C프로그램을 작성한 후, .c로 끝나는 파일로 소스코드를 저장해야 한다. 여기에서는 hello.c라는  
  이름의 파일로 저장한다.
* 컴퓨터는 0과 1만 이해하기 때문에, 우리는 소스코드를 0과 1로 만드는 작업인 컴파일을 해야한다.

* 컴파일이란, 소스코드를 일련의 0과 1들로 이루어진 오브젝트 코드(object code)로 전환해주는 것이다.  
  소스코드가 오브젝트로 코드로 변환되면, 컴퓨터가 이해하고 실행가능한 0과1의 형태로 만들어진다.
* 문장 중 //이나 /* 와*/ 안에 작성되어있는 코드는 컴파일러에 의해 완전히 무시된다. 이것을 주석  
  이라고 부른다. 이주석은 프로그래머들이 코드에 대한 설명을 기록함으로써 나중에 보는 사람들이  
  쉽게 이해할 수 있도록 하는데 자주 사용된다.
* 만약 clang 컴파일러를 사용한다면, make hello 명령어를 입력함으로써 프로그램을 컴파일 할수 있다.  
  만약 에러 없이 성공적으로 컴파일 되면, 우리는 ./hello 라고 명령어를 입력하여 프로그램을 실행  
  할 수 있다. 만약 프로그램이 제대로 작동한다면 화면에 Hello,world라고 출력될 것이다.

## 생각해보기

```c
int main(void){
    printf(hello world\n)
}
```

1. 위 코드에는 오류가 몇개나 있을까요. 오류를 찾아내어 올바른 코드로 작성해 봅시다.

```c
#include<stdio.h>
int main(void){
    prinf("hello world\n")
}
```
