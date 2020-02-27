---
title: programmers 카드 게임
date: 2020-02-26 12:50:12
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 동적계획법(Dynamic Programming)
---

# 분류 / 레벨 / 언어

동적계획법(Dynamic Programming) / LV.4 / Javscript

# 설명

## 처음 풀이

빠르게 구현할 수 있고 동시에 모든 요소를 검증할 수 있는
재귀를 사용해 먼저 풀어보았다.
그러나 left와 right의 최대 길이가 각 1000개씩이고,
left[0] >= right[0] 일 경우 최대 2개씩 갈라지므로
최대 2의 1000제곱 만큼의 loop 발생한다.
돌려보니 역시나 시간 초과가 발생했다.

```javascript
function solution(left, right) {
  let max = 0;

  const next = (l, r, sum) => {
    if (l.length * r.length === 0) {
      if (sum > max) max = sum;
      return;
    }

    let lShift = l.slice(1, l.length);
    let rShift = r.slice(1, r.length);

    if (l[0] > r[0]) next(l, rShift, sum + r[0]);
    else {
      next(lShift, r, sum);
      next(lShift, rShift, sum);
    }
  };

  next(left, right, 0);
  return max;
}
```

## DP로 풀어야 하는 이유

input의 최대 길이가 각 1000이므로 1000을 기준으로 생각해봐야 한다.
2의 1000제곱은 어마어마하게 큰 수지만,
2차원 배열의 크기 1000 x 1000은 백만으로 비교적 다룰만한 수이다.
그리고 2차원 배열의 각 칸에 저장되는 값들도
1~2000 사이 정수들의 합으로 구성되므로
공간복잡도 역시 비교적 작은 편이다.

## Top-down vs Bottom-up

6면 모두 단일 숫자로 구성된 주사위가 여러 개 있다.
주사위는 다음과 같은 규칙으로 합쳐버릴 수 있다.

1 주사위 + 1 주사위 => 2 주사위
2 주사위 + 2 주사위 => 3 주사위
...
5 주사위 + 5 주사위 => 6 주사위

Top-down은 6 주사위 시점부터 접근하는 것이고,
Bottom-up은 1 주사위 시점부터 접근하는 것이다.

## 함수형 프로그래밍

특정 위치(index, index)의 값을 반환하는 getMemo 함수를 정의했다.
memo(캐시)에 접근하여 값이 있으면 바로 반환, 없으면 set한 후에 반환한다.

# 전체 코드

이 문제에서 Top-down과 Bottom-up의 유의미한 속도 차이는 없었다.

## Top-down

```javascript
function solution(left, right) {
  const length = left.length;
  const memo = right.concat(0).map(v => left.map(v => -1).concat(-1));
  memo[0][0] = 0;

  let max = 0;

  const getMemo = (l, r) => {
    if (l < 0 || r < 0) return 0;
    if (memo[l][r] > -1) return memo[l][r];
    memo[l][r] =
      left[l] > right[r - 1]
        ? getMemo(l, r - 1) + right[r - 1]
        : Math.max(getMemo(l - 1, r - 1), getMemo(l - 1, r));
    return memo[l][r];
  };

  for (let a = 0; a < length + 1; a++) {
    if (max < getMemo(a, length)) max = getMemo(a, length);
    if (max < getMemo(length, a)) max = getMemo(length, a);
  }

  return max;
}
```

## Bottom-up

```javascript
function solution(left, right) {
  const length = left.length;
  const memo = right.concat(0).map(v => left.map(v => -1).concat(-1));
  memo[0][0] = 0;

  let max = 0;

  const getMemo = (l, r) => {
    if (l < 0 || r < 0) return 0;
    if (memo[l][r] > -1) return memo[l][r];
    memo[l][r] =
      left[l] > right[r - 1]
        ? getMemo(l, r - 1) + right[r - 1]
        : Math.max(getMemo(l - 1, r - 1), getMemo(l - 1, r));
    return memo[l][r];
  };

  for (let a = 0; a < length + 1; a++) {
    for (let b = 0; b < length + 1; b++) {
      if ((a === length || b === length) && max < getMemo(a, b))
        max = getMemo(a, b);
    }
  }

  return max;
}
```
