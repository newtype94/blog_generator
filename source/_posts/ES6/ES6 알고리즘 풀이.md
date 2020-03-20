---
title: ES6에서 알면 좋은 문법(feat. 알고리즘 문제풀이)
date: 2020-02-11 12:20:10
tags:
  - Javascript
category:
  - ES6
---

알고리즘 문제를 풀며 많이 사용했던 JS 기술들을 정리해보았다.
코테에서 파이썬만큼 강력하진 않지만, JS도 익숙해지면 충분히 좋은 언어다.

# Array

## const vs let

ES6에 변수 선언 방식이 다음과 같이 추가되었다.

const = 재할당 불가능
let = 재할당 가능

배열도 마찬가지이다.
단 헷갈릴 수 있는 부분이 있어 따로 정리해보았다.

```javascript
const constArr = [1, 1, 1];
let letArr = [2, 2, 2];

constArr[1] = ["new"]; //가능
letArr[1] = ["new"]; //가능

constArr.push("new"); //가능
letArr.push("new"); //가능

// 단, 아래처럼 통으로 갈아치우는 것은 차이가 생긴다
constArr = ["new", "arr"]; //불가능
letArr = ["new", "arr"]; //가능

constArr = constArr.reduce(); //불가능
letArr = constArr.reduce(); //가능

constArr = constArr.map(); //불가능
letArr = constArr.map(); //가능
```

## 초기화

```javascript
const input = [1, 2, 3, 4, 5];
const allTrue = new Array(input.length).fill(true);

console.log(allTrue); //[true, true, true, true, true]
```

## 객체, 배열 값 추출

객체, 배열에서 값을 추출할 때
위치와 매칭하여 값을 변수에 바로 저장할 수 있다.

```javascript
const [a, b, c] = [1, 2, 3];
//const a = [1,2,3][0]
//const b = [1,2,3][1]
//const c = [1,2,3][2]

const [d, e] = [4, 5, "add"];

const { f, g, h } = { f: 6, g: 7, h: 8 };
const { i, j } = { i: 9, j: 10, k: 11 };

console.log(a, b, c, d, e, f, g, h, i, j);
//1,2,3,4,5,6,7,8,9,10,11
```

## 큐와 스택처럼 사용하기

큐와 스택처럼 쓸 수 있다.

```javascript
const myArr = [1, 2, 3, 4, 5];

const firstItem = array.shift(); //return : 1
console.log(myArr); //[2,3,4,5]

array.unshift(firstItem); //return : undefined
console.log(myArr); //[1,2,3,4,5]

const lastItem = array.pop(); //return : 5
console.log(myArr); //[1,2,3,4]

array.push(lastItem); //return : undefined
console.log(myArr); //[1,2,3,4,5]
```

## 중간에 위치한 요소 제거, splice

- 원본을 수정시킨다
- splice(index, index로부터 추출할 길이)

```javascript
const myArr = [1, 2, 3, 4, 5];

const part = myArr.splice(1, 2);
console.log(part); //[2,3]
console.log(myArr); //[1,4,5]

//만약 제거하고 싶은 index를 모른다.
const findIdx = myArr.indexOf(1); //0
myArr.splice(findIdx, 1); //index 0부터 1개의 요소 제거완료
console.log(myArr); //[4,5]
```

## 전체 복사, 특정 부위 추출 slice

- 원본을 그대로 놔둔다
- shallow copy
- slice(추출시작 index, 추출하려는 마지막 index + 1)

```javascript
const myArr = [1, 2, 3, 4, 5];

const copy = myArr.splice(1, 2);
console.log(copy); //[2,3]
console.log(myArr); //[1,2,3,4,5]

//만약 제거하고 싶은 index를 모른다.
const findIdx = myArr.indexOf(1); //0
myArr.slice(findIdx, 1); //index 0부터 1개의 요소 제거완료
console.log(myArr); //[4,5]
```

## reduce()

정말 많이 쓰인다.
알고리즘의 거의 모든 문제에서
배열 전체를 돌면서 검증하고, 어떤 아웃풋을 만드는 일이 생기기 때문이다.

**array.reduce(콜백함수, 초깃값)**

콜백함수

1. 매개변수는 (누적값, 현재값, 현재index, 원본배열)
2. return 값은 마지막 턴에서 return하는 누적값이다.
3. 매개변수는 앞에서부터 최소 2개, 쓰고 싶은 곳까지만 쓰면 된다.

루프

1. 매 턴, 전 턴에서 누적된 값을 "누적값"으로 받아온다.
2. 누적값이 없는 첫 턴은 누적값 = 초깃값이다
3. 원본 배열은 건드리지 않는다. 따라서 array는 항상 원본 배열 그대로이다.

```javascript
const fiveNums = [11, 22, 33, 44, 55];
const ten = 10;

let namuzi = 0;

//콜백함수는 당연히 전역 변수(namuzi)도 건드릴 수 있다.
let sum = fiveNums.reduce((acc, curr, currIdx, array) => {
  acc += curr;
  namuzi += curr % ten;
  return acc;
}, 0);
```

## forEach()

for문으로 배열 전체를 훑는 것과 같은 기능이다.
가독성이 조금 더 좋다는 장점이 있고,
중간에 break를 할 수 없다는 단점이 있다.

```javascript
const fiveNums = [11, 22, 33, 44, 55];

//아래 2개의 루프는 정확히 같은 값을 출력한다.

for (let i = 0; i < fiveNums.length; i++) {
  console.log(i);
  console.log(fiveNums[i]);
  console.log(fiveNums);
}

fiveNums((item, index, array) => {
  console.log(index);
  console.log(item);
  console.log(array);
});
```

## every, some

# Object

# set

## set 선언

set 선언시 배열이 input으로 필요하다.

```javascript
const mySet = new Set([1, 2, 2, 3, 3, 4, 4]);
console.log(mySet); //set {1,2,3,4}

console.log(mySet.size); //3
console.log(mySet.has(1)); //true
mySet.add(5);
console.log(mySet); //set {1,2,3,4,5}
mySet.delete(5);
console.log(mySet); //set {1,2,3,4}
```

## set <=> array

보통 set에는 forEach를 제외하면 array에서 유용하게 쓰는 메서드를 지원하지 않는다.
"..."를 활용하여 array로 임시로 형 변환을 하고 array 메서드를 빌릴 수 있다.

[set 표준 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set)
[array 표준 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)

```javascript
const mySet = new Set([1, 2, 2, 3, 3, 4, 4]);

const tmp = [...mySet];
console.log(tmp); //[1,2,3,4]

const newSet = new Set([...mySet].sort((a, b) => a - b).slice(0, 2));
//가장 작은 두 요소를 뽑기 위해 잠깐 배열의 형태를 빌린다고 생각하면 된다.
```

# Math

## min, max

Math.min(1,2,3) => 1
Math.max(1,2,3) => 3

```javascript
//배열은 바로 넣을 수 없다.
const arr = [1, 2, 3];

//요소만 넣어야 한다.
let num = Math.min(...arr);

//가끔 비교해서 작은 경우만 넣고 싶을 때가 있다.
const zero = 0;
if (zero < num) zero = num;

//위처럼 해도 좋지만 가독성을 위해 아래처럼도 많이 쓴다.
num = Math.min(zero, num);
```
