---
title: programmers 조이스틱
date: 2020-02-13 16:11:20
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42860)

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.2 / Javscript

# 설명

## 그리디 풀이 시도

그리디 카테고리에 있어서 처음엔 그리디 방법론으로 접근했다.
조이스틱이 좌-우로 움직이는 순간을 1 turn으로 생각한다.
다음 조건을 만족시키며 turn을 반복한다.

- [1]ㅡ(왼쪽으로 연속된 A의 개수) <내위치> [2]ㅡ(오른쪽으로 연속된 A의 개수)

  [1]과 [2]중 작은 쪽으로 이동한다.
  (Greedy : 현재 내 위치에서 not A가 더 가깝게 있는 쪽으로 움직인다.)
  BBAAA<내위치>ABBB => [1]
  AAAAB<내위치>AABB => [2]
  만약 [1]과 [2]가 같다면 순리대로 오른쪽으로 이동한다.
  BBAAB<내위치>BBBB => [2]

- 모든 글자가 A라면 turn loop를 끝낸다.

그리고 조이스틱의 여러 움직임을 answer++, answer += count, 배열 처리로 구현했다.

## 반례 등장

ABBBA-------------ABA

그리디 알고리즘으로 풀면 처음에 오른쪽으로 움직인다.
총 접근 방향은 다음과 같다.
->, ->, ->
<-, <-, <-,
<-, <-
조이스틱은 9+4로 13번 움직인다.

반대로 처음에 왼쪽으로 움직이면 더 작은 값이 나온다.
<-, <-
->, ->
->, ->, ->
조이스틱은 8+3로 12번 움직인다.

당연히 최솟값은 12가 맞다. 그래서 처음에 왼쪽으로 움직여야 한다.
그러면 한 치 앞의 좋은 경우를 버리고 두 수, 세 수를 내다보고 움직이는 것과 같고,
결국 그리디 알고리즘이라고 할 수 없다.
카테고리를 왜 그리디 알고리즘에 해놓았지?

## DFS풀이

name의 최댓값은 20이다.
조이스틱을 가장 많이 움직이는 경우는
"NNNNNNNNNNNNNNNNNNNN"
위아래 = 19x20
좌우 = 19
합 = 399
이고, 위아래 움직임 count는 각 node별로 계산할 필요 없이
초기에 loop한번만 돌아서 얻을 수 있다. (고정값)
결국 최대 depth가 19밖에 되지 않으므로 충분히 dfs로 풀 수 있다.

# 전체 코드

## 그리디 풀이

```javascript
const updownCnt = word => {
  const index = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("").indexOf(word);
  return Math.min(index, 26 - index);
};

function solution(name) {
  const length = name.length;
  name = name.split("");

  let cur = 0; //내 위치
  let answer = 0;

  while (1) {
    answer += updownCnt(name[cur]);
    name[cur] = "A";
    if (name.every(word => word === "A")) break;

    let rightIdx = cur;
    let leftIdx = cur;
    let rightCnt = 0;
    let leftCnt = 0;

    while (rightCnt === leftCnt) {
      rightIdx === length - 1 ? (rightIdx = 0) : rightIdx++;
      leftIdx === 0 ? (leftIdx = length - 1) : leftIdx--;
      if (name[rightIdx] === "A") rightCnt++;
      if (name[leftIdx] === "A") leftCnt++;
      if (rightCnt > length / 2) break;
    }
    if (leftCnt > rightCnt) cur === length - 1 ? (cur = 0) : cur++;
    else cur === 0 ? (cur = length - 1) : cur--;
    answer++;
  }

  return answer;
}
```

## DFS 풀이

```javascript
const updownCnt = word => {
  const index = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("").indexOf(word);
  return Math.min(index, 26 - index);
};

function solution(name) {
  const length = name.length;
  name = name.split("");

  let updown = 0;
  let min = 19;

  const dfs = (move, cur, aParam) => {
    if (move >= min) return;

    const isA = aParam.slice();
    isA[cur] = true;

    if (isA.every(v => v)) {
      min = move;
      return;
    }
    let right = cur === length - 1 ? 0 : cur + 1;
    let left = cur === 0 ? length - 1 : cur - 1;
    dfs(move + 1, right, isA);
    dfs(move + 1, left, isA);
  };

  const wasA = name.map(word => {
    if (word === "A") return true;
    updown += updownCnt(word);
    return false;
  });
  dfs(0, 0, wasA);

  return updown + min;
}
```
