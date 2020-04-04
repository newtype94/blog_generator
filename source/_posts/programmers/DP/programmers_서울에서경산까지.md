---
title: programmers 서울에서 경산까지
date: 2020-03-09 11:42:50
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 동적계획법(Dynamic Programming)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42899)

# 분류 / 레벨 / 언어

동적계획법(Dynamic Programming) / LV.4 / Javscript

# 설명

## DP문제의 특징

travel의 수가 3~100이다.
매 노드에서 travel을 2개 택할 수 있으므로
완전탐색, 재귀로 푼다면 최악의 경우 2의 100제곱 만큼 연산이 필요하다.

126,7650,6002,2822,9401,4967,0320,5376
양, 자, 해, 경, 조, 억, 만, 천

이 수는 너무 크기 때문에
차라리 1,000,000이나 5,000,000정도의 크기를
메모리에 할당해버리고 n번 연산하는 것이 훨씬 빠르다.

## memoization

- travel의 길이 + 1 = 노드의 개수 = node
- K + 1 = 각 노드에서 각 시간 별로 가능한 최대 돈 = time
- => array[node][time] = maximun money

## 시간복잡도

최악의 경우 100 x 100,000 = 10,000,000

1차 for문 : 각 travel에 대하여 2차 for문을 돌린다.
2차 for문 : 각 K에 대하여 memoization 처리!

# 전체 코드

## 실제 상황 그대로 구현한 가독성 좋은 코드

```javascript
function solution(K, travels) {
  //처음 위치는 서울이다
  const pos = [[]];

  //각 travels에 대하여 다음 작업을 한다
  travels.forEach((tr, i) => {
    //각 travels에 다음 위치로 건너가므로 다음 pos를 하나 push한다
    pos.push(new Array(K + 1).fill(0));

    //첫 travel은 그대로 적용된다
    if (i === 0) {
      pos[1][tr[0]] = tr[1];
      pos[1][tr[2]] = tr[3];
    }
    //이후의 travel은 다음 pos가 최대 money들을 가지게 처리한다
    else
      for (let t = 0; t <= K - Math.min(tr[0], tr[2]); t++) {
        //시간 초과하는 것은 애초에 for문을 돌리지 않는다.

        //현재 pos에서 money가 0인 시간대는 통과한다.
        if (pos[i][t] === 0) continue;

        //K이내로 다음 pos에 도달할 수 있다면
        if (t + tr[0] <= K)
          //그것이 최댓값인지 확인
          pos[i + 1][t + tr[0]] = Math.max(
            pos[i + 1][t + tr[0]],
            pos[i][t] + tr[1]
          );
        //K이내로 다음 pos에 도달할 수 있다면
        if (t + tr[2] <= K)
          //그것이 최댓값인지 확인
          pos[i + 1][t + tr[2]] = Math.max(
            pos[i + 1][t + tr[2]],
            pos[i][t] + tr[3]
          );
      }
  });

  return Math.max(...pos[travels.length]);
}
```

## 효율을 극대화한 코드

풀고나니 굳이 전체 position을 메모리에 둘 필요가 없었다.
이곳 저곳의 계산 결과를 참조하는 것이 아니라
바로 직전의 계산 결과만을 필요로 하기 때문이다.
js array의 reduce()함수는 이전 루프의 return 값을 메모리에 올려 다음 루프를 돈다.
이 장점을 사용하여 공간복잡도를 더 줄이고 코드도 깔끔하게 바꾸었다.

```javascript
function solution(K, travels) {
  return Math.max(
    ...travels.reduce((prev, tr, i) => {
      const next = new Array(K + 1).fill(0);
      if (i === 0) {
        next[tr[0]] = tr[1];
        next[tr[2]] = tr[3];
      } else
        for (let t = 0; t <= K - Math.min(tr[0], tr[2]); t++) {
          if (prev[t] === 0) continue;
          if (t + tr[0] <= K)
            next[t + tr[0]] = Math.max(next[t + tr[0]], prev[t] + tr[1]);
          if (t + tr[2] <= K)
            next[t + tr[2]] = Math.max(next[t + tr[2]], prev[t] + tr[3]);
        }
      return next;
    }, [])
  );
}
```
