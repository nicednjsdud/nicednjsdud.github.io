---
published: true
title: Java 46. Memento Pattern (Design Pattern - 14)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Memento Pattern (Design Pattern - 14)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-27 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Memento Pattern

## 1. Memento Pattern 이란?

- 내부상태를 객체화하여, 나중에 객체가 이 상태로 복구 가능하게 함
- 인스턴스의 상태를 보존해 두었다가 보존해 둔 정보를 가지고 인스턴스를 원래 상태롭 복원
- 인스턴스를 복원하기 위해서는 내부 정보에 자유롭게 접근 가능해야 함
- 캡슐화가 파괴가 일어나지 않도록 주의해야 함

## 2. 의도와 동기

- 이전의 상태로 되돌리는 undo
- 했던 작업을 다시 하는 redo
- 기억해야 하는 순간을 저장하는 객체
- 오류를 복구하거나 수행 결과를 취소하기 위한 작업에 사용

## 3. 객체 협력

### 1) Memento

- Originator 객체의 내부 상태를 필요한 만큼 저장한다. Originator만이 Memento에 접근할 수 있다.

### 2) Originator

- Memento를 생성하여 현재 객체의 상태를 저장하고 내부 상태를 복구

### 3) CareTaker (undo mechanism)

- Memento의 보관을 책임지기는 하지만, memento의 내부를 확인할 수 없음

## 4. 중요한 결론

- 복잡한 Originator 클래스의 내부 상태를 다른 객체로 분리함으로써 상태에 대한 캡슐화를 보장
- 복구에 필요한 상태만 따로 관리함으로써 Originator내부에서 저장하지 않고 Originator가 단순해질 수 있다.
- Memento의 사용에 오버헤드가 발생할 수 있다.

## 5. 예제

- Gamer.java

```java
  package memento;
  import java.util.ArrayList;

  public class Gamer{

    private int meney;          // 소유한 돈
    private ArrayList<String> fruits = new ArrayList<String>(); // 과일
    private Random random = new Random(); //난수 발생기
    private static String[] fruitsname = {    // 과일 이름의 표
      "사과","포도","바나나","귤",
    };
    public Gamer(int money){
      this.money = money;   // 생성자
    }
    public int getMoney(){
      return money;         // 현재의 돈을 얻는다.
    }
    public void bet(){
      int dice = random.nextInt(6) + 1;   // 주사위를 던진다.
      if(dice == 1){
        money += 100;                           // 1이 나온다. 돈이 증가
        System.out.println("돈이 증가했습니다.");
      }
      else if (dice == 2){
        money /= 2;                           // 2가 나온다. 돈이 반으로 줄어듬
        System.out.println("돈이 반으로 줄었습니다.");
      }
      else if(dice == 6){
        String f = getFruit();
        System.out.println("과일 (" + f + ")을 받았습니다."); // 6이 나온다. 과일을 받음
      }
      else{                                 // 그 밖에.. 아무일도 일어나지 않는다.
        System.out.println("아무일도 일어나지 않았습니다.")
      }
    }
    public Memento createMemento(){   // 스냅샷을 찍는다.
        Memento memento = new Memento(Money);
        Iterator<String> fruit = furits.iterator();
        while(fruit.hasNext()){
          String name = fruit.next();
          if( name.startsWith("good~")){
            memento.addFruit(name);
          }
        }
        return memento;
    }
    public restoreMemento(Memento memento){ // undo를 실행한다.
      this.money = memento.money;
      this.furits = memento.fruits;
    }
    public String toString(){
      return "[money = " + money + ", fruits = " + fruits + "]";
    }
    private String getFruits(){
      String prefix = "";
      if(random.nextBoolean()){   // 과일을 한개 얻는다.
        prefix = "good~";
      }
      return prefix + fruitsname[random.nextInt(frutisname.length)];
    }

  }
```

- Main.java

```java
  package memento;

  import java.util.ArrayList;
  public class Main {
    public static void main(String[] args) {
        Gamer gamer = new Gamer(100);               // 처음의 돈은 100
        Memento memento = gamer.createMemento();    // 처음의 상태를 보존해 둔다.
        ArrayList<Memento> history = new ArrayList<Memento>();
        for (int i = 0; i < 100; i++) {
            System.out.println("==== " + i);        // 횟수 표시
            System.out.println("현 상태:" + gamer);    // 현재의 주인공의 상태 표시

            gamer.bet();    // 게임을 진행 시킨다.

            System.out.println("돈은" + gamer.getMoney() + "원이 되었습니다.");

            // Memento의 취급 결정
            if (gamer.getMoney() > memento.getMoney()) {
                System.out.println("    (많이 증가했으니 현재의 상태를 보존해두자)");
                memento = gamer.createMemento();
                history.add(memento);
            } else if (gamer.getMoney() < memento.getMoney() / 2) {
                System.out.println("    (많이 줄었으니 이전의 상태로 복귀하자)");
                gamer.restoreMemento(memento);

            }

            // 시간을 기다림
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
            }
            System.out.println("");
        }
    }
}

```

- Memento.java

```java
public class Memento {
    int money;                              // 돈
    ArrayList<String> fruits;                          // 과일
    public int getMoney() {                 // 돈을 얻는다.(narrow interface)
        return money;
    }
    Memento(int money) {                    // 생성자(wide interface)
        this.money = money;
        this.fruits = new ArrayList<String>();
    }
    void addFruit(String fruit) {           // 과일을 추가한다.(wide interface)
        fruits.add(fruit);
    }
}

```
