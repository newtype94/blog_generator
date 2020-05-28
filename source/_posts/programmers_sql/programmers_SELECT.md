---
title: programmers sql SELECT
date: 2020-05-16 10:32:31
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 sql Kit
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17042)

# 모든 레코드 조회하기

```sql
SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

# 역순 정렬하기

```sql
SELECT NAME, DATETIME
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID DESC
```

# 아픈 동물 찾기

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = "SICK"
ORDER BY ANIMAL_ID
```

# 어린 동물 찾기

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != "AGED"
ORDER BY ANIMAL_ID
```

# 동물의 아이디와 이름

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

# 여러 기준으로 정렬하기

```sql
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC
```

# 상위 n개 레코드

```sql
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1
```