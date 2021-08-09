---
title: "Hash 프로그래머스 '완주하지 못한 선수' 알고리즘 문제풀이"
date: 2019-01-23
layout:
tags: programmers
---

## Problem
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

## Solution
<pre>
import java.util.HashMap;
public class RunnerNotFinishing {
	public String solution(String[] participant, String[] completion) {        
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        for(String name : participant)
        	map.put(name, map.getOrDefault(name, 0) + 1);
        for(String name : completion) {
        	if(map.get(name) > 1)
        		map.replace(name, map.get(name) - 1);
        	else
        		map.remove(name);
        }

        return map.keySet().toString().replaceAll("\\[|\\]", "");
    }
}
</pre>
