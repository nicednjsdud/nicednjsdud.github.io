---
title: Java 22. 자료구조
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is Data Structure?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, data structure
last_modified_at: '2022-04-05 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

자료구조
=========

## 자료구조란? (Data Structure)
* 프로그램에서 사용할 많은 데이터를 메모리 상에서 관리하는 여러 구현 방법들.
* 효율적인 자료구조가 성능 좋은 알고리즘 기반이 됨.
* 자료의 효율적인 관리는 프로그램의 수행속도와 밀접한 관련이 있음.


## 한 줄로 자료를 관리하기 (선형 자료구조)

### 배열(ArrayList)
- 자료의 물리적 위치와 논리적 위치가 같음.
- 동일한 데이터 타입을 순서에 따라 관리하는 자료구조
- 요소의 추가와 제거시 다른 요소들의 이동이 필요함
- 장점 : i번째 요소를 찾는 인덱스 연산이 빠름
- jdk 클래스 : ArrayList, Vector

### 연결 리스트 (LinkedList)
- 자료가 추가될 때 자료는 링크로 연결됨.
- 자료는 링크로 연결됨.

```
    - 동일한 데이터 타입을 순서에 따라 관리하는 자료 구조
    - 자료를 저장하는 노드에는 자료와 다음 요소를 가르키는 링크(포인트)가 있음.
```

- 자료의 물리적 위치와 논리적 위치가 다를 수 있음. 
- 연결 리스트의 i번째 요소를 찾는데 걸리는 시간은 요소의 개수에 비례
- jdk 클래스 : LinkedList
- 리스트에 자료 추가하기
- 리스트에 자료 삭제하기

* Node

```java
public class MyListNode {
	
	private String data;				// 자료
	public MyListNode next;				// 다음 노드를 가리키는 링크
	
	public MyListNode() {				// 둘다 null 값
		data=null;
		next=null;
	}
	
	public MyListNode(String data) {	// 데이터는 o 다음노드링크는 null
		this.data=data;
		this.next=null;
	}
	public MyListNode(String data,MyListNode link) {	
		this.data=data;
		this.next=link;
	}
	
	public String getData() {
		return data;
	}	
}
```

* Linkedlist 구현

```java
public class MyLinkedList {
	
	private MyListNode head;
	int count;
	
	public MyLinkedList() {
		head = null;
		count = 0;
	}
	
	public MyListNode addElement(String data) {		// 추가()
		
		MyListNode newNode;
		if(head == null) {					// 맨 처음일때
			newNode=new MyListNode(data);
			head = newNode;
		}
		else {
			newNode=new MyListNode(data);
			MyListNode temp = head;
			while(temp.next!=null) {		// 맨 뒤로 가서 null인 노드
				temp = temp.next;
			}
			temp.next = newNode;
		}
		count++;
		
		return newNode;
	}
	public boolean isEmpty() {
		if(head==null) {
			return true;
		}
		return false;
	}
	public MyListNode insertElement(int position,String data) {	
              //중간에 노드가 추가되는 경우()
		int i;
		MyListNode tempNode = head;
		MyListNode newNode = new MyListNode(data);				//추가할 노드
		
		if(position<0 || position>count) {
			System.out.println("추가 할 위치 오류임. 현재 리스트의 개수는 "+count+"개 입니다.");
			return null;
		}
		if(position == 0) {
			newNode.next=head;
			head=newNode;
		}
		else {						//중간에 추가되는 경우
			MyListNode preNode=null;//추가할려는곳 앞에노드
			for(i=0;i<position;i++) {
				preNode = tempNode;
				tempNode =tempNode.next;
			}
			newNode.next=preNode.next;
			preNode.next=newNode;
		}
		count++;
		return newNode;	
	}
	//preNode 찾아서삭제처리하면 된다.
	
	public MyListNode removeElement(int position) {					// 요소 삭제()
		int i;
		MyListNode tempNode=head;
		if(position<0 || position>count) {
			System.out.println("삭제 할 위치 오류임. 현재 리스트의 개수는 "+count+"개 입니다.");
			return null;
		}
		if(position==0) {			// 맨 앞에있는 경우의 삭제하는 케이스
			head = tempNode.next;
		}
		else {
			MyListNode preNode=null;
			for(i=0;i<position;i++) {
				preNode=tempNode;
				tempNode=tempNode.next;
			}
			preNode.next=tempNode.next;
		}
		count--;
		System.out.println(position + "번째 항목 삭제되었습니다.");
		return tempNode;
	}
	
	public void printAll() {					// 전체 출력()
		if(count==0) {
			System.out.println("출력할 내용이 없습니다.");
			return;
		}
		
		MyListNode temp = head;
		while(temp!=null) {
			System.out.print(temp.getData());
			temp=temp.next;
			if(temp!=null) {
				System.out.print(" -> ");
			}
		}
		System.out.println("");
	}
	
	public void removeAll() {						// 전체 삭제()
		head=null;
		count =0;
	}
	
	public int getSize() {							// size()
		return count;
	}
	public String getElement(int position) {
		int i;
		MyListNode tempNode = head;
		if(position>=count) {
			System.out.println("검색 위치 오류임. 현재리스크의 개수는"+count+"입니다.");
			return new String("error");
		}
		if(position ==0) {
			return head.getData();
		}
		for(i=0;i<position;i++) {
			tempNode=tempNode.next;
		}
		return tempNode.getData();
		
	}
}
```


### 스택(Stack)
- 가장 나중에 입력된 자료가 가장 먼저 출력되는 자료구조 (LIFO)

```
    - 후입선출
    - 택배 상자가 쌓여있는 모양
```

- 맨 마지막 위치(top)에서만 자료를 추가,삭제됨 (중간의 자료를 꺼낼 수 없다.)    
- 가장 최근의 자료를 찾아오거나 게임에서 히스토리 유지하고 이를 무를 때 사용함
- jdk 클래스 : Stack   

* Stack

```java
public class MyArrayStack {
	
	int top;
	MyArrayList arrayList;
	
	public MyArrayStack() {
		top=0;
		arrayList=new MyArrayList();
	}
	public MyArrayStack(int size) {
		arrayList=new MyArrayList(size);
	}
	
	public void push(int data) {					//push()
		if(isFull()) {
			System.out.println("Stack is full");
			return;
		}
			arrayList.addElement(data);
			top++;
	}
		
	public boolean isFull() {						//isFull()
		if(top== arrayList.ARRAY_SIZE) {
			return true;
		}
		else {
			return false;
		}
		
	}
	
	public void printAll() {
		arrayList.printAll();
	}
	public int pop() {
		if(top==0) {
			System.out.println("stack is empty");
			return arrayList.ERROR_NUM;
		}
		return arrayList.removeElement(top-1);
	}
	public int getSize() {
		return top-1;
	}
}
```

### 큐(Queue)
- 맨 앞(front)에서 자료를 꺼내거나 삭제하고, 맨 뒤(rear)에서 자료를 추가함.
- First In First Out (선입선출) 구조
- 일상생활에서 일렬로 줄서 있는 모양
- 순차적으로 입력된 자료를 순서대로 처리하는데 많이 사용되는 자료구조
- Queue
       
```java
interface IQueue{
	void enQueue(String data);
	void deQueue();
	void printAll();
	
}

public class MyListQueue extends MyLinkedList implements IQueue {
	
	private MyListNode front;
	private MyListNode rear;
	private int tail;
	public MyListQueue() {
		front=null;
		rear=null;
		tail=0;
	}
	
	@Override
	public void enQueue(String data) {
		MyListNode newNode;
		if(isEmpty()) {
			newNode = addElement(data);
			front = newNode;
			rear= newNode;
		}
		else {								// 맨뒤에 들어가는 경우
			newNode = addElement(data);
			rear=newNode;
		}
		tail++;
		System.out.println(newNode.getData()+" 추가됨");
	}
	

	@Override
	public void deQueue() {
			if(isEmpty()) {
				return;
			}
			MyListNode tempNode=front;
			front = tempNode.next;
		}
	public void removeAll() {
		front = null;
		rear = null;
		tail=0;
	}
	

	@Override
	public void printAll() {
		if(isEmpty()) {
			System.out.println("Queue is Empty!");
			return;
		}
		MyListNode temp = front;
		while(temp!=null) {
			System.out.print(temp.getData() + ",");
			temp=temp.next;
		}
		System.out.println();
	}

}
```
