---
published: true
title: Java 35. Prototype Pattern (Design Pattern - 2)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Prototype Pattern
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-15 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Prototype Pattern

## 1. Prototype Pattern

- 복제해서 인스턴스를 만드는 패턴

## 2. 의도와 동기

- 클래스의 인스턴스가 생성과정이 복잡하거나 여러 조합에 의해 생성되어야 하는 경우 하나의 견본을 만듦
- 그 다음, 초기화 해두고 이를 복제하여 객체를 생성하는 방법

## 3. 객체 협력

- 복제하는데 필요한 인터페이스(하나의 통로 , Api)를 정의하고, 그 인터페이스를 구체적으로 쓰는 패턴

## 4. 중요한 결론

- 프로토타입 속성값을 활용하여 다양한 객체를 생성할 수 있음
- 서브 클래스의 수를 줄일 수 있다.
- 자바에서는 clone()메서드를 재정의하여 구현한다.

## 5. 예제

- PrototypeTest.java

```java


class Book {

  private String author;
  private String title;

  public Book(String author, String title){
    this.author = author;
    this.title = title;
  }

  // getter, setter

  public String toString() {

      return "("+author + "," + title; + ")"
  }
}

class BookShelf implements Colneable{

  private ArrayList<Book> shelf;

  public BookShelf() {
    shelf = new ArrayList<Book>();
  }

  public void addBook(Book book) {

    shelf.add(book);
  }

  // getter, setter

  @Override
  protected Object clone() throws CloneNotSupportedException {
    // return super.clone();   // 얕은 복사
    BookShelf another = new BookShelf();    // 깊은 복사
    for(Book book : shelf){
      another.addBook(new Book(book.getAuthor(), book.getTitle())));
    }
    return antoher;
  }

  public String toString() {
    return shelf.toString();
  }
}

public class PrototypeTest {

    public static void main(String[] args) throws CloneNotSupportedException{

        BookShelf bookShelf = new BookShelf();

        bookShelf.addBook(new Book("태백산맥","조정래"));
        bookShelf.addBook(new Book("밥1","밥1"));
        bookShelf.addBook(new Book("bob1","bob1"));

        System.out.println(bookShelf);
        // [(조정래,태백산맥),(밥1,밥1),(bob1,bob1)]

        BookShelf another = (BookShelf)bookShelf.clone();

        System.out.println(another)
        // [(조정래,태백산맥),(밥1,밥1),(bob1,bob1)]

        bookShelf.getShelf().get(0).setAuthor("조정래");
        bookShelf.getShelf().get(0).setTitle("한강");

        System.out.println(bookShelf);
        System.out.println(another);
        // [(조정래,한강),(밥1,밥1),(bob1,bob1)]
        // [(조정래,한강),(밥1,밥1),(bob1,bob1)]
        // 얕은 복사가 됨


        // 깊은 복사 하면
        // [(조정래,한강),(밥1,밥1),(bob1,bob1)]
        // [(조정래,태백산맥),(밥1,밥1),(bob1,bob1)]


    }
}

```
