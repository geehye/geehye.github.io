---
title: "DFS 프로그래머스 알고리즘 자바 '단어 변환' 문제풀이"
date: 2019-03-13
layout:
tags: programmers
---


## Problem
두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.
  1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
  2. words에 있는 단어로만 변환할 수 있습니다.
예를 들어 begin이 hit, target가 cog, words가 [hot,dot,dog,lot,log,cog]라면 hit -> hot -> dot -> dog -> cog와 같이 4단계를 거쳐 변환할 수 있습니다.
두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

- 각 단어는 알파벳 소문자로만 이루어져 있습니다.
- 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
- words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
- begin과 target은 같지 않습니다.
- 변환할 수 없는 경우에는 0를 return 합니다.



## Solution
문자열처리 때문에 애 먹었다. string.replace(old char, new char)를 사용하면 될 것이라고 생각했는데, 이럴경우 old char에 들어가는 문자가 여러개일 경우 전부 다 바뀌는 문제가 있을 뿐아니라 안 바뀌었다. 왜그랬을까...
그래서 stringbuilder 문자형을 사용하려 했으나, string 타입과는 비교도 못 하고(equals) 이래저래 바꿔야 하는 것이 많아서 그냥 substring을 사용했다.

문자가 하나만 바뀌는 형태로, words 배열에 있는 target 문자와 가까워질 때까지 연산해야 하므로 DFS를 사용했다. 바뀐 문자를 begin으로써 계속 문자열을 비교해 최종 target까지 가면 된다.

재귀함수를 사용할 때마다 return 값 때문에 시간을 많이 잡아먹는데 이번에도 역시 무슨 값을 리턴해야될 지 때문에 오래 걸렸다. 마지막 리턴이 answer가 되야하는 것은 맞는데, 그 전까지 answer를 어떻게 연산해줘야 할 지 고민하다가 우선 현재 단어를 선택했으니 과정 1이 추가되야 해서 answer = 1로 했다.
그리고 이전 과정들을 더해나가야 하므로 answer += dfs()로 마무리 지었다.


## Code
```java
class Solution {
	static boolean[] v;
	
	public int dfs(String begin, String target, String[] words) {
		int answer = 0;
		String dupBegin;
		
		for (int i = 0; i < words.length; i++) {
			if (v[i]) continue;
			
			for (int j = 0; j < begin.length(); j++) {
				dupBegin = begin;
				/* 앞자리부터 한글자씩 쪼개서 한자리씩 글자 변환하기 */
				dupBegin = (j > 0 ? begin.substring(0, j) : "") 
                                + words[i].charAt(j) + (j < begin.length()-1 ? begin.substring(j+1) : "");				
				
				if (dupBegin.equals(target)) return 1;
				if (dupBegin.equals(words[i])) {
					v[i] = true;
					answer = 1;
					answer += dfs(dupBegin, target, words);
				}
			}
		}
		
		return answer;
	}
	
	public int solution(String begin, String target, String[] words) {
		v = new boolean[words.length + 1]; // 방문체크 visit
		
		for (int i = 0; i < words.length; i++) {
		    if (target.equals(words[i]))
			return dfs(begin, target, words);
		}
	
		return 0; // 주어진 words[] 에 target이 존재하지 않으므로 0 반환
	}
}
```
