---
title: programmers 숫자 야구
date: 2020-02-14 11:30:12
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 완전탐색
---

# 분류 / 레벨 / 언어

완전탐색 / LV.2 / Javscript

# 설명

숫자 야구라는 미니게임이 있다.
이 문제는 게임을 만드는 것은 아니고, 그것을 풀어나가는 과정을 만드는 것이다.

먼저 공역은 1-9 사이의 서로 다른 수들로 이루어진 3자리 수이고,
따로 주어지지 않아서 알아서 구현해주어야 한다.

공역을 default 답안으로 선택하고,
input과 compare(numA, numB)함수의 결과값을 참고하여 답안을 줄여나간다.

# 전체 코드

```javascript
function solution(baseball) {
  const oneNine = "123456789".split("");
  let numSet = [];

  oneNine.forEach((hun, hunIdx) => {
    oneNine.forEach((ten, tenIdx) => {
      if (tenIdx !== hunIdx)
        oneNine.forEach((one, oneIdx) => {
          if (oneIdx !== tenIdx && oneIdx !== hunIdx)
            numSet.push(hun * 100 + ten * 10 + one * 1);
        });
    });
  });

  const compare = (numA, numB) =>
    numA
      .toString()
      .split("")
      .reduce(
        (acc, curr, currIdx) => {
          numB
            .toString()
            .split("")
            .forEach((v, i) => {
              if (v === curr) i === currIdx ? acc[0]++ : acc[1]++;
            });
          return acc;
        },
        [0, 0]
      );

  return baseball.reduce((a, c) => {
    const temp = [];
    a.forEach(num => {
      if (compare(num, c[0])[0] === c[1] && compare(num, c[0])[1] === c[2])
        temp.push(num);
    });
    return temp;
  }, numSet).length;
}
```
