---
title: "DFS Programmers 프로그래머스 알고리즘 '타겟 넘버' 문제풀이"
date: 2019-03-12
layout:
tags: programmers
---

## Problem
n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.


## Solution
numbers 배열의 처음부터 끝까지 가야하므로 DFS를 적용한다. 인덱스 값을 1씩 증가하면서, 음의 정수 또는 양의 정수 중 택하여 그 합을 구한다. 합이 타겟과 동일하면 경우의 수 1가지가 추가된다.

## Code
<pre>
class Solution {
    public int dfs(int[] numbers, int target, int idx, int sum) {
		if(idx == numbers.length)
			return sum == target ? 1 : 0;
		
		return dfs(numbers, target, idx + 1, sum + numbers[idx]) 
				+ dfs(numbers, target, idx + 1, sum - numbers[idx]);
	}
	
	public int solution(int[] numbers, int target) {
        return new Solution().dfs(numbers, target, 0, 0);
    }
}
