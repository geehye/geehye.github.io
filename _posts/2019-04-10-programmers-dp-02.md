---
title: "DFS 프로그래머스 알고리즘 자바 'N으로 표현' 문제풀이"
date: 2019-04-10
layout:
tags: baekjoon
---

## Problem
아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5) <br>
12 = 55 / 5 + 5 / 5 <br>
12 = (55 + 5) / 5 <br>

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.


## Solution
※ 아직 테스트케이스 1, 6, 7을 해결하지 못 했다.<br>
- N은 영이 아닌 한 자리 양의 정수이다.
- 완전탐색이라고 할 만한 DFS로 풀었다. 모든 가능한 사칙연산을 모두 재귀시켰고, 사용된 숫자의 개수를 cnt로 넘기고 그것이 8보다 크면 종료한다. (최솟값이 8보다 크지 않기 때문이다)
내 코드에서 문제라고 할만한 것은 `55 + 55`를 만들 수 없다. `55 + 5`와 `555 + 5`같이 한쪽만 1의 자리 -> 10의 자리 -> 100의 자리.... 가 된다. 다음에 다시 풀어봐야지. 

## Code
```java
class Solution {
  static int n, num, min = Integer.MAX_VALUE;
	
	private static void dfs(int rslt, int cnt) {
		if(rslt == num) {
			min = Math.min(min, cnt);
			return;
		}
		if(cnt > 8) return;

		dfs(rslt+n, cnt+1);
		dfs(rslt-n, cnt+1);
		dfs(rslt*n, cnt+1);
		dfs(rslt/n, cnt+1);
		dfs(rslt*10+n, cnt+1);
	}
		
	public int solution(int N, int number) {
        n = N; num = number;
        dfs(N, 1);
        return min <= 8? min : -1;
    }
}
```
