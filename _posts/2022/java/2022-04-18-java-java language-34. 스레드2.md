---
title: Java 31. 스레드2
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: What is Thread
tag: java language
article_tag1: java IO
article_section: java IO
meta_keywords: java,java languagem, java thread
last_modified_at: "2022-04-15 18:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Thread

## Thread 동기화

### 배경

- 동일한 변수의 값을 증감시키는 두 스레드가 있다고 가정함
- 변수의 값 메모리에 있음.
- 이 변수의 값을 증감 연산을 하려면 CPU로 값을 옮겨와서 값을 증감 시키는  
  연산 수행하고 다시 메모리에 저장

### critical section (semaphore)

- 두 개 이상의 thread가 동시에 접근 하는 경우 문제가 생길수 있기 때문에  
  동시에 접근할 수 없는 영역
- semaphore : 특별한 형태의 시스템 객체. get(), release() 두개의 기능 제공.
- 한 순간 오직 하나의 thread만이 semaphore 얻을 수 있고,  
  나머지 thread들은 대기(blocking) 상태가 됨.
- semaphore를 얻은 thread만이 critical section에 들어갈 수 있음.

![alt](/assets/images/post/java/thread/5.png)

- 동기화 처리 x

```java

class Bank{
	private int money = 10000;


	public int getMoney() {
		return money;
	}


	public void setMoney(int money) {
		this.money = money;
	}


	public void saveMoney(int save) {		// 입금
		int m = this.getMoney();

		try {
			Thread.sleep(3000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		setMoney(m+save);
	}
	public void minusMoney(int minus) {		// 출금
		int m =this.getMoney();

		try {
			Thread.sleep(200);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		if(money<minus) {
			System.out.println("잔액 부족");
			return;
		}
		else {
		setMoney(m-minus);
		}
	}
}

// PersonA - 3000 저장하는 스레드
class PersonA extends Thread{

	@Override
	public void run() {
		System.out.println("start save");
		SyncMain.myBank.saveMoney(3000);
		System.out.println("saveMoney(3000) : "+SyncMain.myBank.getMoney());
	}
}

// PersonB - 1000원 소비하는 스레드
class PersonB extends Thread{

	@Override
	public void run() {
		System.out.println("start minus");
		SyncMain.myBank.minusMoney(1000);
		System.out.println("minusMoney(1000): "+SyncMain.myBank.getMoney());

	}
}

public class SyncMain {


	public static Bank myBank = new Bank();

	public static void main(String[] args) throws InterruptedException {
		PersonA pA = new PersonA();
		pA.start();	// 9000 동기화 처리 안됨.

		Thread.sleep(200);

		PersonB pB = new PersonB();
		pB.start();	// 13000

	}

}
```

### 동기화 (synchronization)

- 두개의 thread가 같은 객체에 접근할 경우, 동시에 접근함으로써 오류가 발생
- 동기화는 임계영역에 접근한 경우 공유자원을 lock하여 다름 thread의 접근을 제어
- 동기화는 잘못 구현하면 **deadlock**에 빠질 수 있음.

### 자바에서는 synchronized 메서드나 synchronized 블럭을 사용.

#### synchronized 메서드

- 객체의 메소드에 synchronized 키워드 사용.
- 현재 이 메서드가 속해있는 객체에 lock을 검.

```java
public synchronized void saveMoney(int save) {		// 입금
		....
	}
public synchronized void minusMoney(int minus) {		// 출금
		....
	}
```

## Thread pool

![alt](/assets/images/post/java/thread/6.png)

### 배경

- 스레드 개수가 많아지면 객체 생성과 소멸, 스케줄링 등에 CPU와 메모리에  
  많은 부하 발생함.
- 웹 서버처럼 소규모의 많은 요청이 들어올 때마다 스레드 생성 및 종료하면  
  오버헤드가 발생함. (OutOfMemoryError 발생)
- 생성과 종료를 반복해 사용하는 스레드를 재사용하고 동시에 실행하는 개수도  
  제한하여 CPU, 메모리에 가해지는 부하를 줄일 필요가 있음.

### 스레드 풀

- 제한된 개수의 스레드를 JVM에 관리하도록 맡기는 방식임.
- 실행할 작업(task)을 스레드 풀로 전달하면 JVM이 스레드 풀의  
  idle thread(유효 스레드) 중 하나를 서택하여 스레드로 실행시킴.

#### 유형

- newSingleThreadExecutor

```
    - 폴안에 하나의 스레드만 생성하고 유지함.
    - 하나의 태스크가 완료된 이후에 다음 태스크가 실행됨.
    - 여러 스레드가 동시에 실행되지 않는다. => 동기화 x
```

```java

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPool {

	// 모든 스레드에서 값을 공유하여 사용
	public static int money = 0;

	public static void main(String[] args) {

		Runnable task1 = () -> {	//스레드에서 시킬 작업 (10000번 동안 더히기함)
			for(int i=0;i<10000;i++) {
				money++;
			}
			String name = Thread.currentThread().getName();
			System.out.println(name+ " : "+money);
		};

		Runnable task2= () -> {		//스레드에서 시킬 작업 (10000번 동안 빼기함)
			for(int i=0;i<10000;i++) {
				money--;
			}
			String name = Thread.currentThread().getName();
			System.out.println(name+ " : "+money);
		};
		// thread pool 생성
		// 하나의 스레드만 전달받아 처리할 수 있음.
		ExecutorService pool = Executors.newSingleThreadExecutor();
		pool.submit(task1);	// thread pool에 작업 전달 => 스레드 풀은 전달된 스레드 실행
		pool.submit(task2); // thread pool에 작업 전달

		System.out.println("End : "+ Thread.currentThread().getName());

		// 마지막 스레드가 종료되면 스레드 풀을 종료시킴
		pool.shutdown();

	}

}
```

![alt](/assets/images/post/java/thread/7.png)

- newFixedThreadPool

```
    - 풀 안에 인수로 전달된 수의 스레드를 생성하고 유지함.
    - 만약 생성된 스레드가 idle 상태에 있어도 스레드를 제거하지 않고 내버려둠.
```

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

// 최대 스레드 수가 2개인 스레드 풀
public class ThreadPool2 {

	public static void main(String[] args) {

		Runnable task1 = () -> {
			String name = Thread.currentThread().getName();
			try {
				Thread.sleep(5000);
			} catch (InterruptedException e) {}
			System.out.println(name + " 5초 후 실행");
		};

		Runnable task2 = () -> {
			String name = Thread.currentThread().getName();
			System.out.println(name+" 바로 실행");
		};

		Runnable task3 = () -> {
			String name = Thread.currentThread().getName();
			try {
				Thread.sleep(2000);
			} catch (InterruptedException e) {}
			System.out.println(name+" 2초 후 실행");
		};

		// 스레드 풀에서 수행할 수 있는 스레드의 총량을 제한
		// 현재 스레드 풀은 동시에 스레드를 두개를 처리할 수 있음.
		ExecutorService pool = Executors.newFixedThreadPool(2);

		// 스레드를 스레드 풀에 전달함.
		// 스레 풀은 전달된 스레드 실행시킴
		pool.submit(task1);
		pool.submit(task2);
		pool.submit(task3);

		// 마지막 스레드가 종료되면 스레드 풀을 종료시킴.
		pool.shutdown();

	}

}
```

![alt](/assets/images/post/java/thread/8.png)
