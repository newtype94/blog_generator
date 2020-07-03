---
title: 카카오 blind 2019 호텔 방 배정
date: 2020-06-20 19:31:22
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2019 인턴
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64063)

# 문제 풀이

문제 풀이 방향을 세 번이나 바꿔서 진행했다.

1. 완전 탐색 풀이
   테스트 케이스는 다 통과하나
   효율성 테스트에서 통과하지 못함

2. DP 풀이
   완전 탐색보다 좋아졌으나 그래도 효율성에서 걸리는 문제가 있음
   DP특성상 정적 배열을 선언해두므로
   방 수는 많고 손님이 극히 적을 때 비효율성 때문에 문제가 되었나 싶기도 함

3. Map을 사용한 풀이
   Object를 사용해도 되지만 Map에는 Set과 마찬가지로 has 메서드가 있어 편리함
   이 방법으로 풀어 해결했다

# 전체 코드

```javascript
function solution(k, room_number) {
  const rooms = new Map();

  const showMeRoom = (pos) => {
    while (rooms.has(pos)) {
      let temp = pos;
      pos = rooms.get(pos) || pos + 1;
      rooms.set(temp, rooms.get(pos) || temp + 1);
    }
    rooms.set(pos, pos + 1);
    return pos;
  };

  return room_number.map((v) => showMeRoom(v));
}
```
