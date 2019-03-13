---
title: "DFS programmers 프로그래머스 자바 '여행경로' 문제풀이"
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
아직 테스트 케이스 1번을 통과하지 못 했다. 왜 얘만 못 할까...ㅠㅠ (추후 해결 예정)
참고로 시작 공항은 항상 'ICN' 인천 공항임을 잊어서는 안 된다! 이것을 해결하면 테스트 케이스 4번 문제를 통과한다.


## Code
<pre>
class Solution {
    	static boolean[] v;
	public String dfs(String[][] tickets, int idx) {
		String from, to, route = "";
		v[idx] = true;
		for(int i = 0; i < tickets.length; i++) {
			if(i == idx) continue;
			from = tickets[i][0]; to = tickets[i][1];
			
			if(tickets[idx][1].equals(tickets[i][0]) && !v[i]) {
				route = "/" + tickets[i][1];
				route += dfs(tickets, i);
			}
		}
		
		return route;
	}
	
	public String[] solution(String[][] tickets) {
	    int n = tickets.length;
		String min = "Z".repeat(30000), route = "";   

		for(int i = 0; i < n; i++) { // start
			if(tickets[i][0].equals("ICN")) {
				v = new boolean[n];
				route = tickets[i][0] + "/" + tickets[i][1];			
				route += dfs(tickets, i);
				
				if(route.length() == 4*n+3 && min.compareTo(route) > 0)
					min = route;
			}
		}		
	    return min.split("/");
	}
}
