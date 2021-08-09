---
title: "BruteForceSearch 프로그래머스 '모의고사' 알고리즘 문제풀이"
date: 2019-01-27
layout:
tags: programmers
---

## Problem
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

## Solution
<pre>
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
public class MockExam {
	public int[] solution(int[] answers) {      
        int[] num1 = {1,2,3,4,5};
        int[] num2 = {2,1,2,3,2,4,2,5};
        int[] num3 = {3,3,1,1,2,2,4,4,5,5};
        
        Map<Integer, Integer> map = new HashMap<>();
        map.put(1, 0);
        map.put(2, 0);
        map.put(3, 0);
        
        for(int idx = 0; idx < answers.length; idx++) {
        	if(answers[idx] == num1[idx % num1.length])
        		map.put(1, map.get(1) + 1);
        	if(answers[idx] == num2[idx % num2.length])
        		map.put(2, map.get(2) + 1);
        	if(answers[idx] == num3[idx % num3.length])
        		map.put(3, map.get(3) + 1);
        }       
        
        int max = map.entrySet().stream().max(Map.Entry.comparingByValue()).get().getValue();
        List<Integer> list = new ArrayList<>();
        for(int idx = 1; idx <= 3; idx++) {
        	if(map.get(idx) == max)
        		list.add(idx);
        }
        
        int[] answer = new int[list.size()];
        for(int idx = 0; idx < answer.length; idx++)
        	answer[idx] = list.get(idx);
        
        return list.stream().mapToInt(a -> a.intValue()).toArray();
    }
}    
