---
title: "DynamicProgramming 프로그래머스 알고리즘 자바 '정수 삼각형' 문제풀이"
date: 2019-04-10
layout:
tags: programmers
---

## Problem
[[7], [3, 8], [8, 1, 0], [2, 7, 4, 4], [4, 5, 2, 6, 5]]

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.
삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

## Solution
앞에서 구한 값을 계속 축적하는 문제이므로 dp로 문제를 풀었다. dfs로 풀릴 것 같기도 한데 dp가 더 간단하게 떠올라서 그렇게 했다.
- 삼각형의 가장 왼쪽 값과 가장 오른쪽 값은 구하는 방법이 다르다. 중간 값들은 대각선 상향 방향으로 좌, 우의 값 중 최대값을 선택해 지금의 값과 더한 값을 저장하면 된다.
삼각형의 왼쪽 값은 대각선 상향 좌측 방향으로 값이 없기때문에 우측 방향만 가져와야 하며, 오른쪽 값은 좌측 방향만 가져와야 한다.
- 가장 마지막 줄의 값들 중 최대값을 구하면 된다.


## Code
```java
class Solution {
    public int solution(int[][] triangle) {
        int leng = triangle.length;
		    int answer = 0;
        
        int[][] dp = new int[leng][leng]; dp[0][0] = triangle[0][0];
        for(int i = 1; i < leng; i++) {
        	dp[i][0] = dp[i-1][0] + triangle[i][0];
        	for(int j = 1; j < i; j++)
        		dp[i][j] = Math.max(dp[i-1][j-1], dp[i-1][j]) + triangle[i][j];
        	dp[i][i] = dp[i-1][i-1] + triangle[i][i];
        }
        
        for(int i = 0; i < leng; i++) answer = Math.max(answer, dp[leng-1][i]);
        return answer;
    }
}
```
