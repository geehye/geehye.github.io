---
title: "ETC. 프로그래머스 자바 '배달' 문제풀이"
date: 2021-08-08
layout:
tags: programmers
---


## Problem
N개의 마을로 이루어진 나라가 있습니다. 이 나라의 각 마을에는 1부터 N까지의 번호가 각각 하나씩 부여되어 있습니다.
각 마을은 양방향으로 통행할 수 있는 도로로 연결되어 있는데, 서로 다른 마을 간에 이동할 때는 이 도로를 지나야 합니다. 도로를 지날 때 걸리는 시간은 도로별로 다릅니다.
현재 1번 마을에 있는 음식점에서 각 마을로 음식 배달을 하려고 합니다. 각 마을로부터 음식 주문을 받으려고 하는데, N개의 마을 중에서 K 시간 이하로 배달이 가능한 마을에서만 주문을 받으려고 합니다.

마을의 개수 N, 각 마을을 연결하는 도로의 정보 road, 음식 배달이 가능한 시간 K가 매개변수로 주어질 때, 음식 주문을 받을 수 있는 마을의 개수를 return 하도록 solution 함수를 완성해주세요.

제한사항
•	마을의 개수 N은 1 이상 50 이하의 자연수입니다.
•	road의 길이(도로 정보의 개수)는 1 이상 2,000 이하입니다.
•	road의 각 원소는 마을을 연결하고 있는 각 도로의 정보를 나타냅니다.
•	road는 길이가 3인 배열이며, 순서대로 (a, b, c)를 나타냅니다.
  o	a, b(1 ≤ a, b ≤ N, a != b)는 도로가 연결하는 두 마을의 번호이며, c(1 ≤ c ≤ 10,000, c는 자연수)는 도로를 지나는데 걸리는 시간입니다.
  o	두 마을 a, b를 연결하는 도로는 여러 개가 있을 수 있습니다.
  o	한 도로의 정보가 여러 번 중복해서 주어지지 않습니다.
•	K는 음식 배달이 가능한 시간을 나타내며, 1 이상 500,000 이하입니다.
•	임의의 두 마을간에 항상 이동 가능한 경로가 존재합니다.
•	1번 마을에 있는 음식점이 K 이하의 시간에 배달이 가능한 마을의 개수를 return 하면 됩니다.


## Solution


## Code
```java
class Solution {
    public int solution(int N, int[][] road, int K) {
        int answer = 0;
        int[][] timeArr = new int[N+1][N+1]; // timeArr[start][end]
        
        /* timeArr 배열 초기화 */
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++)
                if (i == j)
                    timeArr[i][j] = 0; // 출발점과 도착점이 같으면 걸리는 시간은 0
                else
                    timeArr[i][j] = 500000; // 1 <= k >= 500000
        }

        /* 주어진 시간을 출발점-도착점 배열에 정리하기 */
        for (int i = 0; i < road.length; i++)  {
            if (timeArr[road[i][0]][road[i][1]] < road[i][2]) continue; // 이전에 저장된 값이 더 작으면 skip
            
            timeArr[road[i][0]][road[i][1]] = road[i][2];
            timeArr[road[i][1]][road[i][0]] = road[i][2];
        }
        
        /* 출발점에서 도착점까지 걸리는 최소 시간 구하기 */
        for (int x = 1; x <= N; x++) {
            for (int y = 1; y <= N; y++) {
                for (int z = 1; z <= N; z++) {
                    if (y == z) continue; // 출발점과 도착점이 같으면 걸리는 시간은 0 (이미 최솟값)
                    
                    if (timeArr[y][z] > timeArr[y][x] + timeArr[x][z])
                        timeArr[y][z] = timeArr[y][x] + timeArr[x][z];
                }
            }
        }
        
        for (int i = 1; i <= N; i++) {
            if (timeArr[1][i] <= K) answer++;
        }
        
        return answer;
    }
}
```
