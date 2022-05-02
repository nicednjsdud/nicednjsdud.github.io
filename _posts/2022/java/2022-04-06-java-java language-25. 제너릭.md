---
title: Java 24. 제너릭
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is java generic?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, java generic
last_modified_at: '2022-04-06 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

제너릭
======

## 1.Generic(무엇이든 담을 수 있는) (자료형)프로그래밍

*  변수의 선언, 메서드의 매개변수를 하나의 참조 자료형이 아닌 여러 자료형으로  
   변환 될 수 있도록 프로그래밍 하는 방식

* 클래스에서 사용하는 변수의 자료형이 여러개 일 수 있고, 그 기능(메서드)은  
   동일한 경우 클래스의 자료형을 특정하지 않고, 추후 해당 클래스를 사용할 때  
   지정할 수 있도록 설정

* 실제 사용되는 자료형으로의 변환은 컴파일러에 의해 검증하므로 안정적인 프로그래밍 방식이 됨.

* 컬렉션 프레임워크에서 많이 사용되고 있음.

## 2.다이아몬드 연산자 <>

```java
    ArrayList<String> = new ArayList<>();
```

## 3.자료형 매개 변수 T

* 여러 참조 자료형으로 대체 될 수 있는 부분을 하나의 문자로 표현
* E : element, K : key, V : value 등 여러 알파벳을 의미에 따라 사용 가능 

```java
    class Powder {                              // powder 클래스
	@Override
	public String toString() {
		return "재료는 Powder 입니다.";
	    }
    }
    class Plastic {                             // plastic 클래스
	@Override
	public String toString() {
		return "재료는 Plastic 입니다.";
	    }
    }
    public class GenericPrinter<T>{             // 제너릭 클래스
        private T material;

        public void setMaterial(T material){
            this.material=material;
        }
        public T getMaterial(){
            return material;
        }    
    }
```

```java
public class GenericPrinterTest {

	public static void main(String[] args) {
		GenericPrinter<Powder> powderPrinter = new GenericPrinter<>(); // powder
		powderPrinter.setMaterial(new Powder());                // 객체생성
		Powder powder = powderPrinter.getMaterial();            // 형변환 x
		System.out.println(powder);	// 재료는 powder 입니다.
		
		GenericPrinter<Plastic> plasticPrinter = new GenericPrinter<>();// plastic
		plasticPrinter.setMaterial(new Plastic());			// 객체생성
		Plastic plastic= plasticPrinter.getMaterial();		      // 형변환 x	
		System.out.println(plastic);// 재료는 plastic 입니다.
		
	    }
    }
```

## 4.<T extends 클래스>

* T 대신에 사용될 자료형을 제안하기 위해 사용
* T 자료형의 범위를 제한할수 있음.
* 상위 클래스에서 선언하거나 정의하는 메서드를 활용할 수 있음.
* T에 무작위 클래스가 들어갈 수 없게 상속받은 클래스로 한정.


```java
    abstract class Material {           //추상 클래스
	
	public abstract void doPrinting();
}

    class Plastic extends Material {    // 플라스틱 클래스
	
	@Override
	public String toString() {
		return "재료는 Plastic 입니다.";
	}

	@Override
	public void doPrinting() {
		System.out.println("Plastic으로 프린팅합니다.");
	    }

}
    class Powder extends Material {     // 파우더 클래스
	
	@Override
	public String toString() {
		return "재료는 Powder 입니다.";
	}
	@Override
	public void doPrinting() {
		System.out.println("Powder로 프린팅합니다.");
	    }	
}

    public class GenericPrinter<T extends Material> {   // 제너릭 클래스
	
	private T material;

	public T getMaterial() {
		return material;
	}

	public void setMaterial(T material) {
		this.material = material;
	}
    @Override
	public String toString() {
		return material.toString();
	}
    public void printing() {
		material.doPrinting();
	}    
}
```

```java
public class GenericPrinterTest {

	public static void main(String[] args) {
		GenericPrinter<Powder> powderPrinter = new GenericPrinter<>();	//powder
		Powder powder = new Powder();		// 기본생성자 
		powderPrinter.setMaterial(powder);
		System.out.println(powderPrinter);	// 재료는 powder입니다.
		
//		GenericPrinter<Water> water = new GenericPrinter<>();	// 상속x 
		GenericPrinter<Plastic> plasticPrinter = new GenericPrinter<>();
		Plastic plastic = new Plastic();	// 기본생성자
		plasticPrinter.setMaterial(plastic);
		System.out.println(plasticPrinter); // 재료는 plastic 입니다.
	}

}
```

## 5.자료형 매개 변수가 두개 이상일 때

```java
    public class PointM<T,V>{
        T x;
        V y;

        Point(T x, V y){
            this.x=x;
            this.y=y;
        }
        public T getX(){        // 제네릭 메서드
            return x;
        }
        public V getY(){
            return y;
        }
    }
```    

## 6.제너릭 메서드

* 자료형 매개변수를 메서드의 매개변수나 반환 값으로 가지는 메서드
* 자료형 매개변수가 하나 이상인 경우도 있음.
* 제네릭 클래스가 아니어도 내부에 제네릭 메서드는 구현하여 사용할 수 있음.
* 형식

```java
        public <자료형 매개 변수> 반환형 메서드 이름(자료형 매개 변수...){}
```

```java
public class GenericMethod {
	
	public static <T, V> double makeRectangle(Point<T, V> p1,Point<T, V> p2){
		
		double left = ((Number)p1.getX()).doubleValue();
		double right =((Number)p2.getX()).doubleValue();
		double top = ((Number)p1.getY()).doubleValue();
		double bottom =((Number) p2.getY()).doubleValue();
		
		double width = right -left;
		double height = bottom-top;
		
		return width * height;
		
	}

	public static void main(String[] args) {
		Point<Integer, Double> p1 = new Point<>(0, 0.0);
		Point<Integer, Double> p2=new Point<>(10, 10.0);
		
		double rect = makeRectangle(p1, p2);
		System.out.println("두점으로 만들어진 사각형의 넓이는 : "+rect); //100.0
	}

}
```
