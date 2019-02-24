---
title: "Greedy '큰 수 만들기' 알고리즘 문제풀이"
date: 2019-02-12
layout:
tags: programmers
---

## Problem
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.
문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.


## Solution
해당 코드는 테스트 케이스 10번을 시간초과로 통과하지 못 했다. 해결하려는 중.


<pre>
public class MakeBigNum {
	public String solution(String number, int k) { // time out (test 10)
        String answer = "";
        int index = 0;
        char max = '0';
       
        for(int i = 0; i < number.length()-k; i++) {
        	for(int j = index; j < k+1+i; j++) {
        		if(max < number.charAt(j)) {
        			max = number.charAt(j);
        			index = j + 1;
        		}
        	}
        	
        	answer += max;
        	max = '0';
        	
        	if(answer.length() == number.length()-k)
        		break;
        }
        
        return answer;
    }
}    
