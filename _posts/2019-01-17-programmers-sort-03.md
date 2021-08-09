---
title: "Sort 프로그래머스 자바 'H-Index' 문제풀이"
date: 2019-01-17
layout:
tags: programmers
---


## Problem
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h가 이 과학자의 H-Index입니다.
어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

## Solution
문제를 완전 잘못 이해해서 헤맸다. citations의 값이 반드시 h여야 하는 것은 아니다.
중간값 구하는 느낌으로 h를 구하면 된다.


```java
import java.util.Arrays;
import java.util.Collections;
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        
        Arrays.sort(citations);
        
        for (int i = 0; i < citations.length; i++) {
            /*
             * 현재 논문부터 다음 논문까지의 수가 h이상인 것 중 최대값을 구해야 하므로,
             * 현재 논문부터 다음 논문까지의 수가 h이하가 됐을 때의 값이 정답이다.
             */
            if (citations[i] >= citations.length-i) {
                answer = citations.length-i;
                break;
            }	
        }
        return answer;
    }
}
```
