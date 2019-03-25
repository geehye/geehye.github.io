---
title: "For job interview, about Data Structure 면접 공부하기-자료"
date: 2019-03-23
layout:
categories:
tags:
collections: data_structure
---


## 1. Linked List vs Array 
1) Array 배열
  - 같은 자료형을 갖는 데이터의 집합으로 연속적인 데이터를 저장한다.
  - 생성할 때 데이터를 저장하는 데 필요한 모든 메모리를 한 번에 확보해 사용할 수 있게 해주므로 프로그램이 실행되는 중간에 배열의 크기를 바꿀 수가 없다.
  - 인덱스 값을 알면 O(1)로 원소에 접근 가능하다.
  - 삽입, 삭제 시 빈 공간을 shift해야 하므로 O(n)이다.
  
2) Linked List 연결 리스트
  - 연속적이지 않는 데이터들을 링크로 서로 연결한다. 
  - 따라서 원하는 데이터를 찾을 시 O(n).
  - 중간 노드의 연결이 끊기면 다음 노드 찾기가 어렵다.
  - 새로운 노드를 삽입하거나 삭제하기 간편하다 O(1).
  - cf. Array List : 저장 순서가 유지되고 중복 허용이 된다. 데이터 저장 공간으로 배열을 사용한다. 인덱스로 접근 시 O(1).


## 2. Stack, Queue, Deque, Heap
1) Stack 스택
  - LIFO (Last In First Out)
  - Usage 용도 : 인터럽트가 발생하여/부프로그램 호출시 복귀 주소 저장할 때, 함수 호출의/재귀 프로그램의 순서 제어, 후위표기법 산술 연산할 때, 컴파일러를 이용한 언어 번역할 때, ...
  - 스택이 꽉 찬 상태를 overflow 오버플로우 라고 한다.
  - 스택이 텅 빈 상태를 underflow 언더플로우 라고 한다.
  
2) Queue 큐
  - FIFO (First In First Out)
  - 두 개의 포인터 front/head, rear/tail이 있다.
  
3) 
