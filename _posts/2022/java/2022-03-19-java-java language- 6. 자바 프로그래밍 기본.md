---
title: Java 3.Variable
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is Java
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language
last_modified_at: '2022-03-19 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

## 자바기초
    OOP 입문
    OOP 핵심
    자바의 유용한 클래스들
    자바의 다양한 기능들
    자바 미니 프로그램 만들기

## 1. 자바 개발 환경 구축
### 1. OpenJDK 
### 2. 이클립스

```
    - 괄호 :  ()  소괄호 []  중괄호  {}  대괄호
```

## 2. 자바 예약어
* Keyword

* 자바에서 미리 사용하는 단어

* 지정한 예약어를 클래스명이나 변수명으로 사용불가

## 3. 변수 (variable)

```
    // 떡갈비 를 3개 살려했는데 4개 샀다 (그 수가 어딘가에 저장)
```

* 특정 메모리 영역에 할당한 이름

* 하나의 값을 저장할 수 있는 메모리의 기억공간

* 프로그램에서는 항상 변하는 값을 나타낼 필요가 있음

```
    ex) 학생의 성적, 합계, 게임의 레벨, 회원 주소 ....
```

* 표현하려는 수에 맞는 데이터 타입(자료형)을 이용하여 변수를 선언

* 표현하려는 자료가 숫자, 문자, 문자열을 다양할 수 있으모로 그에 맞는 자료형을 사용

```java
public class VarTest01 {

	public static void main(String[] args) {
		
		int num =10;						//10 진수 (Decimal)
		int bNum = 0B1010;					// 2 진수 (Binary)
		int oNum = 012;						// 8 진수 (Octal)
		int xNum = 0xA;						//16 진수 (Hexadecimal)
		
		System.out.println(num);
		System.out.println(bNum);
		System.out.println(oNum);
		System.out.println(xNum);
		
		int year = 2022;
		int month = 3;
		
		System.out.println(year);
		System.out.println(year+month);
		
		String str =new String("자바");
		System.out.println(str);
		

	}

}
```

### 4. 변수의 이름

* 영문자 (대문자, 소문자 구분)나 숫자를 사용.

```
    - 특수문자 중 $와 _만 사용할수 있음 (나머지는 x)
```    

* 시작은 숫자로 할수 없음
* 예약어는 사용불가  
* **그 용도에 맞게 가독성이 좋게 만드는 것이 중요 (★)**

```
    - int numberOfStudnet; // 학생 수 (카멜 표기법)
    - int number_of_student; // 학생 수 (스네이크 표기법) 
```
        
## 5. 지수 

```
                                                   10진수의 정수값
                            (지수)    
          1     *      2    (1승)   =    2                2
      (가수)          (밑수)



                              (지수)    
                       2      (2승) =    4                4
                      (밑수)


        ...

                              (지수)    
                       2      (8승) =    2 * 2 * 2 .. * 2 =256              
                      (밑수)
```

```
     
            (10진수를 2진수로

              2       |11
              2       | 5         1   | (위로 올라감)
              2       | 2         1   |
              2       | 1         0   |                       10진수 11은 2진수 1011(2진수)
                            ->        |
                      ---------------->

            (2진수를 10진수로

                (2진수)1011 = 1 * 2(3승) + 0 * 2(2승) + 1 * 2(1승) + 1 * 2(0승)
                  
                                8       +     0     +     2      +      1           = 11 
```

```
             -----------------------------------------------------
                10진수 숫자                         2진수 신호

                    0                                            0
                    11                                        1011
                    255                                  1111 1111 
                *   256                        0000 0001 1111 1111                       
             ------------------------------------------------------

                 컴퓨터에서 정보를 처리하는 기본 단위 : 바이트 
                 바이트 단위 
                 256을 표현하는데 2바이트 (16비트)를 사용해서 하나의 신호로 사용
```



## 6. 자료형 (data type)

### 1. 변수와 메모리
* 변수를 선언하면 해당되는 자료형의 크기만큼 메모리가 할당

* 변수는 할당된 메모리를 가리키는 이름

```
    -int num =10;         //4바이트 정수형 메모리가 num 이라는 이름으로 할당됨
```

### 2. 기본 자료형 (primitive data type)의 종류

* 8개 
### byte 와 short
- byte : 1 바이트 단위의 자료형 

```
    => 동영상, 음악 파일, 실행 파일의 자료를 처리할 떄 사용
```    
- short : 2 바이트 단위의 자료형

### int 

- 자바에서 사용하는 정수에 대한 기본 자료형 (defalut)

- 4바이트 단위의 자료형

- 프로그램에서 사용하는 모든 숫자는 int로 저장함.    

### long

- 8 바이트 자료형

 - 숫자의 뒤에 알파벳 (대문자) L 또는 (소문자) l 을 써서 long형임을 표시함.

### 부동 소수점 방식

- 실수는 정수보다 정밀하기 때문에 정수와는 다른 방식으로 표현함

- 실수 값 0.1 표현

- 지수부와 가수부로 표현함.

- 컴퓨터에서는 밑수를 2로 사용 
### float형과 double형
- 자바에서는 실수의 기본 타입은 double을 사용함

### 문자는 어떻게 표현하여 사용하느냐?
- 문자도 정수로 표현함 

- 어떤 문자를 컴퓨터 내부에서 표현하기 위해 특정 정수 값을 정의 

- A는 65

```
    - 'A' => 65 ( encoding : 문자가 숫자로 변환되는 것 )
    - 'A' <= 65 ( decoding : 숫자에서 다시 문자로 변환되는 것 )
```

### 문자세트 (character set): 각 문자를 얼마나 표현할 것인지 코드 값을 모아둔 것
- 문자를 숫자로 변환한 값의 세트

- ASCII (아스키 코드) : 알파벳과 숫자 특수 문자등을 1바이트에 표현하는데 사용하는 문자세트

- UNICODE (유니 코드) : 전세계 표준으로 만든 문자 세트  

- UTF-8 : 1바이트에서 4바이트까지 다양하게 문자를 표현할 수 있음

```
   - EUC-KR등이 있음
```

- 자바는 문자를 나타내기 위해 전세계 표준인 UNICODE를 사용

- 문자를 위한 데이터 타입 char ch = 'A';    


### 논리형
- true(참), false(거짓) 두 가지만 나타냄
- 1바이트 사용
- 값이 존재하는지, 배열이 비었는지, 결과가 참인지 거짓인지를 표현
           
### 자료형 없이 사용하기 (자바 10부터 지원됨)
- Local variable type

- 추론 가능한 변수에 대한 자료형을 선언하지 않음

- 한번 선언하여 추론된 변수는 다른 타입의 값 대입할 수 없다.

- 지역변수만 사용가능

## 7. 상수와 리터럴, 형변환

### 1. 상수 (constant)
- 변하지 않는 수 

- ex) 원주를 3.14, 1년 12개월 등

- final 예약어를 이용하여 선언 

### 2. 리터럴 (literal)
- 프로그램에서 사용하는 숫자, 문자, 논리값을 뜻함 

- 리터럴은 상수 풀(constant pool)에 있음

- 정수 리터럴은 int로 실수 리터럴은 double로 저장

- int 범위를 벗어나는 long 경우는 접미사(식별자) L, l 을 써 줘야 한다.

- float로 사용하려는 경우 접미사(식별자) F, f 을 써 줘야 한다.

```
    - 부동소수점 값을 연산하면 약간의 오차 발생
    -애초에 근사치 값이기 때문.
```

### 3. type conversion (형변환)
- 서로 다른 자료형 간에 연산등의 수행을 위해 하나의 자료형으로 통일하는 것

- 묵시적 형변환 (자동 형변환 : explicit type conversion) ,   
  명시적 형변환 (강제 형변환 : implocit type conversion)

- 바이트 크기가 작은 자료형에서 큰 자료형으로 형 변환은 자동으로 이루어짐 

- 덜 정밀한 자료형에서 더 정밀한 자료형으로 형 변환은 자동으로 이루어짐 

```java
public class VarTest02 {

	public static void main(String[] args) {
		
		long result = 10L;
		float result2 = 10.1F;
		double dou = 9.999;
		
		System.out.println(result);
		System.out.println(result2);
		System.out.println(dou);
		
		double num1 = 1.0000001;
		System.out.println(num1);
		
		double num2 = 2.0000001;
		System.out.println(num2);
		
		double result4 = num1 + num2;
		System.out.println(result4);	//부동 소수점 값을 연산하면 약간의 오차 발생
								//애초에 근사치 값이기 때문에.
				
	}

}
```