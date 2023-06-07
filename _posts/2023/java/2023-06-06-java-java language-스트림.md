---
published: true
title: (10분 테코톡) Java 62. 스트림
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
last_modified_at: "2023-06-06 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 람다와 스트림

## 목차

### 2) 스트림

- 스트림은 뭐하는 거야?
- 스트림은 생성, 중간연산, 최종연산으로 이루어져 있어
- 데이터 소스로부터 스트람을 생성해보자
- 중간연산으로 데이터를 입맛에 맞게 가공해보자
- 최종연산으로 스트림을 닫아보자

## 2. 스트림

### 1) 스트림은 뭐하는 거야?

1. 개울, 시내
2. 물줄기
3. 계속 이어진 줄

- 뭔가 연속된 정보를 처리하기 위해 사용됨
- JAVA 8부터 다량의 데이터 처리 작업을 돕기 위해 추가되었다.

![alt](/assets/images/post/ComputerStudy/1036.png)

* 스트림은 데이터 소스가 다르더라도, 일단 스트림을 생성하기만 한다면, 과거에 그 데이터의 형태가 무엇이었던 같은 방식으로 다룰 수 있게 되어 코드의   
  재사용서잉 높아진다.

```java
  String[] strArr = {"aa","bb","cc","ddd"};
  List<String> strList = Arrays.asList(strArr);

  Stream<String> strStream1 = strList.stream();
  Stream<String> strStream2 = Arrays.stream(strArr);

  strStream1.sorted().forEach(System.out::println);
  strStream2.sorted().forEach(system.out::println);
```

### 2) 스트림은 생성, 중간연산, 최종연산으로 이루어져 있어

![alt](/assets/images/post/ComputerStudy/1037.png)

```java
  List<String> names = crews.stream()   // 생성
          .filter(crew -> crew.getCourse().equals(Course.BACKEND))    //  중
          .map(Crew:;getName)                                         //  간
          .limit(10)                                                  //  연산
          .collect(toList());         // 최종연산
```

### 3) 데이터 소스로부터 스트람을 생성해보자

![alt](/assets/images/post/ComputerStudy/1038.png)

#### 3-1) Collection 클래스

```java
  default Stream<E> stream(){
    return StreamSupport.stream(spliterator(), false);
  }
```

```java
  private final List<Card> cards;

  private boolean hasAce(){
    return cards.steram().anyMatch(Card::isAce);
  }
```

#### 3-2) 배열

```java
  Stream<T> stream.of(T... values)
  Stream<T> stream.of(T[])
  Stream<T> Arrays.stream(T[])
```

#### 3-3) 숫자

```java
  IntStream intStream = new Random().ints();
  LongStream longStream = new Random().longs();
  DoubleStream doubleStream = new Random().doubles();
```

#### 3-4) 람다식

```java
  static <T> stream<T> iterate(T seed, UnaryOperator<T> f)
  static <T> steram<T> generate(Supplier<T> s)
```

```java
  Stream.iterate(0, n- > n + 2)
          .limit(4)
          .forEach(System.out::println);  // 0.2,4,6
```

### 4) 중간연산으로 데이터를 입맛에 맞게 가공해보자

![alt](/assets/images/post/ComputerStudy/1039.png)

#### 4-1) distinct()

* 스트림에서 중복되는 데이터를 제거

```java
  private void validateDuplicatenames(List<PlayerName> names){
      if(name.size() != names.stream().distinct().count()){
        throw nre IllegalArgumentException("플레이어 이름은 중복될 수 없음!")
      }
  }
```

* PlyaerName으로 중복되는 데이터가 있는지 검사하고, 중복이 존재하면 예외를 던지는 코드

#### 4-2) filter(Predicate<T> predicate)

* 조건을 만족하는 데이터만 남기고 나머지를 제외

```java
  public static Menu findMenuByName(String name){
    return menus.stream()
                .filter.elemet -> element.getName().equals(name)
                .findFirst()
                .orelseTrhow(NoSuchElementException::new)
  }
```

* 이름이 같은지 비교해 이 조건을 만족하는 데이터만을 남기고, 나머지는 제외

#### 4-3) sorted(Comparator<T> comparator)

* sorted() : 기본 정렬 기준으로 정렬
* 스트림으로 지정된 Comparator로 정렬

```java
  Stream<String> names = Stream.of("bob1","bob3","bob2");
  system.out.println(names.sorted().collect(Collectors.joining(" ")));
  // bob1 bob2 bob3
```

* Comparator를 별도 지정하지 않아 기본정렬 (가나나순) 기준으로 정렬

#### 4-4) map(Function<T,R> mapper)

* 원하는 필드만 뽑아내거나, 특정 형태로 변환

```java
  public Participants(List<String> names, Cards cards){
    validateSize(names);
    this.players = names.stream()
            .map(Name::new)
            .map(name -> new Player(name, cards.giveInitialCards()))
            .collect(Collectors.toList());
    this.dealer = new Dealer(cards.giveInitialCards());
  }
```

* String에서 name를 변환하고, name에서 Player로 변환

#### 4-5) flatMap(Function<T,R> mapper)

* 트럼프 카드 52장을 만드는 코드

```java
  private static Deque<Card> initializeCards(){
    Deque<Card> cards = new ArrayDeque<>();
    for(Value value : Value.values()){
        for(Shap shape : Shape.values()){
          cards.push(new Card(value,shape));
        }
    }
    return cards;
  }
```

* 평탄화 
* 스트림의 원를 각각 하나의 스트림으로 매핑한 다음, 그 스트림들을 다시 하나의 스트림으로 합침

```java
  private static Deque<Card> initializeCards(){
      return Arrays.stream(Value.values())
              .flatMap(value -> Arrays.stream(Shape.values())
                  .map(shape -> new Card(value, shape)))
              .collect(Collectors.toCollection(ArrayDeque::new));

  }
```

### 5) 최종연산으로 스트림을 닫아보자

![alt](/assets/images/post/ComputerStudy/1040.png)

#### 5-1) forEach(Consumer<? super T> action)

* 스트림의 데이터를 소모하며 주로 출력하는 용도로 사용

```java
  Steram.iterate(0 , n -> n + 2)
        .limit(4)
        .forEach(System.out::println);    // 0,2,4,6
```

* 중간 연산까지 마친 스트림의 숫자를 차례대로 출력

#### 5-2) 조건 검사

```java
  boolean allMatch(Predicate<? super T> predicate)    // 모든 요소가 일치하면 true
  boolean anyMatch(Predicate<? super T> predicate)    // 하나의 요소라도 일치하면 true
  boolean noneMatch(Predicate<? super T> predicate)   // 모든 요소가 불일치하면 true
```

* 현재 가지고 있는 카드 중에 ACE카드가 존재하면 true를 반환

```java
  private boolean hasAceCard(){

      return cards.stream()
              .map(Card::getNumber)
              .anyMatch(cardNumber -> cardsNumber.equals(CardNumber.ACE));
  }
```

* findFirst() : 조건에 일치하는 첫 번째 요소를 반환
* 게임이 끝나지 않은 첫번째 플레이어를 반환

```java
  public Player getUnfinishedPlayer(){
    return players.steram()
            .filter(player -> !player.isFinished())
            .findFirst()
            .orElseThrow(() -> new IllegalStateException("카드를 뽑을 수 있는 플레이거가 더이상 없습니다."));
  }
```



* findAny() : 조건에 일치하는 요소를 하나 반환

#### 5-3) collect(Collector collector)

* 스트림의 요소를 수집해 원하는 형태로 반환
* 스트림의 최종 연산
* 컬렉터를 파라미터로 받음

##### 1) Collector

* 인터페이스
* 이걸 구현해야 collect의 파라미터로 사용할 수 잇음


##### 2) Collectors

* 이미 정의된 컬렉터를 static 메서드로 제공하는 클래스


1. collect(Collectors.toList())
  * 데이터를 수집해 리스트 형태로 반환

```java
  List<String> playerNames = participants.getPlayers().stream()
              .map(Participant::getName)
              .collect(Collectors.toList());
```

2. collect(Collectors.toMap())

```java
  toMap(Function<? super T, ? extends K> keyMapper,
        Function<? super T, ? extends U> valueMapper,
        BunaryOperator<U> mergeFunction)
```

```java
  Map<String,Student> studentsMap = 
              students.stream().collect(
                    toMap(student -> student.getName(),
                            student-> student,
                            (existing,replacement) -> existing));
```

* 같은 이름의 학생이 두번 입력되면 먼저 들어온 학생만을 저장


#### 5-4) collect(Collectors.groupingBy())

```java
  Map<Country, List<Person>> peopleByCountry =
            people.stream().collect(
                groupingBy(person -> person.getCountry()));
```


#### 5-5) collect(Collectores.joining())

* 데이터를 연결하여 반환

```java
  public void printInitialMessage(final List<Player> players){

      String playersNames = players.steram()
              .map(Participant::getName)
              .collect(Collectors.joining(", "));
      System.out.printf("딜러와 %s에게 2장을 나누었습니다." + system.lineSeparator(),playerNames);
  }
```

#### 5-6) reduce(T identity, BinaryOperator<T> accumulator)

* reduce(BinaryOperator<T> accumulator) : 초기값이 없을 경우 사용
* 스트림의 데이터를 줄여 나가면서 연산을 수행하고 최종 결과를 반환


* 분류 함수를 인자로 받아서, 데이터를 그룹화하여 맵을 반환

```java
  public static void main(String[] args){

      int sum = IntStream.rangeColsed(1,5).reduce(0, (number1,nubmer2) -> number1 + number2);
      int count = IntStream.rangeColsed(1,5).reduce(0, (number1,number2) -> number1 + 1);

      System.out.println(sum);    // 15
      System.out.println(count);  // 5
  }
```

## 3. 반복문 vs 스트림

### 1) 반복문

* 지역변수를 읽고 수정해야 할 때
* return, break,continue를 사용해야 할때

### 2) 스트림

* 연속된 데이터를 일관되게 변환할 때
* 연속된 데이터를 필터림 할때
* 연속된 데이터를 하나의 연산으로 합칠 때
* 연속된 데이터에서 특정 조건을 만족하는 데이터를 찾을 때


## 출처

<a href="https://www.youtube.com/watch?v=4ZtKiSvZNu4">깃짱, 이리내의 람다와 스트림</a>
