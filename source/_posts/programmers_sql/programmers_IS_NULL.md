---
title: programmers sql IS NULL
date: 2020-05-20 09:28:31
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 sql Kit
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17045)

# 이름이 없는 동물의 아이디

```sql
SELECT A.ANIMAL_ID, A.NAME
FROM ANIMAL_OUTS A LEFT JOIN ANIMAL_INS B ON A.ANIMAL_ID = B.ANIMAL_ID
WHERE B.ANIMAL_ID IS NULL
ORDER BY A.ANIMAL_ID
```

# 이름이 있는 동물의 아이디

```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID
```

# NULL 처리하기

```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, "No name") AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
```
