---
published: true
title: Java 49. Iterator Pattern (Design Pattern - 17)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Iterator Pattern (Design Pattern - 17)
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-28 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Iterator Pattern

## 1. Iterator Pattern 이란?

- 객체 요소들의 내부 표현방식을 공개하지 않고, 객체에서 되지 않은, 외부에서 객체에 순회하는 객체를 만든다.

## 2. 의도와 동기

- 내부에서 객체의 순차적인 제공을 하지 않음
- 순회 구현 방식이 다르더라도 동일한 방식으로 순회 할 수 있게 제공
- 여러 리스트 객체에 대한 동일한 방식으로 순회하는 방법을 제공하기 위해 순회하는 객체를 따로만듬
- ex) Java Collection FrameWork의 Iterator

## 3. 객체 협력

### 1) Iterator

- 요소에 접근하고 순회하는데 필요한 메서드 제공

### 2) ConcreteIterator

- Iterator에 정의된 인터페이스를 구현하는 클래스

### 3) Aggregate

- Iterator 객체를 생성하는 인터페이스 정의

### 4) ConcreteAggregate

- 해당하는 ConcreteIterator의 인스턴스를 반환하도록 Iterator 생성 인터페이스를 구현

## 4. 중요한 결론

- ConcreteIterator는 리스트를 순회하면서 각 리스트의 요소를 반환하는 메서드도 제공
- 다양한 순회방법이 제공될 수 있다.
- 동일한 Aggregate를 구현한 클래스들은 동일한 방식으로 순회할 수 있다.

## 5. 예제

- Aggregate.java (interface)

```java
  package iterator;
  public interface Aggregate{
    public abstract Iterator iterator(int type);
    public int getLength();
  }
```

- Iterator.java (interface)

```java
  package iterator;

  public interface Iterator {
    public abstract boolean hasNext();
    public abstract Object next();
  }
```

- Constant.java

```java
  package iterator;

  public class Constant {
    public static final int FORWARD = 0;
    public static final int REVERSE = 1;
  }
```

- Factory.java (abstract)

```java
  package iterator;

  public abstract class Factory {
    public final Iterator create(Aggregate list, int type){
      Iterator p = createProduct(list, type);
      return p;
    }

    public abstract Iterator createProduct(Aggregate list, int type);
  }
```

- IteratorFactory.java

```java
  package iterator;

  public class IteratorFactory extends Factory {

    private static IteratorFactory iFactory = new IteratorFactory();
    private IteratorFactory() {}
    public static IteratorFactory getInstance(){     // 싱글톤
      return iFactory;
    }

    @Override
    public Iterator createProduct(Aggregate list, int type){

      return null;
    }
  }
```

- book.java

```java
  package iterator;


  public class Book {
    private String name = "";
    public Book(String name){
      this.name = name;
    }
    public String getName(){
      return name;
    }
  }
```

- BookShelf.java

```java
  package iterator;

  public class BookShelf implements Aggregate {

    private Book[] books;
    private int last = 0;
    Factory f = IteratorFactory.getInstance();

    public BookShelf(int maxSize){
      this.books = new Book[maxSize];
    }
    public Book getBookAt(int index){
      return books[index];
    }
    public void appendBook(Book book){
      this.book[last] = book;
      last++;
    }
    public int getLength(){
      return last;
    }
    public Iterator iterator(int type){
      Iterator i = f.create(this, type);
      return i;
    }
  }
```

- ForwardShelfIterator.java

```java
  package iterator;


  public class ForwardShelfIterator implements Iterator {

    private BookShelf bookShelf;
    private int index;

    public ForwardShelfIterator(Aggregate list){

        bookShelf = (BookShelf)list;
        index = 0;
    }

    @Override
    public boolean hasNext(){
        if(index < bookShelf.getLength()){
          return true;
        }
        return false;
    }

    @Override
    public Object next(){

       Book book = bookShelf.getBookAt(index);
       index ++;
       return book;
    }
  }
```

- ReverseBookShelfIterator.java

```java
  package iterator;

  public class ReverseBookShelfIterator implements Iterator{
     private BookShelf bookShelf;
    private int index;

    public ReverseBookShelfIterator(Aggregate list){

        bookShelf = (BookShelf)list;
        index = bookShelf.getLength() - 1;
    }

    @Override
    public boolean hasNext(){
        if(index >= 0){
          return true;
        }
        return false;
    }

    @Override
    public Object next(){

       Book book = bookShelf.getBookAt(index);
       index --;
       return book;
    }
  }
```
