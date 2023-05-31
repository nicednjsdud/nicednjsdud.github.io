---
published: true
title: (10분 테코톡) Java 60. Generic
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-06-01 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Generic

## 목차

1. 제네릭이란?

- 변성

2. 제네릭 타입
3. 제네릭 메서드
4. 와일드카드
5. 제네릭 타입 소거

## 1. 제네릭 이란?

- 컴파일 타임에 타입을 체크함으로써 코드의 안정성을 높여주는 기능

```java
  List<T>   // 타입 매개 변수
  List<String>  stirngList = new ArrayList<String>();
      // 매개변수화된 타입
```

### 1) 컴파일 타임에 강력한 타입 검사

- 제네릭 미사용

```java
  List stringList = new ArrayList<>();
  stringList.add("BoB");
  stringList.add(1);
  String result = (String) stringList.get(0) + (String) stringList.get(1);    // Runtime Error !
```

- 제네릭 사용

```java
  List<String> stringList = new ArrayList<>();
  stringList.add("BoB");
  stringList.add(1);    // Compile Error !
```

### 2) 캐스팅(타입 변환) 제거

- 제네릭 미사용

```java
  List stringList = new ArrayList<>();
  stringList.add("BoB");
  String result = (String) stringList.get(0);
```

- 제네릭 사용

```java
  List<String> stringList = new ArrayList<>();
  stringList.add("BoB");
  String result = stringList.get(0);
```

### 3) 변성

#### 1) 배열 vs 제네릭 타입

- 배열 - 공변

```java
  Object[] objectArray = new Integer[1];
```

- 제네릭 타입 - 무공변

```java
  List<Object> objectList = new ArrayList<Integer>(); // Compile Error !
```

#### 2) 무공변(Invariance) - `<T>`

- 타입 B가 타입 A의 하위 타입일때, Category`<B>`가 Category`<A>`의 하위 타입이 아닌 경우.
- 즉 아무런 관계가 없다.

#### 3) 공변(Convariance) - `<? extends T>`

- 타입 B가 타입 A의 하위 타입일 때
- Category`<B>`가 Category`<A>`의 하위 타입인 경우.

#### 4) 반공변(Contravariance) - `<? super T>`

- 타입 B가 타입 A의 하위 타입일 때
- Category`<B>`가 Category`<A>`의 상위 타입인 경우.

## 2. 제네릭 타입 (Generic Types)

### 1) Class`<T>` interface`<T>`

- 비제네릭

```java
  class Category {

      private Object object;

      public void set(Object object){
        this.object = object;
      }

      public Object get(){
        return object;
      }
  }
```

- 제네릭

```java
  class Category<T>{

    private T t;

    public void set(T t){
      this.t = t;
    }
    public T get(){
      return t;
    }
  }
```

## 3. 제네릭 메서드 (Generic Methods)

```java
  class NoodleCategory<T>{

    private T t;

    public void set(T t){
      this.t = t;
    }

    public T get(){
      return t;
    }

    public <T> void printClassName(T t){
        System.out.println("클래스 필드에 정의된 타입 = " + this.t.getClass().getName());
        System.out.println("제네릭 메서드에 정의된 타입 = " + t.getClass().getName());
    }
  }

  NoodleCategory<Noodle> noodleCategory = new NoodleCategory<>();
  noodleCategory.set(new Noodle());
  noodleCategory.printClassName(new Pasta());
```

### 1) 제네릭 타입 제한의 필요성

```java
  class NoodleCategory<T>{

    private T t;

    public void set(T t){
      this.t = t;
    }

    public T get(){
      return t;
    }
  }

  NoodleCategory<Noodle> noodleCategory = new NoodleCategory<>();   // OK

  NoodleCategory<Coke> cokeNoodleCategory = new NoodleCategory<>(); // ????
```

### 2) 제한된 제네릭 타입

```java
class NoodleCategory<T extends Noodle>{

    private T t;

    public void set(T t){
      this.t = t;
    }

    public T get(){
      return t;
    }
  }

  NoodleCategory<Noodle> noodleCategory = new NoodleCategory<>();

  NoodleCategory<Ramen> ramenNoodleCategory = new NoodleCategory<>(); // OK

  NoodleCategory<Coke> cokeNoodleCategory = new NoodleCategory<>(); // Compile Error !
```

![alt](/assets/images/post/ComputerStudy/1030.png)

## 4. 와일드 카드

### 1) `<?>` Unbounded Wildcards

- 모든 타입이 가능

![alt](/assets/images/post/ComputerStudy/1031.png)

### 2) `<? extends Noodle>` Upper Bounded Wildcards

- Noodle과 Noodle의 하위 타입

![alt](/assets/images/post/ComputerStudy/1032.png)

### 3) `<? super Noodle>` Lower Bounded Wildcards

- Noodle과 Noolde의 상위 타입

![alt](/assets/images/post/ComputerStudy/1033.png)

### 4) 제한

```java
class NoodleCategory<T>{

    private T t;

    public void set(T t){
      this.t = t;
    }

    public T get(){
      return t;
    }
  }

class CategoryHelper {

  public void popNoodle(Category<? extends Noodle> category){
    Noodle noodle = category().get();   // 꺼내는 건 OK

    category.set(new Noodle());         // 저장은 NO
  }

  public void pushNoodle(Category<? super Noodle> category){
    category.set(new Noodle());       // 저장은 OK

    Noodle noodle = category.get();   // 꺼내는건 NO
  }
}
```

#### 4-1) 언제 무엇을 써야할까?

- **PECS**
- producer - extends, consumer - super

### 5) 와일드 카드 producer - extends

```java
  class NoodleCategory<E>{

    private List<E> list = new ArrayList<>();

    public void pushAll(Collection<? extends E> box){

      for(E e : box){
        list.add(e);
      }
    }
  }
```

### 6) 와일드 카드 consumer - super

```java
  class NoodleCategory<E>{

    private List<E> list = new ArrayList<>();

    public void popAll(Collection<? super E> box){

      box.addAll(list);
      list.clear();
    }
  }
```

## 5. 제네릭 타입 소거

- 타입 매개변수의 경계가 없는 경우에는 Object
- 경계가 있는 경우에는 **경계 타입**으로 타입 파라미터를 변경
- 타입 안전성을 유지하기 위해 필요한 경우 **타입 변환 추가**
- 제네릭 타입을 상속 받은 클래스의 다형성을 유지하기 위해 **Bridge method 생성**

## 출처

<a href="https://www.youtube.com/watch?v=w5AKXDBW1gQ">그린론의 제네릭</a>
