---
title: programmers 단어 변환
date: 2020-02-07 17:29:31
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - DFS,BFS
---

# 분류 / 레벨 / 언어

DFS,BFS / LV.3 / Javscript

# 설명

문제에 필요한 방법론이 DFS일 때, 스택을 쓰거나 재귀함수로 푸는 방법 2개가 있다.
이 문제는 재귀함수를 사용하여 풀었다.
재귀함수는 재귀 탈출을 확실히 정의 할 수 있을 때 사용해야 한다.

이번 문제에서는, 모듈을 분리할 수 있는 것은 가능한 메인 함수 밖에서 정의했다.

# 전체 코드

```javascript
const oneDiff = (a, b) => {
  let cnt = 0;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) cnt++;
    if (cnt > 1) return false;
  }
  if (cnt === 1) return true;
  else return false;
};

const nextAble = (now, nexts) =>
  nexts.reduce((acc, curr) => {
    if (oneDiff(now, curr)) acc.push(curr);
    return acc;
  }, []);

function solution(begin, target, words) {
  if (!words.includes(target)) return 0;

  let answer = 50;

  const goNext = (now, remainWords, cnt) => {
    const nextWords = nextAble(now, remainWords);
    if (!nextWords.includes(target))
      nextWords.forEach(data => {
        const remainCopy = remainWords.slice(0, remainWords.length);
        remainCopy.splice(remainCopy.indexOf(data), 1);
        goNext(data, remainCopy, cnt + 1);
      });
    else if (cnt < answer) answer = cnt;
  };

  goNext(begin, words, 1);
  return answer;
}
```
