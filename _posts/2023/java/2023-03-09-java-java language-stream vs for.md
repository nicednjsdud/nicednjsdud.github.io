---
published: true
title: (10분 테크톡) Java 52. Stream vs for
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Java 51. Stream vs for
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-03-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Stream vs for

1. 함수 객체 vs 코드 블록
2. 외부 반복 (how) vs 내부 반복 (what)
3. 가독성
4. 디버깅
5. 벙렬처리
6. 성능

## 1. for ? stream ?

### 1) for문

```java
  public static void main(String[] args){
    List<Integer> list = List.of(1,2,3,4,5);
    for(int i = 0; i< list.size(); i++){
      System.out.println(list.get(i));
    }
  }
```

- java 1부터 지원 for(초기화; 조건; 후처리)

### 2) 향상된 for 문

```java
  public static void main(String[] args){
      List<Integer> list = List.of(1,2,3,4,5);
      for(Integer i : list){
        System.out.println(i);
      }
    }
```

- java 5부터 지원 가독성 Up 안정성 Up

### 3) stream

![alt](/assets/images/post/ComputerStudy/834.png)

- java 8부터 지원

```java
  public void introduceStream(List<Integer> numbers){
    return number.stream()
            .filter(number -> number > 5)
            .map(Distance::new)
            .collect(Collectors.toList());
  }
```

- stream 생성 -> 중간 연산 -> 최종 연산

### 4) stream vs for

- 둘 다 다량의 데이터 처리 작업 사용
- 가독성이나 성능 등 여러 측면에서 차이가 존재

## 2. 함수 객체 vs 코드 블록 (표현 방식의 차이)

- for문은 **코드 블록**으로 표현

![alt](/assets/images/post/ComputerStudy/835.png)

- 스트림 파이프라인은 함수 객체로 표현

![alt](/assets/images/post/ComputerStudy/836.png)

- for문에서는 코드블록 그 외부 변수인 baseNumber를 코드 블록 내부에서 수정을 할 수 있다.
- stream의 경우에는 람다식으로 표현을 하기 때문에 람다식에서는 final이 붙거나 사실상 final인 변수만 읽을수 있다.
  - 따라서 외부 변수인 baseNumber를 수정할 수가 없다.

![alt](/assets/images/post/ComputerStudy/837.png)

- for에서 할수 있는 continue, break 로직은 stream에서는 할수가 없다.

![alt](/assets/images/post/ComputerStudy/838.png)

## 3. 외부 반복(how) vs 내부 반복 (what)

- 다음은 중복 체크에서 중복이 제거된 요소돌의 개수를 구하는 코드이다.

![alt](/assets/images/post/ComputerStudy/839.png)

- for문에서 중복을 허용하지 않는 set에 데이터들을 삽입하고, size 메소드를 통해 중복이 제거된 요소들의 개수를 구함

  - 이는 구체적인 구현 로직이 외부에 노출되는 외부 반복 형식이다.
  - **how 중심의 코드**

- stream은 구체적인 구현로직이 외부에 노출되지 않는 내부 반복의 형태를 띈다.
  - **what 중심의 코드**

## 4. 가독성

- 점수의 평균을 구하는 코드이다.

![alt](/assets/images/post/ComputerStudy/840.png)

- 로또 당첨 코드이다.

![alt](/assets/images/post/ComputerStudy/841.png)

- 이처럼 for문으로 요소를 순회하면서 return을 하는 경우에는 메서드 추출을 통해 Indent Depth를 줄이는 것이 어렵다.
- 이런 경우엔 Stream을 이용하면 Depth를 줄여서 가독성을 높일 수 있다.

### 1) 하지만 stream이 무조건 가독성이 좋은것이 아니다.

![alt](/assets/images/post/ComputerStudy/842.png)

- 해당 코드는 이펙티브 자바에서 발췌한 아나그램에 관한 코드이다.
- stream을 활용한 코드를 보면 collect도 여러개이고 로직이 람다식으로 복잡하게 얽혀있어 읽기 어렵다..
- 이런 경우에는 오히려 왼쪽 처럼 for문으로 표현한 코드가 읽기 쉬울 수 있다.

![alt](/assets/images/post/ComputerStudy/843.png)

- 이와 같이 단순한 이중 for문의 경우에도 stream으로 변환했을 시 Stream이 for문보다 복잡해 보일 수 있다.

## 5. 디버깅

![alt](/assets/images/post/ComputerStudy/844.png)

- 해당 코드는 숫자들을 특정값으로 나눠 합하는 로직을 for문과 stream으로 각각 구현한 코드이다.
- 여기에서 만약 매개변수 dividedNumber에 0이 들어온다면 DivideByZeroException이 발생

### 1) 스트림 예외

![alt](/assets/images/post/ComputerStudy/845.png)

- 스트림에서 stack trace 발생
- steram은 내부적으로 수행되는 작업이 많기 때문에 굉장히 복잡하게 출력된다.
- 스트림은 많은 내부 수행 작업과 지연 연산으로 인해 디버깅이 다수 어렵다.

### 2) for문 예외

![alt](/assets/images/post/ComputerStudy/846.png)

- for문에서 stack trace 발생
- 간결하게 출력되어 디버깅에 유리할 수 있다.

## 6. 벙렬 처리

![alt](/assets/images/post/ComputerStudy/847.png)

- 숫자들의 합을 계산하는 간단한 예시이다.
  - List의 size가 커진다면?
  - iterativeSum이 많이 호출된다면?

### 1) 스트림을 사용하지 않는다면

![alt](/assets/images/post/ComputerStudy/848.png)

- 오른쪽 코드를 보시면 벙렬처리를 위해 Runnable을 구현하여 숫자들의 합을 구하는 SumThread 클래스를 작성
- 왼쪽 코드는 SumThread를 이용하여 숫자들의 합을 병렬방식으로 구하는 작업을 수행

- 만약 로직이 복잡하다면?

### 2) 스트림을 사용한다면

![alt](/assets/images/post/ComputerStudy/849.png)

- 스트림이 내부적으로 처리해주기 때문에 보다 쉽게 벙렬처리를 표현할 수 있다.

## 7. 성능

### 1) 측정 대상

1. int 배열 덧셈
2. ArrayList 덧셈
3. int 배열 최대값 구하기
4. ArrayList 최대값 구하기

### 2) 배열 덧셈 성능 비교

![alt](/assets/images/post/ComputerStudy/850.png)

- 배열 덧셈의 경우에는 for가 Stream에 비해 약 7배 정도 빠른 성능을 보여줌

### 3) 배열 최댓값 성능 비교

![alt](/assets/images/post/ComputerStudy/851.png)

- 배열 최댓값의 경우에는 for가 Stream에 비해 약 2.6배 정도 빠른 성능을 보여줌

### 4) ArrayList 덧셈 성능 비교

![alt](/assets/images/post/ComputerStudy/852.png)

- ArrayList 최댓값의 경우에는 for가 Stream에 비해 약 1.4배 정도 빠른 성능을 보여줌

### 5) ArrayList 최댓값 성능 비교

![alt](/assets/images/post/ComputerStudy/853.png)

- ArrayList 최댓값의 경우에는 for가 Stream에 비해 약 0.9배 정도 빠른 성능을 보여줌

### 6) int 배열에서 for문이 stream보다 빠른 이유

![alt](/assets/images/post/ComputerStudy/854.png)

- for는 나온지 오래된 만큼 stream에 비해 JVM에서 최적화가 많이 이루어졌다.
- 하지만 Stream은 자바 8부터 등장했기 때문에 상대적으로는 최적화가 덜 되어 있다.
- 따라서 for문이 성능면에서는 더 낫다.

### 7) 스트림 생성에 따른 오버헤드 발생

![alt](/assets/images/post/ComputerStudy/855.png)

- 스트림은 사용하려면 Stream 객체를 생성해야 한다.
- 이 생성 과정에서 여러 작업들이 이루어지고 Stream에서 필요한 다른 객체를 생성하는데 오버헤드가 발생
- 반면 for의 경우에는 추가적인 객체 생성 없이 Index를 통해서 메모리에 직접 접근을 하기 때문에  
  Stream에 비해서 오버헤드가 발생하지 않는다.

### 8) PS. 향상된 for문에서는 원시타입 배열에 어떻게 접근 할까?

- 원시타입 배열이 들어오는 경우에는 내부적으로 전통 for문 처리

![alt](/assets/images/post/ComputerStudy/856.png)

### 9) List에서 성능 차이가 미미한 이유

![alt](/assets/images/post/ComputerStudy/857.png)

- int 배열은 요소들이 원시타입인 반면에 컬렉션은 Wrapper 타입이 들어오게 된다.
- 그래서 이와같은 박싱 및 언박싱에 대한 오버헤드가 발생이 된다.
- 이 오버헤드는 충분이 크기때문에 컬렉션에 대한 성능 측정은 앞서 설명한 이 오버헤드에 지배되면서 큰 성능차이 x
- 하지만 int 배열에 대한 성능 측정에서는 이와 같은 오버헤드의 영향이 적어 분명한 성능 차이가 보인다.
  - 성능을 고려한다면 for문과 원시타입 배열을 사용하는것이 좋아 보인다.

![alt](/assets/images/post/ComputerStudy/858.png)

- 오늘날의 하드웨어는 충분히 빠르기 때문에 소프트웨어에서는 성능보다는 다른 점들을 더욱 신경쓰는 추세
- 성능이 정말 중요한 프로그램이라면 고려해볼만 하지만
  - 그렇지 않다면 성능보다는 유지보수, 가독성 등을 고려하는 것이 더욱 좋다.

## 8. 결론

### 1) 가독성

- Stream이 가독성이 좋을 수도 있다.
- 가독성은 결국 취향의 영역
- 하지만 그렇다고 Steram을 남용한다면 오히려 가독성을 해칠 수도 있다.

### 2) 디버깅

- for문에 비해 stream이 디버깅하기 어렵다.

### 3) 벙렬처리

- 벙렬처리는 개발자들이 직접 신경 써야 할 부분들을 Stream이 내부적으로 처리를 해주기 때문에 Stream을 통한  
  벙렬처리가 보다 간단하다.

### 4) 성능

- for문이 성능이 더 좋을 수 있다.
- 하지만 오늘날 성능이 그리 중요한 쟁점은 아니다.
- 가독성, 유지보수성등 다른 점들을 더욱 고려해야한다고 생각

### 5) 스트림을 적용하기 좋은 조건

- 원소들의 시퀀스를 **일관되게 변환**한다.
- 원소들의 시퀀스를 **필터링** 한다.
- 원소들의 시퀀스를 **하나의 연산을 사용해 결합**한다.
- 원소들의 시퀀스를 **컬렉션에 모은다.**
- 원소들의 시퀀스에서 **특정 조건을 만족하는 원소를 찾는다.**
- **절대적이 아님으로 참고용**

## 출처

<a href="https://www.youtube.com/watch?v=by8hb75i9X4">크리스, 로마의 steram vs for</a>
