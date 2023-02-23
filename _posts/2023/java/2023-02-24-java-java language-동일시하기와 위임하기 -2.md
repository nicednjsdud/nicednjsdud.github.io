---
published: true
title: Java 42. 동일시하기와 위임하기 Composite Pattern (Design Pattern - 10)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: 동일시하기와 위임하기 Decorator,Composite
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-24 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 동일시하기와 위임하기 Decorator,Composite

## 1. Composite Pattern 이란?

- 그릇과 내용물을 동일시

## 2. 의도와 동기

- 부분과 전체에 대한 복합 객체의 트리구조를 나타낼 수 있음
- 클라이언트가 개별 객체와 복합 객체를 동일하게 다룰 수 있는 인터페이스를 제공
- 재귀적인 구조

## 3. 객체 협력

### 1) Component

- 전체의 부분 객체에서 공통적으로 사용할 인터페이스 선언
- 전체와 부분 객체에서 공통으로 사용할 기능 구현
- 전체 클래스가 부분 요소들을 관리하기 위해 필요한 인터페이스 선언

### 2) Leaf

- 집합 관계에서 다른 객체를 포함할 수는 없고 포함되기만 하는 객체로 가장 기본이 되는 기능을 구현

### 3) Compsite

- 여러 객체를 포함하는 복함 객체에 대한 기능 구현
- 포함한 여러 객체를 저장하고 관리하는 기능을 구현

### 4) Client

- Component에 선언된 인터페이스를 통하여 부분과 전체를 동일하게 처리

## 4. 중요한 결론

- 기본 객체는 복합 객체에 포함이 되고, 복합 객체 역시 또 다른 복합객체에 포함될 수 있다.
- 클라이언트 코드는 기본객체와 복합객체에 대한 일관된 프로그래밍을 할 수 있다.
- 기본객체가 증가하여도 전체 객체의 코드에 영향을 주지 않는다.
- 새로운 요소의 추가가 편리하고 범용성 있는 설계가 가능하다.

## 5. 예제

- 제품의 카테고리와 제품의 계층구조를 Compsite Pattern으로 구현

- ProductCategory.java

```java
  package composite;

  public class ProductCategory {

      int id;
      String name;
      int price;

      public ProductCategory(int id, String name, int price){
        this.id = id;
        this.name = name;
        this.price = price;
      }

      public abstract void addProductCategory(ProductCategory productCategory);
      public abstract void removeProductCategory(ProductCategory productCategory);
      public abstract int getCount();
      public abstract int getPrice();
      public abstract String getName();
      public abstract int getId();

  }
```

- Product.java

```java
  package composite;

  public class product extends ProductCategory{

    public Product(int id, String name, int price){
      super(id, name, price);
    }

    @Override
    public void addProductCategory(ProductCategory productCategory){

    }

    @Override
    public void removeProductCategory(ProductCategory productCategory){

    }

    @Override
    public int getCount(){
      return 1;
    }

    @Override
    public int getPrice(){
      return price;
    }

    @Override
    public String getName(){
      return name;
    }

    @Override
    public int getId(){
      return id;
    }

  }
```

- Category.java

```java
  package composite;

  public class Category extends ProductCategory {

    ArrayList<ProductCategory> list;

    public Category(int id,String name, int price){
      super(id,name,price);
      list = new ArrayList<ProductCategory>();
    }

     @Override
    public void addProductCategory(ProductCategory productCategory){
        list.add(productCategory);
    }

    @Override
    public void removeProductCategory(ProductCategory productCategory){
        for(ProductCategory temp : list){
          if(temp.getId() == productCategory.getId()){
            list.remove(temp);
            return;
          }
        }
        System.out.println("상품이 없습니다.");
    }

    @Override
    public int getCount(){
      int count = 0;
      for( ProductCategory temp : list){
        count += temp.getCount();
      }
      return count;
    }

    @Override
    public int getPrice(){
      int price = 0;
      for( ProductCategory temp : list){
        price += temp.getPrice();
      }
      return price;
    }

    @Override
    public String getName(){
      return name;
    }

    @Override
    public int getId(){
      return id;
    }
  }
```
