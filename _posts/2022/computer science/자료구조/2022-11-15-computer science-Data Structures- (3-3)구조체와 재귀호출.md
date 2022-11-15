---
title: (자료구조) 3-3 구조체와 재귀 호출
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 구조체와 재귀 호출
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-11-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 구조체와 재귀호출

## 1. 구조체의 사용

### 1) 구조체

- 배열처럼 여러 개의 데이터를 그룹으로 묶어서 하나의 자료형으로 정의하고 사용하는 자료형
- 배열은 같은 자료형만을 그룹으로 묶을수 있지만, 구조체는 서로 다른 자료형을 그룹으로 묶을 수 있어  
  복잡한 자료형태를 정의하는데 유용

![alt](/assets/images/post/ComputerStudy/57.png)

- file = set of records
- record = multi field;

![alt](/assets/images/post/ComputerStudy/58.png)

### 2) 구조체 선언

- 여러 자료형의 변수들을 그룹으로 묶어서 하나의 자료형으로 선언
- 구조체는 구조체 이름, 자료형, 데이터 항목으로 구성

#### (1) 구조체의 이름

- 구조체로 정의하는 새로운 자료형의 이름

#### (2) 항목

- 구조체를 구성하는 내부 변수들의 이름
- 구조체의 항목은 배열의 각 배열요소에 해당

##### 배열요소

- 모든 같은 자료형으로 되어있으므로 배열요소에 대한 선언 없이 사용
- 구조체에서는 각 항목이 다른 자료형을 가질 수 있기 때문에 항목별로 자료형과 항목이름(변수이름)  
  을 선언해야함.

#### (3) 선언 형식

```c++
  struct 구조체이름 { 자료형 항목 1; 자료형 항목2; ... 자료형 항목n;}
```

- 사용할 구조체의 모양을 정의한 것뿐이므로 사용할 구조체 변수를 다시 선언해야함.

```c
  struct 구조체이름 구조체변수;
```

- 선언된 구조체 변수는 일반변수와 똑같이 취급하고 사용

#### (4) 사용 예 : 직원 관리 프로그램

```c
  struct employee{
            char name[10];
            int year;
            int pay;
  }
```

![alt](/assets/images/post/ComputerStudy/59.png)

##### 구조체 변수 선언

```c
  struct employee Lee,Kim,Park;
```

![alt](/assets/images/post/ComputerStudy/60.png)

## 2. 구조체의 연산

### 1) 구조체의 초기화

- 구조체는 여러 개의 내부 항목으로 구성되어 있으므로 내부 항목의 자료형과 개수, 순서에  
  맞추어 초기값을 지정하되 두개 이상의 값을 나열해야 하므로 중괄호 사용

```c
  struct employee Lee = {"Ann",2005,3200};  // 구조체 변수의 초기화
```

![alt](/assets/images/post/ComputerStudy/61.png)

### 2) 구조체 데이터 항목의 참조

- 구조체 변수에 있는 각 데이터 항목을 참조하기 위해서는 구조체 연산자 사용

#### (1) .(점 연산자)

- 구조체 변수의 데이터 항목을 지정한다.

```c
  struct employee Lee;  // (1)
  Lee.name = "Ann";     // (2)
  Lee.year = 2005;      // (3)
  Lee.pay = 3200;       // (4)
```

![alt](/assets/images/post/ComputerStudy/62.png)

#### (2) ->(화살표 연산자)

- 구조체형 포인터에서 포인터가 가리키는 구조체 변수의 데이터 항목을 지정한다.

```c
  struct employee kim;
  struct employee *Sptr = &kim; // (1)
  Sptr -> name = "susan";       // (2)
  Sptr -> year = 2004;          // (3)
  Sptr -> pay = 3400;           // (4)
```

![alt](/assets/images/post/ComputerStudy/63.png)

### 3) 구조체의 연산

#### (1) 데이터 항목 참조 연산

- 점 연산자와 화살표 연산자를 이용하여 구조체의 데이터 항목을 개별적으로 참조

```c
  struct employee Lee;
         struct employee *Sptr;
         Sptr = &Lee;
         Lee.year = 2005;
         Sptr->pay = 3000;
         Sptr->name = "Ann";
```

#### (2) 구조체 복사 연산

- 같은 구조체에 대한 구조체 변수 간에는 내용을 한번에 복사하는 연산 사용 가능

```c
  struct employee Lee,Kim,team[5];

  Lee = Kim;
  Lee = team[2];
  team[2] = team[3];
```

#### (3) 구조체 변수의 주소 구하기 연산

- 포인터의 주소 연산자를 사용하여 구조체 변수의 주소를 구하거나 구조체 변수가 배열인 경우  
  배열의 특성에 따라 구조체 배열 변수의 이름에서 주소를 구함.

```c
  struct employee Lee,team[5];
  struct employee *Sptr1, *Sptr2;

  Sptr1 = &Lee;
  Sptr2 = team;
```

## 3. 재귀호출

### 1) 의미

- 자기 자신을 호출하여 순환 수행하는 것
- 함수에서 실행하는 작업의 특성상 일반적인 호출 방식보다 재귀호출 방식을 사용하여 함수를 만들면  
  프로그램의 크기를 줄이고 간단하게 작성 가능

### 2) 예 : factorial

- n에 대한 factorial 연산은 1부터 n까지의 모든 자연수를 곱하여 구하는 연산

```c
      n! = n x (n-1)!
  (n-1)! = (n-1) X (n-2)!
  (n-2)! = (n-2) x (n-3)!
          ....
      2! = 2 X 1!
      1! = 1
```

- 마지막에 구한 하위값을 이용하여 상위값을 구하는 작업을 반복 수행
- 재귀호출을 사용하여 함수를 작성

```c
    long int fact(int n){
      if(n<=1) return (1);
      else return (n*fact(n-1));
    }
```

![alt](/assets/images/post/ComputerStudy/64.png)
.
