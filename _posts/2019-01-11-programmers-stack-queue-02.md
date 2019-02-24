---
title: "Stack/Queue '다리를 지나는 트럭' 알고리즘 문제풀이"
date: 2019-01-11
layout:
tags: programmers
---

## Problem
트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

## Solution
<pre>
import java.util.LinkedList;
import java.util.Queue;
public class Truck {

	public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0;
        int sum = 0;
        Queue<Integer> queue = new LinkedList<>();
        
        // initialise
        for(int i = 0; i < bridge_length; i++)
        	queue.add(0);

        for(int i = 0; i < truck_weights.length; i++) {
        	sum -= queue.poll();

        	if(sum + truck_weights[i] <= weight) { 
        		queue.add(truck_weights[i]);
        		sum += truck_weights[i];
        	}else {
        		queue.add(0);
        		i--;
        	}
        	answer++;
        }
        
        return answer + bridge_length;
    }
} 
</pre>
