---
title: "DynamicProgramming 프로그래머스 알고리즘 자바 '등굣길' 문제풀이"
date: 2019-04-10
layout:
tags: programmers
---

## Problem
계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.
아래 그림은 m = 4, n = 3 인 경우입니다.
<br>
가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.
격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어질 때, 학교에서 집까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

- 격자의 크기 M, N은 1 이상 100 이하인 자연수입니다.
- 물에 잠긴 지역은 0개 이상 10개 이하입니다.
- 집과 학교는 물에 잠기지 않았습니다.


## Solution
물에 잠긴 부분을 어떻게 처리할까 고민하다가 dp 배열에 -1로 저장하기로 하였다. 이때 주의해야 할 점은 보통 arr[가로][세로] 로 표현하는데, puddles에 들어있는 값은 (세로, 가로) 형태이다.
따라서 dp[puddles[i]<strong>[1]</strong>][puddles[i]<strong>[0]</strong>] 으로 저장해야 한다.
- 내가 있는 곳에 웅덩이가 있으면 안 되니까 dp가 -1이면 건너뛴다.
- 이전에 있던 곳이 웅덩이가 있으면 안 되니까 dp가 -1이면 건너뛴다.
- 이전에 있던 곳이 범위를 벗어나면 안 되니까 가로값, 세로값이 0과 같으면 건너뛴다. (가장 가까운 거리만 계산해야 하므로 이동은 하향 또는 우향만 가능하다.)
- 이미 %연산을 한 값을 저장하였지만, 반환할 때도 %연산을 하지 않으면 효율성에서 실패한다.



## Code
```java
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        int[][] dp = new int[n+1][m+1];
        
        for(int i = 0; i < puddles.length; i++) dp[puddles[i][1]][puddles[i][0]] = -1;
       
        dp[1][1] = 1;
        for(int i = 1; i <= n; i++) {
        	for(int j = 1; j <= m; j++) {
        		if(dp[i][j] == -1) continue;
        		if(i-1 > 0 && dp[i-1][j] != -1) dp[i][j] += dp[i-1][j]%1000000007;
        		if(j-1 > 0 && dp[i][j-1] != -1) dp[i][j] += dp[i][j-1]%1000000007;
        	}
        }               
        return dp[n][m]%1000000007;
    }
}
```
