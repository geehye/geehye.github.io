---
title: "DFS 프로그래머스 자바 '여행경로' 문제풀이"
date: 2019-03-13
layout:
tags: programmers
---


## Problem
주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 ICN 공항에서 출발합니다.
항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

- 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
- 주어진 공항 수는 3개 이상 10,000개 이하입니다.
- tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
- 주어진 항공권은 모두 사용해야 합니다.
- 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
- 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.


## Solution
- 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 반환한다고 하여 비교하기 쉽게 String 타입으로 경로를 저장하였다. 구분값은 ","
- 모든 항공권을 사용해야 하므로 visit[] 배열로 해당 항공권을 사용한적이 있는지 확인하였다.
- visit이 모두 true인지 확인하는 것보다 시간을 줄이기 위해 총 몇 장의 항공권을 사용했는지 카운트 변수 cnt를 두었다. 다 사용했을 경우 해당 경로를 list에 저장했다. 만약 항공권을 다 사용하지 못 하고 경로가 종료되는 경우는 list에 저장되지 않는다.
- 지금까지의 경로 외에 중간에 다른 경로를 갈 수 있기 때문에 dfs 호출이 종료되면 visit과 route에서 현재 방문 위치를 빼줘야 한다.
- list를 오름차순으로 정렬한다. (문자가 빠른 순) 


## Code
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
class Solution {
    List<String> list = new ArrayList<>();
	static String route = "";
	static boolean[] visit;
	
	private void dfs(String[][] tickets, String end, int cnt) {
		route += end + ",";
		
		if(cnt == tickets.length) {
			list.add(route); return;
		}
		
		for(int i = 0; i < tickets.length; i++) {
			String s = tickets[i][0], e = tickets[i][1];
			if(s.equals(end) && !visit[i]) {
				visit[i] = true;
				dfs(tickets, e, cnt + 1);
				visit[i] = false; route = route.substring(0, route.length()-4);
			}
		}
	}
	
	public String[] solution(String[][] tickets) {
		for(int i = 0; i < tickets.length; i++) {
			visit = new boolean[tickets.length];
			String start = tickets[i][0], end = tickets[i][1];
			
			if(start.equals("ICN")) {
				route = start + ","; visit[i] = true; 
				dfs(tickets, end, 1);
			}
		}
		
		Collections.sort(list);
		String[] answer = list.get(0).split(",");

		return answer;
	}
}
```
