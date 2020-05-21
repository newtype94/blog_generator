---
title: 카카오 blind 2019 인턴 불량 사용자
date: 2020-05-08 14:12:21
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2019 인턴
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64064)

# 문제 풀이

user_id가 banned_id에서 여러 개에 걸릴 수 있다. 그래서 NxN의 완전탐색으로 풀면 경우의 수를 놓칠 수 있다.

재귀(DFS)로 user_id와 banned_id가 매칭된 상태를 다음 재귀로 넘겨주며
가능한 상황을 다 count해야 한다.

# 전체 코드

```javascript
const checkWord = (a, b) =>
  new RegExp("^" + b.split("*").join(".") + "$").test(a);

function solution(user_id, banned_id) {
  let temp = {};

  const compare = (users, ban, depth) => {
    if (depth < banned_id.length)
      users.forEach((user, i) => {
        if (checkWord(user, ban[0])) {
          const userCopy = users.slice();
          const banCopy = ban.slice();
          userCopy.splice(i, 1);
          banCopy.splice(0, 1);
          compare(userCopy, banCopy, depth + 1);
        }
      });
    else temp[users] = true;
  };

  compare(user_id, banned_id, 0);

  return Object.keys(temp).length;
}
```
