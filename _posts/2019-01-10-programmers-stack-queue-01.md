---
title: "[programmers] Stack/Queue '쇠막대기' 문제풀이"
date: 2019-01-10
layout:
categories: algorithms
---

<pre>
import java.util.Stack;
public class IronStick {
	Stack st = new Stack();
	
	public int solution(String arrangement) {
		int answer = 0;
		int idx = 0;
		char now = '*', next = '*';
		
		while(idx < arrangement.length()-1) {
			now = arrangement.charAt(idx);
			next = arrangement.charAt(++idx);
			
			if(now == '(') {
				st.add('(');
				if(next == ')' && !st.empty()) {
					st.pop();
					idx++;
					answer += st.size();
				}					
			}else{
				st.pop();
				answer++;
			}			
		}
		st.pop();
		return answer + 1;
	}
}
</pre> 
