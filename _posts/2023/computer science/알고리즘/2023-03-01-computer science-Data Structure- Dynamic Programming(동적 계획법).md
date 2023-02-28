---
title: (알고리즘) Dynamic Programming (동적 계획법)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: Dynamic Programming (동적 계획법)
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-26 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Dynamic Programming (동적 계획법)

## 1. 개요

- DP, 즉 다이나믹 프로그래밍은 기본적인 아이디어로 하나의 큰 문제를 여러 개의 작은 문제로 나누어서 그 결과를 저장하여 다시 큰 문제를  
  해결할 때 사용하는 것
- 특정한 알고리즘이 아닌 하나의 문제해결 패러다임으로 볼 수 있음
- 큰 문제를 작은 문제로 쪼개서 그 답을 저장해두고 재활용

## 2. DP를 쓰는 이유

- 재귀 방식과 매우 유사
- 큰 차이점은 일반적인 재귀를 단순히 사용 시 **동일한 작은 문제들이 여러번 반복 되어 비효율적인 계산**이 될수 있음
- 예) 피보나치 수열

```
  1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144 ...
```

- 피보나치 수를 구하고 싶을 때 재귀로 함수를 구성하면 `return f(n) = f(n-1) + f(n-2)`
- 그런데 `f(n-1), f(n-2)`에서 각 함수를 1번씩 호출하면 동일한 값을 2번씩 구하게 됨
  - 이로인해 100번째 피보나치 수를 구하기 위해 호출되는 함수의 횟수는 기하급수적으로 증가
  - 왜냐하면, `f(n-1)`에서 한번 구한 값을 `f(n-2)`에서 또 다시 같은 값을 구하는 과정을 반복하게 됨
  - 위에 피보나치를 재귀가 아닌 재사용이면 어떨까? -> `O(n^2) -> O(f(n))`

## 3. DP의 사용 조건

- **Overlapping Subproblems (겹치는 부분 문제)**
- **Optimal Substructure (최적 부분 구조)**

### 1) Overlapping Subproblems

- DP는 기본적으로 문제를 나누고 그 문제의 값을 재활용해서 전체답을 구함
- **그래서 동일한 작은 문제들이 반복하여 나타는 경우에 사용이 가능**
- 즉, DP는 부분 문제의 결과를 저장하여 재 계산하지 않을 수 있어야 하는데, 해당 부분 문제가 반복적으로 나타나지 않는다면 재사용이 불가
- 그래서 부분 문제가 중복되지 않는 경우에는 사용 X

### 2) Optimal Substrcture

- **부분 문제의 최적 결과 값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우를 의미**
- 그래서 특정 문제의 정답은 문제의 크기에 상관없이 항상 동일!
- 만약, A-B까지의 가장 짧은 경로를 찾고자 하는 경우를 예시로 할때, 중간에 X가 있을 때, A-X/X-B가 많은 경로 중에 가장 짧은 경로라면,  
  전체 최적 경로도 A-X-B가 정답이 된다.

![alt](/assets/images/post/ComputerStudy/809.png)

- 위에 그림에서 A-X 사이의 최단 거리는 AX2이고 X-B는 BX2이다. 전체 최단 경로는 `AX2-BX2`이다.
  - 다른 경로를 선택한다고 해서 전체 최단 경로가 변할수 없다.
- 이와 같이 부분 문제에서 구한 최적 결과가 전체 문제에서도 동일하게 적용되어 결과가 변하지 않을때 DP를 사용할 수 있음
- 피보나치 수열도 동일하게 이전의 계산 값을 그대로 사용하여 전체 답을 구할 수 있어 최적 부분 구조를 갖고 있다.

## 4. DP 사용 하기

- **DP는 특정한 경우에 사용하는 알고리즘이 아니라 하나의 방법론이므로 다양한 문제해결에 쓰일 수 있다.**
- 그래서 DP를 적용할 수 있는 문제인지를 알아내는 것부터 코드를 짜는 과정이 난이도가 쉬운것부터 어려운 것 까지 다양하다.
- 일반적으로 DP를 사용하기전에 아래의 과정을 거쳐 진행 할 수 있다.

```
  1) DP로 풀 수 있는 문제인지 확인
  2) 문제의 변수 파악
  3) 변수 간 관계식 만들기 (점화식)
  4) 메모하기
  5) 기저 상태 파악하기
  6) 구현하기
```

### 1) DP로 풀 수 있는 문제인지 확인

- 애초에 이 부분 부터 해결이 매우 어렵다.
- 우선 DP의 조건 부분에서 써내렷듯이, 현재 직면한 문제가 작은 문제들로 이루어진 하나의 함수로 표현될 수 있는지를 판단
- **즉, 위에서 쓴 조건들이 충족되는 문제인지를 한번 체크해보는 것이 좋다.**
- 보통 특정 데이터 내 최대화 / 최소화 계산을 하거나 특정 조건 내 데이터를 세야 한다거나 확률 등의 계산의 경우 DP로  
  풀수 잇는 경우가 많다.

### 2) 문제의 변수 파악

- DP는 현재 변수에 따라 그 결과 값을 찾고 그것을 전달하여 재사용하는 것을 거친다.
- 즉, 문제 내 변수의 개수를 알아내야 한다는 것, 이것을 영어로 `state`를 결정한다고 한다.
- 예를 들어, **피보나치 수열**에서는 n번째 숫자를 구하는 것이므로 n이 변수가 된다.

  - 그 변수가 얼마이냐에 따라 결과값이 다르지만 그 결과를 재사용 하고 있다.

- 또한, **문자열 간의 차이**를 구할 때 문자열의 길이,Edit 거리 등 2가지 변수를 사용한다.
- 또, 유명한 **Knapsack 문제**에서는 index, 무게로 2가지의 변수를 사용한다.

### 3) 변수 간의 관계식 만들기

- 변수들에 의해 결과 값이 달라지지만 동일한 변수값인 경우 결과는 동일하다.
- 또한, 우리는 그 결과값을 그대로 이용할 것이므로 그 관계식을 만들어낼 수 있어야 하낟.
  - 그러한 식을 **점화식**이라고 부르며 그를 통해 우리는 짧은 코드 내에서 반복/재귀를 통해 자동으로 해결되도록  
    구축할 수 잇게 된다.

### 4) 메모하기

- 변수 간 관계식까지 정상적으로 생성되었다면 **변수의 값에 따른 결과를 저장**해야 한다.
- 이를 메모한다고 하여 `Memoization`이라고 부른다.
- 변수 값에 따른 결과를 저장할 배열등을 미리 만들고 그 결과를 나올 때마다 배열 내에 저장하고 그 저장된 값을 재사용  
  하는 방식으로 문제를 해결해 나간다.
- 이 결과 값을 저장할 때는 보통 배열을 쓰며 변수의 개수에 따라 배열의 차원이 1 ~ 3 차원 등 다양할 수 있다.

### 5) 기저 상태 파악하기

- **가장 작은 문제의 상태를 알아야 한다.**
- 보통 몇 가지 예시를 직접 손으로 테스트 하여 구성하는 경우가 많다.
- 피보나치 수열을 예시로들면, `f(0) = 0 f(1) = 1`과 같은 방식이다.
  - 이후 두가지 숫자를 더해가며 값을 구하지만 가장 작은 문제는 저 2개로 볼 수 있다.
- 해당 기저 문제에 대해 파악 후 미리 배열등에 저장해두면 된다.

### 6) 구현하기

- **Bottom-Up (Tabulation 방식) - 반복문 사용**
- **Top-Down(Memozation 방식) - 재귀 사용**

#### 6-1) Bottom-Up 방식

- **아래에서 부터 계산을 수행하고 누적시켜서 더 큰 문제를 해결하는 방식**이다.
- 메모를 위해서 dp라는 배열을 만들었고 이것이 1차원이라 가정했을때, `dp[0]`가 기저 상태이고 `dp[n]`을 목표  
  상태라고 하자.
  - Bottom-up은 `dp[0]`부터 시작하여 반복문을 통해 점화식으로 결과를 내서 `dp[n]`까지 그값을 전이시켜  
    재활용 하는 방식
- 반복을 통해 `dp[0]`부터 하나씩 채우는 과정을 `table-filing`이라고 하며, 이 Table에 저장된 값에 직접  
  접근하여 재활용하므로 `Tabulation`이라는 명칭이 붙었다고 한다.
- 사실상 근본적인 개념은 결과값을 기억하고 재활용한다는 측면에서 메모하기와 크게 다르지 않다.

#### 6-2) Top-Down 방식

- `dp[0]`의 기저 상태에서 출발하는 대신 `dp[n]`의 값을 찾기 위해 **위에서 부터 바로 호출을 시작**하여 `dp[0]`.
  의 상태까지 내려간 다음 해당 **결과값을 재귀를 통해 전이시켜 재활용 하는 방식**
- 피보나치 예시처럼 `f(n) = f(n-2) + f(n-1)`의 과정에서 함수 호출 트리의 과정에서 보이듯, n = 5 일때  
  f(3), f(2)의 동일한 계산이 반복적으로 나오게 된다.
- 이 때, 이미 이전에 계산을 완료한 경우에는 단순히 메모리에 저장되어 있던 내역을 꺼내서 활용하면 된다.
  - 그래서 가장 최근의 상태 값을 메모해 두었다고 해서 `Memoization`이라고 부른다.

### 7) 예시 (피보나치)

```java
  public class Fibonacci {

    // DP 를 사용 시 작은 문제의 결과값을 저장하는 배열
    // Top-down, Bottom-up 별개로 생성
    static int[] topDown_memo;
    static int[] bottomUp_table;
    public static void main(String[] args){

      int n = 30;
      topDown_memo = new int[n+1];
      bottomUp_table = new int[n+1];

      long startTime = System.currentTimeMillis();
      System.out.println(naiveRecusrsion(n));
      long endTime = System.currentTimeMillis();
      System.out.println("일반 재귀 소요 시간 : " + (endTime - startTime));

      System.out.println();

      long startTime = System.currentTimeMillis();
      System.out.println(topDown(n));
      long endTime = System.currentTimeMillis();
      System.out.println("Top-Down DP 소요 시간 : " + (endTime - startTime));

      System.out.println();

      long startTime = System.currentTimeMillis();
      System.out.println(bottmUp(n));
      long endTime = System.currentTimeMillis();
      System.out.println("Bottom-Up DP 소요 시간 : " + (endTime - startTime));

      System.out.println();
    }

    // 단순 재귀를 통해 Fibonacci를 구하는 경우
    // 동일한 계산을 반복하여 비효율적으로 처리가 수행됨
    public static int naiveRecursion(int n){

      if( n <= 1){
        reutrn n;
      }
      return naiveRecursion(n-1) + naiveRecursion(n-2);
    }

    // DP Top-Down을 사용해 Fibonacci을 구하는 경우
    public static int topDown(int n){

      // 기저 상태 도달시 0 , 1 초기화
      if(n < 2) return topDown_memo[n] = n;

      // 메모에 게산된 값이 있으면 바로 반환
      if(topDown_memo[n] > 0) reutrn topDown_memo[n];

      // 재귀 사용
      topDown_memo[n] = topDown(n-1) + topDown(n-2);

      return topDown_memo[n];
    }

    // DP Bottom-Up을 사용해 Fibonacci를 구하는 경우
    public static int bottomUp(int n){

      // 기저 상태의 경우 사전에 미리 저장
      bottomUp_table[0] = 0;
      bottomUp_table[1] = 1;

      // 반복문을 사용
      for(int i = 2; i<=n; i++){
        // Table을 채워감
        bottomUp_table[i] = bottomUp_table[i-1] + bottomUp_table[i-2];
      }
      return bottomUp_table[n];
    }
  }

  /*
결과
832040
일반 재귀 소요 시간 : 9

832040
Top-Down DP 소요 시간 : 0

832040
Bottom-Up DP 소요 시간 : 0
*/
```

<a href="https://hongjw1938.tistory.com/47">출처</a>
