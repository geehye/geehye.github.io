---
title: "DFS 프로그래머스 알고리즘 자바 '네트워크' 문제풀이"
date: 2019-03-13
layout:
tags: programmers
---

## Problem
네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.


## Solution
연결된 노드를 끝까지 찾아가는 형태이므로 DFS로 풀어야 한다. 즉, 재귀함수 문제!
2차원 배열 computers가 주어지므로, for문으로 1차원씩 잘라서 재귀함수를 호출했다. (i,i)가 연결되지 않았다는 것은 아직 방문한 적이 없는 것이므로 answer++로 연결의 첫 시작을 알린다.
나머지는 토마토 문제 풀었을 때와 비슷하게 진행했다. 연결된 적이 없을 경우, 지금 노드와 또 연결된 다른 노드를 찾기 위해 재귀함수를 호출하면서 연결을 모두 시켜놓는다!


## Code
<pre>
class Solution {
	static boolean[][] link;
	public void dfs(int[][] computers, int idx, int n) {
		for(int i = 0; i < n; i++) {			
			if(computers[idx][i] == 1 && !link[idx][i]) {
				link[idx][i] = link[i][idx] = true;
				dfs(computers, i, n);
			}
		}
	}
	
	public int solution(int n, int[][] computers) {
		int answer = 0;
		link = new boolean[n][n];
		
        for(int i = 0; i < n; i++) {
        	if(!link[i][i]) {
        		dfs(computers, i, n);
        		answer++;
        	}
        }
		return answer;
    }
}
