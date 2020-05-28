---
title: programmers sql SUM, MAX, MIN
date: 2020-05-17 11:12:51
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 sql Kit
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17043)

# 최댓값 구하기

```sql
SELECT MAX(DATETIME) AS 시간
FROM ANIMAL_INS
```

# 최솟값 구하기

```sql
SELECT MIN(DATETIME) AS 시간
FROM ANIMAL_INS
```

# 동물 수 구하기

```sql
SELECT COUNT(ANIMAL_ID) AS count
FROM ANIMAL_INS
```

# 중복 제거하기

```sql
SELECT COUNT(DISTINCT NAME) AS count
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```
