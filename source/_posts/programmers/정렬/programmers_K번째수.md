---
title: programmers K번째 수
date: 2020-01-25 11:35:19
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 정렬
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42748)

# 분류 / 레벨 / 언어

정렬 / LV.1 / Javscript

# 설명

이 문제는 특히 해야할 일을 input에 순차적으로 명시했다.
commands를 여러 command로 분리하고
array를 특정 구간 command[0],command[1] 사이로 자른 후,
정렬하여,
command[2] 위치를 출력한다.
각 언어의 내장 함수를 활용하여 풀어야 한다.

# 전체 코드

```javascript
function solution(array, commands) {
  return commands.map(
    v => array.slice(v[0] - 1, v[1]).sort((a, b) => a - b)[v[2] - 1]
  );
}
```
