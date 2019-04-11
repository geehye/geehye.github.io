---
title: "Hash 프로그래머스 알고리즘 자바 '베스트앨범' 문제풀이"
date: 2019-01-26
layout:
tags: programmers
---

## Problem
스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.


## Solution
※ 약 2달 뒤 다시 풀어서 성공했다!<br>
- 우선 속한 노래가 많이 재생된 장르를 찾아야 하므로 key가 장르, value가 해당 장르의 재생 횟수를 모두 더한 값인 Hashmap genMap을 만든다.
- 고유 번호와 장르와 재생 횟수를 저장할 Hashmap을 만드는데, key는 중복이 허용되지 않으므로 중복이 절대 발생할 일 없는 '고유번호 + 장르'를 key로 저장하고 재생 횟수를 value로 저장했다.
- 재생 횟수가 가장 높은 순으로 장르 맵을 정렬한다.
- 정렬된 장르 맵에서 장르를 순서대로 뽑고, filter()를 이용해 key에 해당 장르 이름이 포함된 앨범을 필터링하고 <strong>재생 횟수가 같으면 고유번호가 낮은 순으로</strong> 정렬한다. 이 부분을 구현하지 않아서 이전 코드에서 테스트 2번과 15번을 통과하지 못 했다.
- 하나의 장르 당 최대 2개의 앨범을 실으므로 limit(2)를 사용했다.
- 구해진 key는 '고유번호_장르' 형태이므로 "_"로 split 해서 고유번호만 뽑는다. 처음에는 keys[i].charAt(0)을 사용했었는데 고유번호가 10의 자리 수, 100의 자리 수가 될 수 있다는 사실을 간과했다. 반드시 split을 써야 한다!!!




## Code
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.Map;
import java.util.Queue;
import java.util.stream.Collectors;
class Solution {
    public int[] solution(String[] genres, int[] plays) {
         Map<String, Integer> genMap = new HashMap<>();
		 Map<String, Integer> albMap = new HashMap<>();
		 for(int i = 0; i < genres.length; i++) {
			 genMap.put(genres[i], genMap.getOrDefault(genres[i], 0) + plays[i]);
			 albMap.put(i+"_" + genres[i], plays[i]);
		 }
		 genMap = genMap.entrySet()
				 		.stream()
				 		.sorted(Map.Entry.<String, Integer>comparingByValue().reversed())
				 		.collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2) -> e1, LinkedHashMap::new));
		 
		 Queue<Integer> queue = new LinkedList<>();		 
	     for(String g : genMap.keySet()) {
	    	 String[] keys = albMap.entrySet()
	    			 			   .stream()
	    			 			   .filter(a -> a.getKey().contains(g))
	    			 			   .sorted((a,b) -> {
	    			 				   return a.getValue().equals(b.getValue())? a.getKey().compareTo(b.getKey()) :                                                                                                      b.getValue().compareTo(a.getValue());
	    			 			   })
                                   .limit(2)
	    			 			   .map(a -> a.getKey())
	    			 			   .collect(Collectors.joining(","))
	    			 			   .split(",");
	    	 for(int i = 0; i < keys.length; i++) {
	    		String[] s = keys[i].split("_");
		    	queue.add(Integer.parseInt(s[0]));
	    	}
	     }

	     int[] answer = new int[queue.size()];
	     for(int i = 0; i< answer.length; i++) answer[i] = queue.poll();
	     return answer;
    }
}
```
