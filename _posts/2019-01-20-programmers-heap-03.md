---
title: "Heap '이중우선순위큐' 알고리즘 문제풀이"
date: 2019-01-20
layout:
tags: programmers
---

## Problem
이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

+ I숫자 : 큐에 주어진 숫자를 삽입합니다.
+ D1    : 큐에서 최댓값을 삭제합니다.
+ D-1   : 큐에서 최솟값을 삭제합니다.

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
    - 원소는 “명령어 데이터” 형식으로 주어집니다.최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

## Solution
<pre>
import java.util.Collections;
import java.util.PriorityQueue;
Public class DoublePQ {
    public int[] solution(String[] operations) {
        PriorityQueue<Integer> queue = new PriorityQueue<>(); // min
		PriorityQueue<Integer> rQueue = new PriorityQueue<>(Collections.reverseOrder()); // max
		
		for(int i = 0; i < operations.length; i++) {
			switch(operations[i].charAt(0)) {
			case 'I':
				queue.add(Integer.parseInt(operations[i].substring(1).trim()));
				rQueue.add(Integer.parseInt(operations[i].substring(1).trim()));
				break;
			case 'D':
				if(Integer.parseInt(operations[i].substring(1).trim()) == 1)
					queue.remove(rQueue.poll());
				else
					rQueue.remove(queue.poll());
				break;
			}
		}
		
		int min = (queue.isEmpty())? 0 : queue.poll();
		int max = (rQueue.isEmpty())? 0 : rQueue.poll();
		int[] answer = {max, min};
        
    return answer;
    }
}
