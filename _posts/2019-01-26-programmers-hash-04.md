---
title: "Hash '베스트앨범' 알고리즘 문제풀이"
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
해당 코드는 테스트 케이스 2번만 통과하지 못 했다. 왜 그런지는 아직 찾고있는 중이다.

<pre>
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.Map;
import java.util.Queue;
import java.util.stream.Collectors;
public class BestAlbum {
    public int[] solution(String[] genres, int[] plays) {
        Map<String, Integer> genreMap = new HashMap<>();
        Map<String, Integer> musicMap = new HashMap<>();
        String[] tmp = new String[2];
        
        for(int i = 0; i < plays.length; i++) {
        	genreMap.put(genres[i], genreMap.getOrDefault(genres[i], 0) + plays[i]);
        	musicMap.put(genres[i] + "_" + i, plays[i]);
        }      
        genreMap = genreMap.entrySet().stream().sorted((Map.Entry.<String, Integer>comparingByValue().reversed())).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2) -> e1, LinkedHashMap::new));
        musicMap = musicMap.entrySet().stream().sorted((Map.Entry.<String, Integer>comparingByValue().reversed())).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2) -> e1, LinkedHashMap::new));
        
        Queue<Integer> queue = new LinkedList<Integer>();
        for(String genre : genreMap.keySet()) {
        	byte cnt = 0; 
        	for(String key : musicMap.keySet()) {
        		if(key.startsWith(genre) && cnt < 2) {
        			tmp = key.split("_");
        			queue.add(Integer.parseInt(tmp[1]));
        			cnt++;
        		}       			
        	}
        }
       
        int[] answer = new int[queue.size()];
        for(int i = 0; i < answer.length; i++)
        	answer[i] = queue.poll();
        return answer;
    }
}
