---
title: Java 30. 스레드
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is Thread
tag : java language
article_tag1: java IO
article_section: java IO
meta_keywords: java,java languagem, java thread
last_modified_at: '2022-04-15 18:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Thread
=======

## 1. Thread의 이해

```  
    Process : 실행중인 프로그램. 
    운영체제 (OS)
    하드웨어 (CPU,RAM)
```

### 1) Process

* 프로그램이 실행되면 OS로 부터 메모리를 할당받아 프로세스 상태가 됨.

* 프로세스는 자신만의 자원을 가짐.

```
    - 여러 프로세스가 동시에 실행되더라도 자신만의 메모리를 사용 => 서로 독립적
```
![alt](\assets\images\post\java\thread\1.process.png)

### 2) Thread

* 하나의 프로세스는 하나 이상의 thread를 가지게 되고, 실제 작업(task)을   
  수행하는 단위는 thread 임.

![alt](\assets\images\post\java\thread\2.thread.png)

### 3) 멀티태스킹 (Multi-tasking)

* 두 가지 이상의 작업(task)을 동시에 처리하는 것.

```java
public class CurrentThread {

	public static void main(String[] args) {
		
		String name = Thread.currentThread().getName();
		System.out.println("현재 스레드 이름 : "+name); //main
	}
}
```

## 2.스레드 생성과 실행

### 1) Thread 클래스를 상속받아 만들기

* run() 메서드 오버라이딩

```java
class MyThread extends Thread{
	@Override
	public void run() {
		int sum = 0;
		for(int i=0;i<10;i++) 
			sum += i;
		
		// 스레드명 : 일련번호가 붙여진 이름이 반환됨
		String name = Thread.currentThread().getName();
		System.out.println(name+" : "+sum);
	}
}

public class ThreadClass {

	public static void main(String[] args) {
		MyThread myThread = new MyThread();
		
		/*
		 *  스레드의 run()메서드를 바로 호출하지 않고,
		 *  스레드의 start()메서드를 호출해야 run() 메서드가 실행됨.
		 */
		myThread.start(); // Thread-0 : 45
		System.out.println("main 메서드의 스레디 이름 : "
		                      +Thread.currentThread().getName());
	}

}
```

### 2) Runnable 인터페이스 구현하기

```java
class MyThread2 implements Runnable{

	@Override
	public void run() {
		int sum = 0;
		for(int i=0; i<10; i++) {
			sum += i;
		}
		String name = Thread.currentThread().getName();
		System.out.println(name +" : "+sum);
	}
	
}

public class RunnableInterface {

	public static void main(String[] args) {
		Thread myThread = new Thread(new MyThread2());
		myThread.start(); // Thread-0 : 45
		
	}

}
```

### 3) Anonymous 구현

```java
public class AnonymousThread {

	public static void main(String[] args) {
		
		Runnable task = new Runnable() {
			
			@Override
			public void run() {
				try {
					Thread.sleep(3000);	// 3초후 실행 
				} catch (InterruptedException e) {
					e.printStackTrace();
					throw new RuntimeException(e);	// 일부러 예외발생!
				}
				int sum=0;
				for(int i=0;i<10;i++)
					sum+=i;
				String name = Thread.currentThread().getName();
				System.out.println(name + " : "+ sum);
			}
		};
		Thread thread = new Thread(task);
		thread.start(); // 3초후 Thread-0 : 45
	}

}
```

### 4) 람다식 구현

```java
public class RambdaThread {

	public static void main(String[] args) {
		
		Runnable task = () -> {			// Runnable 참조변수에 람다식을 대입
			try {
				Thread.sleep(3000);	// 3초후 실행 
			} catch (InterruptedException e) {
				e.printStackTrace();
				throw new RuntimeException(e);	// 일부러 예외발생!
			}
			int sum=0;
			for(int i=0;i<10;i++)
				sum+=i;
			String name = Thread.currentThread().getName();
			System.out.println(name + " : "+ sum);
		};
		
		Thread thread = new Thread(task);
		thread.start(); // Thread-0 : 45
	}

}
```

## 3. Multi-threading (여러 개의 스레드 동시에 실행)

* 여러 thread가 동시에 수행되는 프로그래밍.

* 여러 작업 (task)이 동시에 실행되는 효과.
* thread는 각각 자신만의 작업 공간을 가짐 **(context)**
* 각 thread 사이에서 공유하는 자원이 있을 수 있다. 

```
    - 자바에서 static 
```

* 여러 thread가 자원을 공유하여 작업이 수행되는 경우 서로 자원을  
  차지하려는 **race condition** 이 발생할 수 있다.

* 이렇게 여러 thread가 공유하는 자원 중 경쟁이 발생하는 부분을 **critical section** 이라고 함.
* **critical section**에 대한 **동기화(일종의 순차적 수행)**를 구현하지 않으면 오류가 발생할 수 있음.

![alt](\assets\images\post\java\thread\3.mutil.png)

```java
public class MultiThreadTest {

	public static void main(String[] args) {
		
		Runnable task1 = () -> {
			// 20미만 짝수 출력
			for(int i=0;i<20;i=i+2) {
				System.out.print(i+" ");
				
				try {
					Thread.sleep(1000);	// 1초 쉬었다가 반복
				} catch (InterruptedException e) {
				} 
			}
		};
		
		Runnable task2 = () -> {
			// 10미만 수 출력
			for(int i=9;i>0;i--) {
				System.out.print("("+ i +")");
				try {
					Thread.sleep(500); // 0.5초 쉬었다가 반복
				} catch (InterruptedException e) {
					
				} 	
			}
		};
		Thread thread1 = new Thread(task1);
		Thread thread2 = new Thread(task2);
		thread1.start();
		thread2.start();
		// 0 (9)(8)2 (7)(6)4 (5)(4)6 (3)(2)8 (1)10 12 14 16 18 
	}

}
```

## 4. Thread 우선순위

```java
 Thread.MIN_PRIORITY(-1) ~ Thread.MAX_PRIORITY(-10)
```

* 디폴트 우선 순위 : **Thread.NORM_PRIORITY(-5)**

* 우선 순위가 높은 Thread가 CPU의 배분을 받을 확률이 높다.
* setPriority() / getPriority()

```java
class PriorityThread extends Thread{
	
	@Override
	public void run() {
		int sum = 0;
		Thread thread = Thread.currentThread();
		System.out.println(thread + "start");
		
		for(int i=0; i<=1000000;i++) {
			sum += i;
		}
		System.out.println(thread.getPriority()+" 우선순위 스레드 end"); 
	}
}

public class PriorityTest {

	public static void main(String[] args) {
		
		int i;
		for(i=Thread.MIN_PRIORITY;i<=Thread.MAX_PRIORITY;i++) {
			PriorityThread pThread = new PriorityThread();
			pThread.setPriority(i);
			pThread.start();
		}
	}

}
```

```java
public class PriorityTest2 {

	public static void main(String[] args) {
		
		PriorityThread2 pThread1 = new PriorityThread2();
		PriorityThread2 pThread2 = new PriorityThread2();
		PriorityThread2 pThread3 = new PriorityThread2();

		pThread1.setPriority(Thread.MIN_PRIORITY);
		pThread2.setPriority(Thread.NORM_PRIORITY);
		pThread3.setPriority(Thread.MAX_PRIORITY);
		
		pThread1.start();
		pThread2.start();
		pThread3.start();
	}

}
```

## 5. Thread status
* Runnable

* Run
* Not Runnable
* Dead

![alt](\assets\images\post\java\thread\4.thread status.png)
## 6. join()

* 동시에 두개 이상의 Thread가 실행 될 때 Thread의 결과를 참조하여 실행해야 하는 경우

```
    - join() 함수를 사용
```

* join() 함수를 호출한 Thread가 not-Runnable 상태가 됨.
* 다른 Thread의 수행이 끝나면 runnable 상태로 돌아온다.

```java
// 1부터 50까지, 51부터 100까지 합을 각각 구하는 두개의 Thread.
public class JoinTest extends Thread{
	
	int start;
	int end;
	int total;
	
	public JoinTest(int start,int end) {
		this.start=start;
		this.end=end;
	}
	@Override
	public void run() {
		int i;
		for(i = start; i<=end;i++) {
			total += i;
		}
	}
		
	public static void main(String[] args) {
		System.out.println(Thread.currentThread() +" start");
		JoinTest jTest1 = new JoinTest(1, 50);
		JoinTest jTest2 = new JoinTest(51,100);
		
		jTest1.start();
		jTest2.start();
		
		try {
			jTest1.join();
			jTest2.join();
		} catch (InterruptedException e) {
			System.out.println(e);
		}
		
		int lastTotal = jTest1.total + jTest2.total;
		System.out.println("jTest1.total ="+jTest1.total);
		System.out.println("jTest2.total ="+jTest2.total);
		System.out.println("lastTotal ="+lastTotal);
		System.out.println(Thread.currentThread() +" end");

	}

}
```

## 7. Thread 종료하기

* Thread를 종료할 때 사용함.

* 무한 반복의 경우 while(flag)의 flag 변수값을 false로 바꾸어 종료를 시킴

```java
public class TeminateThreadTest extends Thread {

	private boolean flag = false;

	public void setFlag(boolean flag) {
		this.flag = flag;
	}

	public TeminateThreadTest(String name) {
		super(name);
	}

	@Override
	public void run() {
		while (!flag) {
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		System.out.println(getName() + "thread end");
	}

	public static void main(String[] args) throws IOException {
		
		TeminateThreadTest threadA = new TeminateThreadTest("A");
		TeminateThreadTest threadB = new TeminateThreadTest("B");
		TeminateThreadTest threadC = new TeminateThreadTest("C");
		
		threadA.start();
		threadB.start();
		threadC.start();
		
		System.out.print("종료시킬 스레드 이름 입력(A, B, C, M)");
		int in;
		while(true) {
			in = System.in.read();
            System.in.read(); 		// \r
			System.in.read(); 		// \n
			if(in == 'A') {
				threadA.setFlag(true);	// true넣으면 정지
			}
			else if(in == 'B') {
				threadB.setFlag(true);
			}
			else if(in == 'C') {
				threadC.setFlag(true);
			}
			else if(in =='M') {
				threadA.setFlag(true);
				threadB.setFlag(true);
				threadC.setFlag(true);
				break;
			}
			else {
				System.out.println("다시 입력하세요.");
			}
		}
		System.out.println("main thread end");
	}

}
```


