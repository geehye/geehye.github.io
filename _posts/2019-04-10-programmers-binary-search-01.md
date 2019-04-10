---
title: "BinarySearch 프로그래머스 알고리즘 자바 이분탐색 '징검다리' 문제풀이"
date: 2019-04-10
layout:
tags: programmers
---


## Problem
출발지점부터 distance만큼 떨어진 곳에 도착지점이 있습니다. 그리고 그사이에는 바위들이 놓여있습니다. 바위 중 몇 개를 제거하려고 합니다.
예를 들어, 도착지점이 25만큼 떨어져 있고, 바위가 [2, 14, 11, 21, 17] 지점에 놓여있을 때 바위 2개를 제거하면 출발지점, 도착지점, 바위 간의 거리가 아래와 같습니다.

|제거한 바위의 위치|각 바위 사이의 거리|거리의 최솟값|
|----------------|------------------|------------|
|[21, 17]	       |[2, 9, 3, 11]	    |2           |
|[2, 21]	       |[11, 3, 3, 8]	    |3           |
|[2, 11]	       |[14, 3, 4, 4]	    | 3          |
|[11, 21]	       |[2, 12, 3, 8]	    | 2          |
|[2, 14]	       |[11, 6, 4, 4]	    | 4          |

위에서 구한 거리의 최솟값 중에 가장 큰 값은 4입니다.
출발지점부터 도착지점까지의 거리 distance, 바위들이 있는 위치를 담은 배열 rocks, 제거할 바위의 수 n이 매개변수로 주어질 때, 바위를 n개 제거한 뒤 각 지점 사이의 거리의 최솟값 중에 가장 큰 값을 return 하도록 solution 함수를 작성해주세요.

- 도착지점까지의 거리 distance는 1 이상 1,000,000,000 이하입니다.
- 바위는 1개 이상 50,000개 이하가 있습니다.
- n 은 1 이상 바위의 개수 이하입니다.


## Solution
무엇을 이분탐색할 것인가, 에서 나는 이전에 백준에서 풀었던 것처럼 징검다리 사이의 거리를 선택했다.
- 우선 입력받은 징검다리를 오름차순으로 정렬한다.
- 거리의 최소값은 1이므로 left는 1로 저장하고, right는 입력받은 도착지점 distance를 저장한다.
- 원래 생각한 것은 현재 지점과 이전 지점 사이의 거리가 mid보다 크면 제거한 바위의 개수 cnt 를 증가시켰다. 그렇게 하면, 바위를 제거하고 나면 이전 지점과의 거리가 늘어나고 늘어나고 또 늘어나서 계속 제거하는 꼴이 된다.
그래서 현재 지점과 이전 지점 사이의 거리가 mid보다 작거나 같으면 제거한다는 컨셉으로 갔다.
- 만약 제거되지 않았다면 현재 지점과 이전 지점 사이의 거리의 최솟값을 구한다.
- 루프를 다 돈 후, 마지막 바위에서 도착지점 distance까지의 거리를 구하기 위해 if-else문을 추가로 작성해 주었다.
- 이렇게 구한 거리의 최솟값 중 최대값을 구한다. 출력한다. 끝!


## Code
```java
import java.util.Arrays;
class Solution {
    public int solution(int distance, int[] rocks, int n) {
        int max = 0;
        Arrays.sort(rocks);
        
        int left = 1, right = distance, mid = 0;
        while(left <= right) {
        	int cnt = 0, prev = 0, min = distance;
        	mid = (left + right) / 2;
        	
        	for(int i = 0; i < rocks.length; i++) {
        		if(rocks[i] - prev <= mid ) cnt++;
        		else {
        			min = Math.min(min, rocks[i] - prev);
        			prev = rocks[i];
        		}
        	}
        	if(distance - prev <= mid) cnt++;
        	else min = Math.min(min, distance - prev);
        	
        	if(cnt <= n) {
        		max = Math.max(max, min);
        		left = mid + 1;
        	}else right = mid - 1;
        }
        
        return max;
    }
}
```
