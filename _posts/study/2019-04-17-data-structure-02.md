---
title: "For job interview, about Data Structure 면접 공부하기-자료구조 2"
date: 2019-04-17
layout:
tags: DataStructure
---

## 1. Tree 트리
#### 1. 이진트리 순회
- Pre-order 전위 순회 : 루트 - 왼쪽 자식 - 오른쪽 자식
- In-order 중위 순회 : 왼쪽 자식 - 루트 - 오른쪽 자식
- Post-order 후위 순회 : 왼쪽 자식 - 오른쪽 자식 - 루트

#### 2. 트리와 그래프 차이
- 트리는 방향 그래프이다.
- 트리는 사이클 cycle, 자체 간선 self-loop 도 불가능하다.
- 그래프는 루트 노드의 개념이 없는 반면, 트리는 한 개의 루트 노드만 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가진다.

<br><br>
## 2. Sorting Algorithms 정렬 알고리즘
#### 1. Insertion Sort 삽입 정렬
- 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 알고리즘이다.
- n개의 데이터가 있을 때 최악의 경우 1 + 2 + ... + n-1 번의 비교를 하기 때문에 시간 복잡도는 O(n^2)이다.

#### 2. Selection Sort 선택 정렬
- 제자리 정렬 알고리즘의 하나로, 최솟값 또는 최대값을 찾고 앞에서부터 차례대로 비교하며 정렬을 완성하는 알고리즘이다.
- 시간 복잡도는 O(n^2)이다. 버블 정렬보다 우수하나 삽입 정렬보다 우수하지 않다.

#### 3. Bubble Sort 거품 정렬
- 서로 인접한 두 개의 원소를 검사하여 정렬하는 알고리즘이다. 
- 시간 복잡도는 O(n^2)이다.

#### 4. Quick Sort 퀵 정렬
- 비교 정렬 알고리즘의 하나로, 재귀적으로 분할 정복 방법(피벗 pivot 이용)을 통해 리스트를 정렬한다. 
- 시간 복잡도는 최악의 경우(선택한 피벗이 최소 원소나 최대 원소일 경우) O(n^2)이지만 평균적으로 O(NlogN)이다.
- 거의 모든 언어에서 (파이썬 제외) 제공하는 정렬 함수에서 사용된다.
- 현존하는 컴퓨터 아키텍처 상에서 비교 연산자를 이용해 구현된 정렬 알고리즘 중 가장 고성능인 알고리즘이다. (단, 데이터에 접근하는 시간이 오래 걸리는 하드디스크 등에서 직접 정렬을 수행할 경우 병합 정렬이 더 빠르다.)

#### 5. Merge Sort 합병 정렬
- 비교 정렬 알고리즘의 하나로, 퀵 정렬처럼 재귀적 분할 정복 방법을 사용한다. 
- 퀵 정렬은 기준(피벗)을 두고 정렬한다면, 합병 정렬은 리스트의 길이가 1이 될 때까지 분할한 다음 대소를 비교하며 합병하고 그것을 또 비교하는 방식이다.
- 시간 복잡도는 O(NlogN)이다.

<br><br>
## 3. Fibonacci 피보나치 수열 알고리즘
- Recursion 재귀
  - 시간복잡도는 O(2^n)이며, 재귀를 호출할 때마다 스택에 새로운 계층을 쌓으므로 공간복잡도는 O(n)이다.
  - 반드시 탈출 조건이 있어야 스택 오버플로우 stack overflow 를 방지할 수 있다.
  - 같은 행위가 반복될 때 재귀 함수를 사용한다.
  - 예제.
  ```java
  public int fibo_recursion(int n) {
    if(n == 0) return 0;
    if(n == 1) return 1;
    return fibo_recursion(n-1) + fibo_recursion(n-2);
  }
  ```
- Dynamic Programming 동적 프로그래밍
  - 시간복잡도는 O(n)이다.
  - 이전 연산 값을 memoization 메모이제이션(cache 캐시)을 하며 subproblem을 해결하는 방식이다.
  - 다음은 Top-down 방식이다.
  ```java
  int[] fibo_dp = new int[100]; // 임의로 사이즈 100으로 한정
  public int fibo_dynamicP(int n) {
    if(n <= 1) return n;
    if(fibo_dp[n] != 0) return fibo_dp[n];
    fibo_dp[n] = fibo_dynamicP(n-1) + fibo_dynamicP(n-2);
    return fibo_dp[n];
  }
  ```
  - 다음은 Bottom-up 방식이다.
  ```java
  int[] fibo_dp = new int[100]; // 임의로 사이즈 100으로 한정
  public int fibo_dynamicP(int n) { 
    if(n <= 1) return n;   
    fibo_dp[0] = fibo_dp[1] = 1; 
    for(int i = 2; i < n; i++) fibo_dp[i] = fibo_dp[i-1] + fibo_dp[i-2];
    return fibo_dp[n];
  }
  ```
 
- Iteration 반복 : 시간복잡도는 O(n)이며, 안정성 문제로 가장 좋은 방법이다. 
```java
public long fibo_iteration(int n) {
  for(int i = 2; i < n; i++) fibo_arr[i] = fibo_arr[i-1] + firbo_arr[i-2];
  return fibo_arr[n-1] + fibo_arr[n-2];
}
```



<br><br>
※ 참고 : https://makefortune2.tistory.com/60, https://wayhome25.github.io/cs/2017/04/15/cs-16-1-recursion/, 위키백과, 나무위키 

