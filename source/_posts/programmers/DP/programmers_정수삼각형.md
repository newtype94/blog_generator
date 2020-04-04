---
title: programmers 정수 삼각형
date: 2020-02-24 14:21:08
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 동적계획법(Dynamic Programming)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43105)

# 분류 / 레벨 / 언어

동적계획법(Dynamic Programming) / LV.3 / Javscript

# 설명

마찬가지로 메모이제이션을 할 건데,
이 문제는 삼각형의 각 노드에 메모이제이션을 해줄 수 있어 편하다.

각 loop가 의미하는 것은 삼각형의 row들을 점검하는 것이고
row 점검을 마무리한 후, 최댓값(최적의 값)으로 덮어씌운다.

그리고 이 과정을 보다 짧게 코딩하기 위해 reduce를 사용했다.

# 전체 코드

```javascript
function solution(triangle) {
  return Math.max(
    ...triangle
      .reduce((acc, cur, idx) => {
        if (cur.length === 1) acc.push(cur);
        else
          acc.push(
            cur.map((v, i) => {
              if (i === 0) return v + acc[idx - 1][0];
              else if (i === cur.length - 1) return v + acc[idx - 1][i - 1];
              else return v + Math.max(acc[idx - 1][i - 1], acc[idx - 1][i]);
            })
          );
        return acc;
      }, [])
      .pop()
  );
}
```
