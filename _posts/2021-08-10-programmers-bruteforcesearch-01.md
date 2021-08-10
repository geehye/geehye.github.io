---
title: "BruteForceSearch 프로그래머스 알고리즘 자바 '문자열 압축' 문제풀이"
date: 2021-08-10
layout:
tags: programmers
---


## Problem
데이터 처리 전문가가 되고 싶은 "어피치"는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, "ababcdcdababcdcd"의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 "2ab2cd2ab2cd"로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 "2ababcdcd"로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, "abcabcdede"와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 "abcabc2de"가 되지만, 3개 단위로 자른다면 "2abcdede"가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

<b>제한사항</b><br>
s의 길이는 1 이상 1,000 이하입니다.
s는 알파벳 소문자로만 이루어져 있습니다.

https://programmers.co.kr/learn/courses/30/lessons/60057


## Solution
문자열을 문자열 개수의 절반을 초과하는 수로 나누는 것은 의미가 없다. 따라서 문자열을 나누는 수(num)는 1 이상 s.length() / 2 까지다.
문자열 나누기는 항상 첫 문자부터 시작해서 나눠야 하므로 now 변수에는 substring 인덱스가 0인 것부터 들어간다.
substring의 끝 인덱스는 '현재 인덱스(idx) * 나누는 수(num) + 나누는 수(num)'이다. 시작 인덱스가 idx * num 이므로 여기에 num 크기만큼 추출해야 하기 때문이다.
하지만, 그 값이 전체 문자열의 길이를 초과할 수 있으므로 초과할 경우 마지막 인덱스는 문자열의 끝으로 정한다.




## Code
```java
class Solution {
    public int solution(String s) {
        int answer = s.length();
        int cnt = 1, endIdx = 0;
        String now = "", next = "", tmpStr = "";
        
        // num: 문자열을 자르는 단위
        for (int num = 1; num <= s.length()/2; num++) {
            cnt    = 1;
            tmpStr = "";
            now    = s.substring(0, num); // 현재 비교 문자열
            
            for (int idx = 1; idx <= s.length()/num; idx++) {
                endIdx = (idx+1)*num > s.length() ? s.length() : (idx+1)*num;
                
                next = s.substring(idx*num, endIdx); // 다음 비교 문자열
                
                if (now.equals(next) == true) {
                    cnt++;
                }
                else {
                    // 2이상일 경우만 축약해서 숫자로 표기하므로 비교 로직 필요
                    tmpStr += ((cnt > 1 ? cnt : "") + now);
                    
                    now = next;
                    cnt = 1;
                }
            }
            
            tmpStr += ((cnt > 1 ? cnt : "") + now);
            answer = Math.min(answer, tmpStr.length());
        }
        
        return answer;
    }
}
```
