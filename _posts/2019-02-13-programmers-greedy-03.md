---
title: "Greedy 프로그래머스 알고리즘 자바 '조이스틱' 문제풀이"
date: 2019-02-13
layout:
tags: programmers
---


## Problem
조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동

예를 들어 아래의 방법으로 JAZ를 만들 수 있습니다.
- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.

만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

- name은 알파벳 대문자로만 이루어져 있습니다.
- name의 길이는 1 이상 20 이하입니다.


## Solution
※ 2019.02.28 테스트 케이스가 추가되었는데 그래서 11번 문제는 통과하지 못 했다. 아마도 'AAABAAAA' 와 같은 유형일 것 같은데 해결 방법이 조금 복잡해질 것 같아서 해결하는 것을 잠시 보류한다.<br>
- 테스트케이스가 추가되기 전에는 좌측으로 해결하는 방법과 우측으로 해결하는 방법 2가지만 고려했다.
- 좌측으로 움직일 경우 첫번째 커서에서 마지막 커서로 움직이게 되는데, 커서 이동 전에 name의 첫번째 값을 바꾼 후 이동하는 것이 훨씬 적은 조작 횟수가 나온다. 따라서 for문을 돌기 전에 첫번째 문자에 대해 처리를 한다.
- A ~ Z 중에서 A를 0으로 뒀을 때 N은 13이고 O는 14이다. 하지만, Z ~ A 중에서 Z를 1로 뒀을 때 (커서를 끝으로 움직이면 스틱을 한 번 움직인 것이기 때문) O는 12이고 N은 13이다. 따라서 문자가 13번째보다 앞에 있는지 뒤에 있는지에 따라 '다음 알파벳'으로 갈지 '이전 알파벳'으로 갈지 정한다.
- 나머지도 마찬가지로 수행하며, 현재까지 바뀐 문자열이 원하는 문자열과 같은지 확인하고 같으면 더이상 스틱을 조작하지 않도록 한다.
- 매 움직임마다 카운트 변수 lcnt, rcnt를 증가시키고 이 중 가장 작은 값을 반환한다.

## Code
```java
import java.util.Arrays;
class Solution {
    public int solution(String name) {
        int lcnt = 0, rcnt = 0, idx = 0;
        char[] larr = new char[name.length()];
        char[] rarr = new char[name.length()];
        Arrays.fill(larr, 'A'); Arrays.fill(rarr, 'A');
        
        if(name.charAt(0) != 'A') {
        	int cnt = (name.charAt(0) - 'A' <= 13? name.charAt(0) - 'A' : 91 - name.charAt(0));
        	
        	rarr[0] = name.charAt(0); larr[0] = name.charAt(0);
        	rcnt = lcnt = cnt;
		idx = 1;
        }
        
        for(int i = idx, j = name.length() - 1; i < name.length(); i++, j--) {	
        	if(!String.copyValueOf(rarr).equals(name)) {
        		rcnt++;
            		if(name.charAt(i) - 'A' <= 13) rcnt += name.charAt(i) - 'A';
            		else rcnt += 91 - name.charAt(i);
            		rarr[i] = name.charAt(i);
        	}
        	
        	if(!String.copyValueOf(larr).equals(name) && j > 0) {
            		lcnt++;
            		if(name.charAt(j) - 'A' <= 13) lcnt += name.charAt(j) - 'A';
            		else lcnt += 91 - name.charAt(j);        	        	
            		larr[j] = name.charAt(j);
        	}
        }     
        return Math.min(lcnt, rcnt);  
    }
}    
```
