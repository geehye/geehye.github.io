---
title: "Greedy 프로그래머스 '섬 연결하기' 알고리즘 문제풀이"
date: 2019-02-15
layout:
tags: programmers
---

## Problem
n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.
다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

- 섬의 개수 n은 1 이상 100 이하입니다.
- costs의 길이는 ((n-1) * n) / 2이하입니다.
- 임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
- 같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
- 모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
- 연결할 수 없는 섬은 주어지지 않습니다.


## Solution
<pre>
mport java.util.ArrayList;
import java.util.List;
public class LinkIsland {
	public int solution(int n, int[][] costs) { // kruskal algorithm
        int answer = 0;
        int[][] link = new int[n][n];
        int minCost = costs[0][2];
        int minIsland1 = costs[0][0], minIsland2 = costs[0][1];
        
        List<Boolean> visited = new ArrayList<>();
        for(int i = 0; i < n; i++)
        	visited.add(false);       
        
        for(int i = 0; i < costs.length; i++) {
        	link[costs[i][0]][costs[i][1]] = costs[i][2];
        	link[costs[i][1]][costs[i][0]] = costs[i][2];
        	
        	if(costs[i][2] < minCost) { // select first island
        		minCost = costs[i][2];
        		minIsland1 = costs[i][0];
        		minIsland2 = costs[i][1];
        	}
        }      
        
        while(visited.contains(false)){
        	answer += minCost;
            visited.set(minIsland1, true);
            visited.set(minIsland2, true);
            minCost = (int)1e9;

            for(int i = 0; i < n; i++) {
            	if(visited.get(i) == true) {
            		for(int j = 0; j < n; j++) {
            			if(link[i][j] != 0 && visited.get(j) == false && minCost > link[i][j]) {
            				minCost = link[i][j];
            				minIsland1 = i;
            				minIsland2 = j;
            			}
                    }		
            	}
            }
        }
  
        return answer;
    }
}    
