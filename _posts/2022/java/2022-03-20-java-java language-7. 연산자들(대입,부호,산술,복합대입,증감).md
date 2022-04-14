---
title: Java 4.연산자들
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is 연산자?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language
last_modified_at: '2022-03-20 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

## 1. 항과 연산자

* 항 (operand) : 연산에 사용되는 값

*  연산자 (operator) : 항을 이용하여 연산하는 기호


## 2. 대입 연산자 (assingnment operator)

* 변수에 변수나 값을 대입하는 연산자 

* 이항 연산자 중 우선순위가 가장 낮은 연산자
* 왼쪽 변수 = 오른쪽 변수(or 식, 값)

## 3. 부호 연산자 

*  단항 연산자

*  변수의 부호를 유지하거나(+) 바꿈(-)

```
        +           +x      부호 유지(의미없는 연산)
        -           -x      부호 반전
```

* 실제 변수의 부호가 변하려면 대입 연산자를 사용해야 함.


## 4. 산술 연산자

### 사칙 연산자

```java
        +
        -
        *           곱하기
        /           나누기의 몫
        %           나누기의 나머지
```

## 5. 복합 대입 연산자 

* 대입연산자와 다른 연산자가 함께 사용

```java
       a += b       a = a + b
       a -= b       a = a - b
       a *= b       a = a * b
       a /= b       a = a / b
       a %= b       a = a % b
```    

```java
public class AssignOperatorTest {

	public static void main(String[] args) {
		int result =0;
		
		result +=10;							//result = result +10;
		System.out.println("result : " + result);
		
		result -=5;								//result = result -5;
		System.out.println("result : "+result);
		
		result *=5;								//result = result*5;
		System.out.println("result : "+result);
		
		result /=5;								//result = result/5;
		System.out.println("result : "+result);
		
		result %=5;								//result = result%5;
		System.out.println("result : "+result);
	}

}
```

## 6. 증가, 감소 연산자
    
*  증감연산자는 변수의 값을 1증가시키거나 1감소시킬 때 사용.

```
       ++           ++x             다른연산 전 x값을 증가시킴
                    x++             다른연산 후 x값을 증가시킴

       --           --x             다른연산 전 x값을 감소시킴
                    x--             다른연산 후 x값을 감소시킴            
```

## 7. 비교 연산자 ( 관계 연산자 )

*  두 피연산자를 비교해 결과값으로 논리 값인 true나 false를 반환해줌.

```java
    int x = 2;
    int y = 1;
```

```java
       ==           x==y        x와 y는 같다.       false                    
       !=           x !=y       x와 y는 같지 않다.  true
       >                                           true
       >=                                          true 
       <                                           false
       <=                                          false

```

## 8. 논리 연산자       

* 관계연산자와 혼합하여 많이 사용 됨

* 연산의 결과가 true, false으로 반환 됨

### 연산자

```
    && ( 논리곱, And )      두 항이 모두 참이면 결과값이 참 그렇지 않으면 다 거짓

    || ( 논리합, Or  )      두 항중에 하나의 항이라도 참이면 결과값은 참 
                                두 항이 모두 거짓이면 결과값은 거짓

    !  ( 부정, Not   )      값이 참인 경우는 거짓으로 바꿈 값이 거짓인 경우 참으로 바꿈
```

```java
public class ShortCircuitEvaluation {

	public static void main(String[] args) {
		
		int x =0;
		int y =0;
		boolean result;
		
		result = ((x= x + 1)< 0 ) && ((y = y + 1) > 0);
		System.out.println("result = " + result);
		System.out.println("x= "+x);
		System.out.println("y= "+y);
		
		result = ((x= x+1)>0) || ((y=y+1)>0);
		System.out.println("result = " + result);
		System.out.println("x= "+x);
		System.out.println("y= "+y);
	}

}
```

### 논리연산 진리표

```java
        A              B                    A && B              A || B          !A
    ---------------------------------------------------------------------------------

        true         true                     true                true          false
        true         false                   false                true          false
        false        true                    false                true          true
        false        false                   false                false         true   
    ---------------------------------------------------------------------------------
```

* 두 명제가 모두 참이면 논리곱은 참

```
       두 명제중 하나라도 참이면 논리곱은 참
       참의 부정은 거짓, 거짓의 부정은 참
```

* 논리 연산에서 모든 항이 실행되지 않는 경우 - short circuit evaluation (SCE)

```
    - 최단 거리 평가
    - 연산의 효율 및 속도 향상을 위해 불필요한 연산을 수행하지 않는 기능
    - 논리곱
        - 둘다 참이어야 참 => 앞쪽이 거짓이면 뒤쪽 계산을 수행하지 않음

    - 논리합
        - 둘중 하나라도 참이면 참 => 앞쪽이 참이면 뒤쪽 계산을 수행하지 않음
```

## 9. 조건 연산자

* 삼항 연산자
* 주어진 조건식이 참인 경우와 거짓인 경우에 다른 결과값을 나타내주는 연산자

```
    - 조건식의 결과가 true인 경우와 false인 경우에 따라서 다른 결과가 수행됨
```

* 조건식 ? 참일 때 실행 : 거짓일 때 실행 ;

```
       조건식 ?   결과 1     :      결과 2  ;
       => 조건식이 참이면 결과1 조건식이 거짓이면 결과2가 선택됨    
```

## 10. 단항, 이항, 삼항 연산자가  

* 연산자를 항 개수로 구분
* 단항연산자 : 하나의 피연산자만으로 이루어진 식으로 연산 수행.

```
                    ++x, y--
```

* 이항연산자 : 피연산자를 두 개 가지고 식을 구성함 
* 삼항연산자 : 항이 세개 있어야 함

```java
public class ConditionTest2 {
	public static void main(String[] args) {
		
		Scanner scanner = new Scanner(System.in);
		
		System.out.print("정수를 입력하세요 : ");
		int score = scanner.nextInt();
		
		char grade = (score>= 90) ? 'A' : 'B';
		System.out.println("당신의 점수등급은 : "+grade);
		
		
		//삼항연산자 중첩
		grade = (score >= 90) ? 'A' : ((score >=80) ? 'B' : 'C');
		System.out.println("당신의 점수등급은 : "+grade);
	
				
		scanner.close();
	}
}
```

## 11. 연산자 우선순위

```java
                우선순위            종류            연산자
            --------------------------------------------------                    

                    1                              . []   () 
                    2               단항            ++ -- ! + -
                    3               산술            *   /  %
                    4               산술            +   -
                    5               비교            < <= > >=
                    6               관계            ==  !=
                    7               논리곱          &&
                    8               논리합          ||
                    9               조건            ? : 
                    10              대입            = += -= /= %=
            ---------------------------------------------------
```