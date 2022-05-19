---
title: CS50 3-3강 변수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 변수
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs, 시간
last_modified_at: '2022-05-12 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)

변수
====

## 변수 (Variable)

* 변수는 값을 담아둘 수 있는 저장 공간으로 프로그램 수행에 따라  
  값이 수정되거나 변경될 수 있다.
* 컴퓨터 프로그램은 나중에 코드에서 사용할 수 있는 중요한 정보를  
  기억하기 위해 변수를 사용

## 변수를 선언하여 사용하기

![alt](/assets/images/post/computer science/CS50/1/28.png)

* C에서 변수를 사용하는 첫번째 단계는 변수 사용을 원한다는 것을  
  프로그램이 알 수 있도록 하는 것이다. 이단계를 변수선언(declaration)  
  이라고 부른다.
* C에서, 변수 선언을 해주기 위해서는 변수의 자료형을 알려준 후   
  변수의 이름을 명시해준다.
* 한번 변수를 선언하면, 다양한 방법으로 다룰 수 있다. 2행을 보면  
  변수 count에 2라는 값을 할당했다. 이제 숫자 2가 변수 count안에  
  저장된 것이다. 선택적으로 1행과 2행을 하나의문장으로 합칠 수 있는데  
  변수를 선언하는 동시에 값을 지정하도록 int count =2;라고 작성한다.
* 변수에 값을 넣어준 다음에도 값을 바꿀수 있다. 3행은 count의 값을  
  8로 바꿔준다. 이제 count는 이전에 저장한 값인 2를 잊고 8을기억한다.
* 변수에 들어있는 값은 이름만으로도 접근할 수 있다. (4행)

![alt](/assets/images/post/computer science/CS50/1/29.png)

## 사용자 입력을 받는 변수

```c
#include<stdio.h>

int main(void){
    int i;
    scanf("%d",&i);
    printf("i is %d",i)
}
```

* 다양한 상황에서, 프로그램은 사용자로부터 입력값을 받아오고 변수에  
  저장하는것이 필요하다. 입력값을 받기위해 일반적으로 사용하는 함수는  
  scanf 이다.
* 6행에서 scanf("%d",&i);를 통하여 사용자가 입력하는 정수를 i가   
  저장된 주소에 저장할 수 있다. %d는 정수값을 담아두는 플레이스홀더  
  이며, &i는 i라는 변수의 주소라는 뜻이다.
* 7행에서 변수의 값을 화면에 보여준다. prinf다음에 오는 괄호 안에  
  "i는 %d"라는 문자열과 %d를 대체할 정수 i를 입력해준다.

![alt](/assets/images/post/computer science/CS50/1/30.png)

## 생각해보기

1. 변수는 왜 필요한가요? 변수를 사용할 수 없다면, 프로그램에는 어떤일  
   들이 벌어질까요?

```
    변수는 중요한 수를 기억하기위해 선언하는 것이다. 변수를 사용할 수 
    없다면 상수만 이용하여 프로그램을 짜야하는데 굉장히 유지보수등 
    비효율적이다.
```

2. 만약 변수에 접근할 수 없다면, 두개의 숫자를 프로그램은 어떻게 작성  
  할 수 있나요?

```
    상수로 접근을 해야한다.
```

## 실습 코드 등록

```c++
#include <stdio.h> //printf 함수가 포함된 라이브러리입니다.

int main() 
{
  //이 아래부터 코드를 작성합니다.
  //int형 변수를 선언합니다.
  int number;
  //변수에 100을 저장합니다.
  number = 100;
  //변수를 출력합니다.
   printf("%d",number);
  
  return 0; //main 함수를 종료합니다.
}
```

### 실행결과

![alt](/assets/images/post/computer science/CS50/1/31.png)
