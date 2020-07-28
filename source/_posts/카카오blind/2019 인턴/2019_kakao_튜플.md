---
title: 카카오 blind 2019 튜플
date: 2020-07-23 17:15:46
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2019 인턴
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64065)

# 문제 풀이

1. input : string => array => sort
2. answer : set => array

# 전체 코드

```javascript
function solution(s) {
  const sets = s
    .split("}")
    .reduce((a, b) => {
      b = b.replace("{{", "").replace(",{", "");
      if (b.length > 0) a.push(b.split(","));
      return a;
    }, [])
    .sort((a, b) => a.length - b.length);

  let answer = new Set([]);

  while (sets.length > 0) {
    const temp = sets.shift();
    while (temp.length > 0) {
      answer.add(parseInt(temp.shift()));
    }
  }

  return [...answer];
}
```
