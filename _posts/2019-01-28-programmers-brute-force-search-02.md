---
title: "BruteForceSearch 프로그래머스 '소수 찾기' 알고리즘 문제풀이"
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


```java
import java.util.List;
import java.util.ArrayList;
import java.util.stream.Collectors;

class Solution {
    static List<Integer> numList = new ArrayList<Integer>();
    
    public int solution(String numbers) {
        int tmp = 0;
        
        makePrimeNum("", numbers);
        
        numList = numList.stream().distinct().collect(Collectors.toList()); // 중복값 제거
        numList.removeIf(a -> a == 1 | a == 0); // 0과 1은 소수가 아니다.
        
        for (int i = 0; i < numList.size(); i++) {
            tmp = numList.get(i);
            
            for (int j = 2; j < tmp; j++) {
                /* 자기보다 작은 수로 나눠서 나머지가 0이면 약수가 존재하므로 소수가 아님 */
                if (tmp % j == 0) {
                    numList.remove(i--); // 삭제하고나면, 리스트 사이즈 줄어드므로 인덱스 조정 필요
                    break;
                }
            }
        }

        return numList.size();
    }
    
    public void makePrimeNum(String str, String numStr) {
        if (numStr.length() == 0) {
            if (!str.equals(""))
                numList.add(Integer.parseInt(str));
        }
        else
        {
            for (int i = 0; i < numStr.length(); i++) {
                makePrimeNum(str + numStr.charAt(i), numStr.substring(0, i) + numStr.substring(i + 1, numStr.length()));
            }
            
            makePrimeNum(str, "");
        }
    }
}
```
