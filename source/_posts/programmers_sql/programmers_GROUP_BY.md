---
title: programmers sql GROUP BY
date: 2020-05-19 15:31:33
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 sql Kit
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17044)

# 고양이와 개는 몇 마리 있을까

```sql
SELECT ANIMAL_TYPE, COUNT (*) AS count
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = "Cat" OR ANIMAL_TYPE = "Dog"
GROUP BY ANIMAL_TYPE
```

# 동명 동물 수 찾기

```sql
SELECT NAME, COUNT (*) AS count
FROM ANIMAL_INS
WHERE NAME IS NOT null
GROUP BY NAME
HAVING count >= 2
ORDER BY NAME
```

# 입양 시각 구하기(1)

```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >= 9 AND HOUR(DATETIME) <= 19
GROUP BY HOUR
```

# 입양 시각 구하기(2)

```sql
SET @hour = -1;
SELECT (@hour := @hour + 1) AS HOUR,
  (
      SELECT COUNT(*) AS COUNT
      FROM ANIMAL_OUTS
      WHERE HOUR(DATETIME) = @hour
  )
FROM ANIMAL_OUTS
WHERE @hour < 23
```
