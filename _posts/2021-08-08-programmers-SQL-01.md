---
title: "SQL 프로그래머스 ORACLE '우유와 요거트가 담긴 장바구니' 문제풀이"
date: 2021-08-08
layout:
tags: programmers
---


## Problem
데이터 분석 팀에서는 우유(Milk)와 요거트(Yogurt)를 동시에 구입한 장바구니가 있는지 알아보려 합니다. 우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요.
이때 결과는 장바구니의 아이디 순으로 나와야 합니다.

## Solution
LISTAGG(컬럼명, 구분자) WITHIN GROUP(ORDER BY 컬럼명)
- 컬럼 값을 합쳐서 한 줄로 만듦

## Code
```sql
SELECT CART_ID
  FROM CART_PRODUCTS
 GROUP BY CART_ID
HAVING LISTAGG(NAME, ' ')  WITHIN GROUP(ORDER BY NAME) LIKE '%Milk%'
   AND LISTAGG(NAME, ' ')  WITHIN GROUP(ORDER BY NAME) LIKE '%Yogurt%'
```
