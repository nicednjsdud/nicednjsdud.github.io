---
title: (자료구조) 3-2 포인터
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 배열
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2022-11-15 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 포인터

.

## 1. 포인터

### 1) 정의

- **변수의 메모리 주소값**
- **포인터 변수**
- 주소값을 저장하는 특별한 변수
- 변수가 어떤 변수의 주소를 저장하고 있다는 것은 포인터 변수가 그 변수를 가리키고 있다.  
  (포인트하고 있다.)는 의미

### 2) 포인터 변수

- 포인터 변수를 이용하여 연결된 주소의 변수 영역을 액세스 함
- 포인터 변수를 간단히 포인터라고 함

#### (1) 의미

- 편지봉투에 받는 사람의 집주소를 쓰면, 그주소로 편지가 전달되어 집주인이 편지를 받게 된다.
- 편지봉투 : 포인터 변수
- 편지봉투에 쓰는 받는 사람 주소 : 포인터 변수에 저장된 변수의 메모리 주소
- 주소에 해당하는 집주인이 편지를 받는 것 : 포인터 변수를 통한 변수의 엑세스

![alt](/assets/images/post/ComputerStudy/44.png)

#### (2) 예

```c
  int i;  ........ // (1)
  int *prt = &i; ....// (2)
```

- (1)에서 변수 i를 선언했을 때에 저장된 메모리 번지를 150번지라고 한다면,
- (2)에서 변수 i의 주소를 포인터 변수 ptr에 저장하면 ptr에는 메모리 주소 150이 저장되므로,  
  포인터 변수 ptr은 150번지의 변수 i를 가리키는 상태가 됨.

![alt](/assets/images/post/ComputerStudy/45.png)

### 3) 포인터 변수 선언

- 포인터 선언 형식

```c
  자료형 *포인터 변수이름
  ---   -----------
  (1)       (2)
```

#### (1) 자료형

- 포인터 변수 자체의 자료형이 아니라, 포인터 변수에 저장할 주소에 있는 일반 변수의 자료형

#### (2) 포인터 변수 이름

- 일반 변수이름과 구별하여 변수이름 앞에 `'*'`를 표시하여 포인터 변수임을 표시

#### (3) 포인터 변수의 자료형에 따른 메모리 액세스 범위

```c
  char *ptr;    // (1) 1byte
  short *ptr;   // (2) 2byte
  int *ptr;     // (3) 4byte
```

![alt](/assets/images/post/ComputerStudy/46.png)

### 4) 포인터 연산 - &

- 주소 연산자 : &
- 변수의 주소를 구하기 위하여 사용
- 변수 앞에 &를 사용하여 그 변수의 주소를 사용
- 사용할 주소 영역의 변수와 포인터 변수는 같은 자료형으로 선언

```c
  포인터 변수 = &변수;
```

#### (1) 주소 연산자 사용 예

```c
    int i = 10;
    int *ptr;
```

![alt](/assets/images/post/ComputerStudy/47.png)

```c
  ptr = &i;
```

![alt](/assets/images/post/ComputerStudy/48.png)

### 5) 포인터 연산 - `*`

- 참조 연산자 : `*`
- 저장된 주소에 있는 값(변수에 저장된 값)을 액세스하는 연산자

#### (1) 사용 방법 1

- 지정한 값을 포인터가 가리키고 있는 주소에 저장

```c
  * 포인터 변수 = &변수;
```

#### (2) 사용 방법 2

- 포인터가 가리키는 주소에 있는 값을 변수에 저장

```c
  변수 = *포인터 변수;
```

#### (3) 사용 예

```c
  int i,j;
  int *ptr;

  ptr = &i;   // (1)
  *ptr = 10;  // (2)
  j = *ptr;   // (3)
```

![alt](/assets/images/post/ComputerStudy/49.png)

### 6) 포인터의 초기화

- 초기화

```c
  자료형 *포인터 변수 = 초기값 주소;
```

#### (1) 포인터 초기화 방법 1

- 주소 연산자를 사용하여 변수의 주소 지정

```c
  int i;
  int *ptr = &i;
```

#### (2) 포인터 초기화 방법 2

- 동적 메모리를 할당하고 그 시작주소를 포인터 값으로 지정

```c
  char *ptr = (char *) malloc(100);
```

#### (3) 포인터 초기화 방법 3

- 문자형 포인터에 문자열의 시작주소를 지정

```c
  char *ptr = "korea";
```

#### (4) 포인터 초기화 방법 4

- 배열의 이름을 이용하여 배열시작주소를 지정
- 배열 이름은 문자열과 마찬가지로 그 시작주소를 전달할 수 있음

```c
  char A[100];
  char *ptr = A;
```

#### (5) 포인터 초기화 방법 5

- 배열의 첫 번째 요소의 주소를 사용하여 배열 시작 주소를 지정
- 인덱스로 표시하는 배열의 각 요소는 그 이름만으로는 주소를 전달 할 수 없기 때문에  
  주소연산자 &를 사용

```c
  char A[100];
  char *ptr = &A[0];
```

## 2. 문자 배열 vs 포인터 배열

### 1) 포인터와 문자 배열

- 포인터를 사용하여 문자열 연산 처리

```c
  ptr1 = string1;
```

![alt](/assets/images/post/ComputerStudy/50.png)

#### (1) 거꾸로 찍어 보기 예제

```c
  for(i = 16; i >= 0; i--){
    putchar(*(ptr1 + i))
  }
```

![alt](/assets/images/post/ComputerStudy/51.png)

### 2) 포인터 배열

- 포인터 자료형을 배열로 구성
- 여러 개의 포인터를 하나의 배열로 구성한 배열의 특징과 포인터의 특징을 모두 활용 가능
- 포인터 배열이 선언형식

```c
  자료형 * 포인터배열이름[배열크기];
```

- 포인터 배열에서 각 배열요소는 포인터
- 2차원 문자배열을 1차원 포인터배열로 표현
  - 2차원 배열의 행의 개수 : 포인터 배열 크기
  - 포인터 배열의 각 배열요소
    - 각 문자열에 대한 시작주소를 가진 포인터

#### (1) 2차원 배열 예제

```c
  char string[3][10] = {"Dreams","come","true!"};
```

![alt](/assets/images/post/ComputerStudy/52.png)

#### (2) 1차원 포인터 배열

```c
  char *ptr[3] = {% raw %}{{"Dreams"},{"come"},{"true!"}}{% endraw %};
```

![alt](/assets/images/post/ComputerStudy/53.png)

## 3. 포인터의 포인터

### 1) 정의

- 포인터를 가리키는 포인터 **(즉, 이중 포인터)**

### 2) 선언 형식

```c
  자료형 **포인터변수이름

  char **ptr;
```

![alt](/assets/images/post/ComputerStudy/54.png)

### 3) 예제

```c
  char *ptrArray[2];
  char **ptrptr;
```

![alt](/assets/images/post/ComputerStudy/55.png)

```c
  ptrptr = ptrArray;
```

![alt](/assets/images/post/ComputerStudy/56.png)
