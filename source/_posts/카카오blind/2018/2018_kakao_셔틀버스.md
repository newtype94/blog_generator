---
title: 카카오 blind 2018 셔틀버스
date: 2020-09-11 15:18:42
tags:
  - 알고리즘
  - 카카오
category:
  - 카카오 blind test
  - 2018
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17678)

# 문제 풀이

배열과 루프를 활용한 구현 문제이다.

단, 주의할 점이 있다.

보통 이런 류의 문제는 버스를 기다리는 사원들(timetable)이 전부 다 탈 수 있도록 설계해서 내지만 이 문제는 그렇지 않았다.
즉 timetable 안에서 버스를 못타는 사람이 충분히 생길 수 있다.

이것을 해결하기 위해 timetable을 sort하고 n\*m으로 slice하고 푼다고 해도,
아래와 같은 경우라면 버스를 못타는 사람이 또 생길 수 있다.

- 2인승 버스 3대가 준비되어있고, 9시 이전에 1명만 대기한다.
- 사람이 10명 대기하고 있어서 앞에서 6명을 잘랐다.
- 첫 버스에 1명만 탈 수 있다. 두 번째 버스에는 2명이 탄다. 마지막 버스 차례에 3명이 대기중인데 2인승이므로 1명은 낙오된다.

그래서 이 문제는 if로 분기를 잘 나누어야 한다.

# 전체 코드

```javascript
const toTime = (str) => {
  let hour = Math.floor(str / 60);
  let minute = str % 60;
  if (hour < 10) hour = "0" + hour;
  if (minute < 10) minute = "0" + minute;
  return hour + ":" + minute;
};

function solution(n, t, m, timetable) {
  let remain = n * m; //이용 가능한 좌석 수

  timetable = timetable
    .map((v) => {
      const [hour, minute] = v.split(":");
      return 60 * hour + 1 * minute;
    })
    .sort((a, b) => a - b)
    .slice(0, remain);

  let now = 540;
  let lastBus = 540 + (n - 1) * t;
  let thisBus = [];

  while (now <= lastBus) {
    thisBus = [];

    while (timetable.length > 0 && timetable[0] <= now && thisBus.length < m) {
      thisBus.push(timetable.shift());
    }

    if (timetable.length === 0)
      return thisBus.length === m ? toTime(thisBus.pop() - 1) : toTime(lastBus);
    if (timetable[0] > lastBus) return toTime(lastBus);

    now += t;
  }

  return timetable.length > 0 ? toTime(thisBus.pop() - 1) : toTime(lastBus);
}
```
