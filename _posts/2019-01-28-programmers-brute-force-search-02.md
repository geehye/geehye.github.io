---
title: "BruteForceSearch  '소수 찾기' 알고리즘 문제풀이"
date: 2019-01-28
layout:
tags: programmers
---

## Problem
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.
각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- '013'은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.


## Solution
<pre>
import java.util.ArrayList;
import java.util.List;
public class FindPrimeNumber {	
	static List<Integer> list = new ArrayList<Integer>();
	static List<Integer> noDupList = new ArrayList<Integer>();
	
	public int solution(String numbers) {
        permutation("", numbers);
        for(int i = 0; i < list.size(); i++) {
        	if(!noDupList.contains(list.get(i)))
        		noDupList.add(list.get(i));
        }
        
        noDupList.removeIf(a -> a == 1 | a == 0);
        for(int i = 0; i < noDupList.size(); i++) {
        	int tmp = noDupList.get(i); 
        	for(int j = 2; j < tmp; j++)
        		if(tmp % j == 0) {
        			noDupList.remove(i--); // after removing list, index changed.
        			break;
        		}       			
        }                    

        return noDupList.size();
    }
	
	public void permutation(String s, String number) {
		if(number.length() == 0) {
			if(!s.equals(""))
				list.add(Integer.parseInt(s));
		}else {
			for(int i = 0; i < number.length(); i++)
				permutation(s + number.charAt(i), number.substring(0, i) + number.substring(i + 1, number.length()));
			for(int i = 0; i < number.length(); i++)
				permutation(s, number.substring(0, i) + number.substring(i + 1, number.length()));
		}
	}
}  
