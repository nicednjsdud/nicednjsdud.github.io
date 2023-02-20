---
published: true
title: Java 36. Abstract Factory Pattern (Design Pattern - 3)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Abstract Factory Pattern
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-02-17 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Abstract Factory Pattern

## 1. Abstract Factory Pattern

- 여러 제품군을 한꺼번에 생성하는 패턴

## 2. 의도와 동기

- 구체적인 클래스를 생성하지 않고도 서로 관련성이 있거나 독립적인 여러 객체의 군을 생성하기 위한 인터페이스 제공
- 추상화된 인터페이스 팩토리를 제공하고 상황에 따라 그에 맞는 인스턴스들이 생성되도록 함
- 가령 데이터베이스에 따라 DAO 클래스가 달라져야 한다고 할 때, 현재 사용해야 하는 DB의 종류에 따른 DAO 인스턴스를  
  한꺼번에 생성
- 위젯을 생성하여 보여줄 때 선택한 옵션에 따라 위젯의 set이 달라질 수 있도록 함
- 생성되고 구성되고 표현되는 방식과 무관하게 시스템을 독립적으로 만들고자 할 때
- 하나 이상의 제품군들 중 하나를 선택하여 시스템을 설정해야 하고 한번 구성한 제품을 다른것으로 대체할 수 있을 때

## 3. 객체 협력

### 1) AbstractFactory

- 개념적 제품에 대한 객체를 생성하는 오퍼레이션 인터페이스를 제공

### 2) ConcreteFactory

- 구제적인 제품에 대한 객체를 생성하는 오퍼레이션 제공

### 3) AbstractProduct

- 개념적 제품 객체에 대한 인터페이스를 제공

### 4) ConcreteProduct

- 구체적으로 팩토리가 생성할 객체를 정의하고, AbstractProduct가 정의하고 있는 인터페이스를 구현

### 5) Client

- AbstractFactory 와 AbstractProduct 클래스에 선언된 인터페이스를 사용

## 4. 중요할 결론

- 일반적으로 ConcreteFactory 클래스의 인스턴스는 실행 할 때 만들어진다.
- 구체적 팩토리는 어떤 특징 구현을 갖는 제품 객체를 생성한다.
- 서로 다른 제품 객체를 생성하기 위해서 사용자는 서로 다른 ConcreteFactory를 사용
- AbstractFactory는 ConcreteFactory 서브클래스를 통해 필요한 제품 객체를 생성하는 책임을 위임

## 5. 구현

- UserInfo.java

```java
  package domain.userinfo;

  public class UserInfo {

    private String userId;
    private String password;
    private String userName;

    // getter, setter
    ...
  }
```

- Product.java

```java
  package domain.product;

  public class Product {

    private String productId;
    private String productName;

    // getter, setter
    ...
  }
```

- ProductDao.java **(Interface)**

```java
  package domain.product.product;

  import doamin.product.Product;

  public interface ProductDao {

    void insertProduct (Product product);
    void updateProduct (Product product);
    void deleteProduct (Product product);
  }
```

- UserInfoDao.java **(Interface)**

```java
  package domain.userinfo.dao;

  import domain.userInfo.userInfo

  public interface UserInfoDao {

    void insertUserInfo (UserInfo userInfo);
    void updateUserInfo (UserInfo userInfo);
    void deleteUserInfo (UserInfo userInfo);
  }
```

### Mysql, Oralce DAO 생성

- ProductMySqlDao.java

```java
  package domain.product.dao.mysql;

  import domain.product.Product;
  import domain.product.dao.ProductDao;

  public class ProductMySQlDao implements ProductDao{

      @Override
      public void insertProduct(Product product){

      }

      @Override
      public void updateProduct(Product product){

      }

      @Overrdie
      public void deleteProduct(Product product){

      }
  }
```

- ProductOracleDao.java

```java
  package domain.product.dao.oracle

  import domain.product.Product;
  import domain.product.dao.ProductDao;

  public class ProductOracleDao implements ProductDao{

      @Override
      public void insertProduct(Product product){

      }

      @Override
      public void updateProduct(Product product){

      }

      @Overrdie
      public void deleteProduct(Product product){

      }
  }
```

- UserInfoMySqlDao.java

```java
  package domain.userinfo.dao.mysql;

  import domain.userinfo.userInfo;
  import domain.userinfo.dao.UserInfoDao;

  public class UserInfoMySQlDao implements UserInfoDao{

      @Override
      public void insertUserInfo(UserInfo userInfo){

      }

      @Override
      public void updateUserInfo(UserInfo userInfo){

      }

      @Overrdie
      public void deleteUserInfo(UserInfo userInfo){

      }
  }
```

- ProductOracleDao.java

```java
  package domain.userinfo.dao.oracle

  import domain.userinfo.UserInfo;
  import domain.userinfo.dao.UserInfo;

  public class UserInfoOracleDao implements UserInfoDao{

      @Override
      public void insertUserInfo(UserInfo userInfo){

      }

      @Override
      public void updateUserInfo(UserInfo userInfo){

      }

      @Overrdie
      public void deleteUserInfo(UserInfo userInfo){

      }
  }
```

### Factory 생성

- DaoFactory.java

```java
  import domain.product.dao.ProductDao;
  import domain.userinfo.dao.UserInfoDao;

  public interface DaoFactory{

    public UserInfoDao createUserInfoDao();
    public ProductDao createProductDao();
  }
```

- OralceDaoFactory.java

```java

  import domain.product.dao.ProductDao;
  import domain.product.dao.oracle.ProductOralceDao;
  import domain.userinfo.dao.UserInfoDao;
  import domain.userinfo.dai.oracle.UserInfoOracleDao;

  public class OracleDaoFactory implements DaoFactory{

    @Override
    public UserInfoDao createUserInfoDao() {
      return new UserInfoOracleDao();
    }

    @Override
    public ProductDao createProductDao() {
      return new ProductOracleDao();
    }
  }
```

- MysqlDaoFactory.java

```java

  import domain.product.dao.ProductDao;
  import domain.product.dao.mysql.ProductOralceDao;
  import domain.userinfo.dao.UserInfoDao;
  import domain.userinfo.dai.mysql.UserInfoOracleDao;

  public class MysqlDaoFactory implements DaoFactory{

    @Override
    public UserInfoDao createUserInfoDao() {
      return new UserInfoMysqlDao();
    }

    @Override
    public ProductDao createProductDao() {
      return new ProductMysqlDao();
    }
  }
```

### Web (main)

- WebClient.java

```java
  public class WebClinet {

    public static void main(String[] args){

      FileInputStream fis = new FileInputStream("db.properties");

      Properties prop = new Properties();
      prop.load(fis);

      String dbType = prop.getProperty("DBTYPE");

      UserInfo userInfo = new UserInfo();
      userInfo.setUserId("12345");
      userInfo.setPassword("!@#$%");
      userInfo.setUserName("BOB");

      Product product = new Product;
      product.setProductId("0011AA");
      product.setProductName("TV");

      DaoFactory daoFactory = null;

      if(dbType.equals("MYSQL")){
        daoFactory = new MySqlDaoFactory();
      }
      else if (dbType.equals("ORACLE")){
        daoFactory = new OracleDaoFactory();
      }
      else{
        System.out.println("error");
      }

      UserInfoDao userInfoDao = daoFactory.createUserInfoDao();

      userInfoDao.insertUserInfo(userInfo);
      userInfoDao.updateUserInfo(userInfo);
      userInfoDao.deleteUserInfo(userInfo);

      ProductDao productDao = daoFactory.createProductDao();

      productDao.insertProduct(product);
      productDao.updateProduct(product);
      productDao.deleteProduct(product);
    }
  }
```

- db.properties

```java
  DBTYPE = ORACLE
```

- 혹은

```java
  DBTYPE = MYSQL
```
