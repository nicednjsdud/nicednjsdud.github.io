---
title: 자바 I/O 3
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is IO
tag : java language
article_tag1: java IO
article_section: java IO
meta_keywords: java,java languagem, java IO
last_modified_at: '2022-04-14 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

## 1. 보조 스트림

* 실제 읽고 쓰는 스트림이 아닌 보조 기능을 제공하는 스트림

* **FilterInputStream** 과 **FilterOutputStream**이 보조 스트림의 상위 클래스들
* 생성자의 매개변수로 또 다른 스트림(기반 스트림이나 다른 보조 스트림)을 가짐 

```
    - protected FilterInputStream (InputStream in)
        - 생성자 매개변수 Inputstream을 받음.

    - public FilterOutputStream (OutputStream out)
        - 생성자 매개변수로 OutputStream을 받음.    
```

* **decorator** pattern으로 구현됨.

```
 바이트 단위 파일 입력 스트림 (기반 스트림) + 문자로 변환 기능 추가(보조 스트림)
                                                 + 버퍼링 기능 추가 (보조 스트림)    
``` 

* 보조스트림 활용

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

public class InputStreamReaderTest {

	public static void main(String[] args) {
		
		try(InputStreamReader isr =new InputStreamReader
								(new FileInputStream("reader.txt"))){
			
			int i;
			while((i=isr.read()) != -1) {
				System.out.print((char)i);
				// 안녕하세요 여러분들. abc
			}
			
		}catch(IOException e) {
			e.printStackTrace();
		}
	}

}
```

## 2. InputStreamReader와 OutputStreamWriter

* 바이트 단위로 읽거나 쓰는 자료를 문자로 변환해주는 보조 스트림

### buffered 활용 x

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileCopyTest {

	public static void main(String[] args) {
		
		long milisecond = 0;
		try(FileInputStream fis = new FileInputStream("mybatis-3.5.9.zip");
				FileOutputStream fos = new FileOutputStream("copy.zip")){			
			milisecond = System.currentTimeMillis();			
			int i;
			while((i = fis.read()) != -1) {
				fos.write(i);
			}
			milisecond = System.currentTimeMillis() - milisecond;
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		System.out.println("파일 복사하는 데 "+milisecond+ "milisecond 소요");
		// 파일 복사하는 데 17274milisecond 소요		
	}
}
```

## 3. BufferedInputStream 과 BufferedOutputStream
* 약 8192 바이트 배열을 가지고 있음. 

```
    - 입출력이 빠르게하는 기능이 제공되는 보조 스트림
```

* **BufferedInputStream** ( 바이트 기반 버퍼 입력 스트림 )

* **BufferedOutputStream** ( 바이트 기반 버퍼 출력 스트림 )
* **BufferedReader** ( 문자 기반 버퍼 입력 스트림 )
* **BufferedWriter** ( 문자 기반 버퍼 출력 스트림 ) 


### buffered 활용

```java
import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class BufferedStreamTest {

	public static void main(String[] args) {
		
		long milisecond = 0;
		
		try(FileInputStream fis = new FileInputStream("mybatis-3.5.9.zip");
				FileOutputStream fos = new FileOutputStream("copy2.zip");
				BufferedInputStream bis = new BufferedInputStream(fis);
				BufferedOutputStream bos = new BufferedOutputStream(fos)){
				
			milisecond = System.currentTimeMillis();
			
			int i;
			while((i=bis.read()) != -1) {
				bos.write(i);
			}
			
			milisecond = System.currentTimeMillis() -milisecond;
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		System.out.println("파일 복사하는 데 "+milisecond+ "milisecond 소요");
		// 파일 복사하는 데 33milisecond 소요
	}

}
```

## 4. DataInputStream과 DataOutputStream

* 자료가 메모리에 저장된 상태 그대로 자료형을 유지하며 읽거나 쓰는 기능을 제공

### 1. DataInputStream 메서드

* byte readByte()

```
    - 1바이트를 읽어 반환함
```

* boolean readBoolean()

```
    - 읽은 자료가 0이 아니면 true 0이면 false
```

* char readChar()

```
    - 한 문자를 읽어 반환 함
```

* short readShort()

```
    - 2바이트를 읽어 정수 값을 반환함
```

* int readInt()

```
    - 4바이트를 읽어 정수 값을 반환함
```

### 2. DataOutputStream 메서드

* void writeByte (int v)

```
    - 1바이트의 자료를 출력함
```

* void writeBoolean (boolean v)

```
    - 1바이트의 값을 출력함
```

* void writeUTF (String str)

```
    - UTF-8 인코딩 기반으로 문자열을 출력함
```

 등등

```java
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class DataStreamTest {

	public static void main(String[] args) {
		
		try(FileOutputStream fos = new FileOutputStream("data.txt");
				DataOutputStream dos = new DataOutputStream(fos)){
			
			dos.writeByte(100);
			dos.writeChar('A');
			dos.writeInt(10);
			dos.writeFloat(3.14F);
			dos.writeUTF("Hello");
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		try(FileInputStream fis = new FileInputStream("data.txt");
				DataInputStream dis = new DataInputStream(fis)){
			
			System.out.println(dis.readByte()); //100
			System.out.println(dis.readChar()); // A
			System.out.println(dis.readInt());  // 10
			System.out.println(dis.readFloat());// 3.14F
			System.out.println(dis.readUTF());  // Hello
			
		}catch(IOException e) {
			e.printStackTrace();
		}
	}

}
```

## 5. 직렬화 ( serialization )
* 객체의 상태를 그대로 저장하거나 다시 복원하는 것.

* 자바가상머신의 메모리에 있는 객체 데이터를 바이트 형태로 변환하는 기술.

```
    - 객체 자체를 저장할 수 있음.
```

* 인스턴스 상태 그대로 파일로 저장하거나 네트웍으로 전송하고 (serialization)  
  이를 다시 복원하는 방식

* 자바에서는 보조 스트림을 활용하여 직렬화를 제공함

* ObjectInputStream 과 ObjectOutputStream를 사용하여 파일에 쓰거나 네트웍으로 전송가능.

```
    - ObjectInputStream (InputStream in)
    - InputStream를 생성자의 매개변수로 받아 ObjectInputStream을 생성함.
```

```
    - ObjectOutputStream (OutputStream in)
    - OutputStream를 생성자의 매개변수로 받아 ObjectOutputStream을 생성함.
```

* 직렬화는 객체의 내용 중 private이 선언된 부분이 있더라도 인스턴스의 내용이  
  외부( 파일, 네트웍 )로 내용이 유출되는 것

```
    - 프로그래머가 직렬화 의도를 표시해야 함.
    - java.io.Serializable 인터페이스를 사용
    - 추상메서드가 없음 (구현 코드 없음)
    - 직렬화 의도를 밝히기 위해 인터페이스를 적용하는 것 (Marker Interface)
```

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class Person implements Serializable{ // 직렬화하겠다는 의도 표시
	String name;		
	String job;
	
	public Person(String name, String job) {
		this.name = name;
		this.job = job;
	}
	
	@Override
	public String toString() {
		return name +", "+job;
	}
}
public class SerializationTest {

	public static void main(String[] args) throws ClassNotFoundException {
		
		Person personLee = new Person("이순신", "프로그래머");
		Person personHa	= new Person("하륜", "영업사원");
		// 보내기
		try(FileOutputStream fos = new FileOutputStream("serial.out");
			ObjectOutputStream oos = new ObjectOutputStream(fos)){
			
			oos.writeObject(personLee);
			oos.writeObject(personHa);
			
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		
		// 받기
		try(FileInputStream fis = new FileInputStream("serial.out");
			ObjectInputStream ois = new ObjectInputStream(fis)){
			
			Person person1 =(Person)ois.readObject();
			Person person2 =(Person)ois.readObject();
			
			System.out.println(person1);
			System.out.println(person2);
			
		}catch(IOException e) {
			e.printStackTrace();
		}
		
	}

}
```

## 6. Decorator pattern

* 장식과 실제 내용물을 동일시

```
    - decorator와 component는 동일한 것이 아님
```

* 객체에 동적으로 책임을 추가

* 상속을 사용하지 않고 기능의 유연한 확장이 가능한 패턴

* 전체가 아닌 개별적인 객체에 새로운 기능을 추가 할수 있음.

* 자바의 입출력 스트림은 decorator pattern 임.

```
    - 데코레이터는 다른 데코레이터나 또는 컴포턴트를 포함해야 함.
    - 기반 스트림 클래스가 직접 읽고 쓸수 있음. 
    - 보조 스트림은 추가적인 기능 제공
```
### 객체 협력 (collaborations)

* Component : 동적으로 추가할 서비스를 가질 수 있는 객체

* ConcreteComponent : 추가적인 서비스가 필요한 실체 객체

* Decorator : Component의 참조자를 관리하면서 Component에 정의된  
  인터페이스를 만족하도록 정의

* ConcreteDecorator : 새롭게 추가되는 서비스를 실제 구현한 클래스로 구현  

![alt](\assets\images\post\java\decorator.png)

```java
/*
 *	아메리카노 
 *	카페 라떼 = 아메리카노 + 우유
 *	모카 커피 = 아메리카노 + 우유 + 모카시럽
 *	크림 올라간 모카 커피 = 아메리카노 + 우유 + 모카시럽 + whipping cream
 *
 *  => 커피 : 컴포넌트
 *     우유, 모카시럽, whipping cream : 데코레이터 
 */

public abstract class Coffee {
	
	public abstract void brewing();
}
```

```java
public abstract class Decorator extends Coffee{

	Coffee coffee;
	
	public Decorator(Coffee coffee) {
		this.coffee=coffee;
	}
	
	@Override
	public void brewing() {
		coffee.brewing();
	}
}
```

```java
public class Latte extends Decorator {
	
	public Latte(Coffee coffee) {
		super(coffee);
	}
	@Override
	public void brewing() {
		super.brewing();
		System.out.println("Adding milk");
	}
	
}
```

```java
public class Mocha extends Decorator{

	public Mocha(Coffee coffee) {
		super(coffee);
	}
	
	@Override
	public void brewing() {
		super.brewing();
		System.out.println("adding Mocha Syrup");
	}
}
```

```java
public class WhippedCream extends Decorator {

	public WhippedCream(Coffee coffee) {
		super(coffee);
		
	}
	@Override
	public void brewing() {
		super.brewing();
		System.out.println("Adding Mocha WhippedCream");
	}
	
}
```

```java
public class AAmericano extends Coffee{

	@Override
	public void brewing() {
		System.out.println("AAmericano Coffee");
	}
	
	
}
```

```java
public class BAmericano extends Coffee {

	@Override
	public void brewing() {
		System.out.println("BAmericano Coffee");
	}

}
```

```java
public class CoffeeTest {

	public static void main(String[] args) {
		Coffee aamericano = new AAmericano();
		aamericano.brewing(); // AAmericano Coffee
		
		Coffee latte = new Latte(new AAmericano());
		latte.brewing();// AAmericano Coffee Adding milk
		
		Coffee mocha = new Mocha(new Latte(new AAmericano()));
		mocha.brewing(); // ... adding Mocha Syrup
		
		Coffee mocha2 = new Mocha(new Latte(new BAmericano()));
		mocha2.brewing(); // BAmericaon Coffe ~~~
		
		
		
		
	}

}
```

### 결론
* 단순한 상속보다 설계의 융통성을 증대
* Decorator의 조합을 통해 새로운 서비스를 지속적으로 추가할 수 있다.
* 필요없는 경우 Decorator를 삭제할 수 있다.
* Decorator와 실제 컴포넌트는 동일한 것이 아님.
* 작은 규모의 객체들이 많이 생성될 수 있음
* 자바의 I/O 스트림 클래스는 Decorator 패턴임.

