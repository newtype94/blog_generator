---
title: Javascript(ES5, ECMAscript2014)
date: 2017-08-10 13:11:01
tags:
  - javascript
category:
  - web
  - javascript
---

## 기본문법

### 시작

식별자 = 변수명 or 함수명

주석 = HTML태그주석 or 자바스크립트 주석

`<!-- -->`로 문자열을 감싸 생성
`//한줄짜리 주석`
`/* 여러 줄 주석 */`

`alert("메시지");` 기본적인 출력 알람 팝업

사칙연산 : + - \* / %

문자열 '끼리 또는 "끼리 쓰면 되는데 '를 권장

\t 수평탭
\n 행 바꿈
`\\` \\
`\'` '
`\"` "
문자열 연결 연산자 = +
'김' + '용훈' = '김용훈'
불리언 : >=, <=, >, <, ==, !=

! 논리 부정
!! 논리합
&& 논리곱
var로 모든 변수 선언
복합 대입 연산자
+=, -=, \*=, /=, %=

### 증감 연산자

- 변수++, 변수--(후위)
- ++변수, --변수(전위)

### 자료형 검사

- typeof(값)
- typeof(초기화되지 않은 변수) = undefined

### 입력 받기

`prompt('나이 입력하샘', 'ex) 24살');` //문자열로 입력받음
`var input = confirm('수락할거임?');` //확인,취소 버튼이 뜨고 불리언으로 입력받음

### 숫자 <-> 문자열 자료형 변환

- String(숫자) : 문자열이 됨
- Number(문자열) : 숫자가 됨
- Number(문자열) : 숫자로 변환 불가할 경우 NaN으로 출력됨

### 불 자료형 변환

이 5가지가 false이고 나머지는 모두 true

- Boolean(0)
- Boolean(Nan)
- Boolean('')
- Boolean(null)
- Boolean(undefined)

### 일치 연산자

- === : 양쪽 변의 자료형과 값이 일치
- !== : 양쪽 변의 자료형과 값이 다름
- ex) 0 == false는 자동 형 변환을 거쳐 true로 인식되지만 0 === false는 false로 인식됨

### ECMAScript6에 추가된 것

- 템플릿 문자열 = \${ 표현식 } // 문자열이 만들어질 때 표현식이 계산되어 들어감
- '100 + 50 은' + \${ 100+ 50 } + '이다' = '100 + 50은 150이다'
- \${ 변수 }도 가능

| 키워드   | 종류  | 성격              |
| ----- | --- | --------------- |
| var   | 변수  | 전역 스코프, 재선언 가능  |
| let   | 변수  | 해당 스코프, 재선언 불가능 |
| const | 상수  | 해당 스코프, 재선언 불가능 |

## 조건문

```javascript
	if (조건문) {
		참 일 경우 실행
	}

	if (조건문) {
	} else if{
	} else {
	}
```

```javascript
	switch (<비교할 값>) {
		case <값>:
			<문장>
			break;
		case <값>:
			<문장>
			break;
		default :
			<문장>
			break;
	}
```

### 삼항 연산자

- <불 표현식> ? <참일 때 실행하는 문장> : <거짓일 때 실행하는 문장>
- EX) (number > 0) ? alert('양수') : alert('양수가 아님') ;

### 짧은 조건문

연산자 뒤 문장이 영향이 있는지가 중요

```javascript
true || alert("실행안됨");
false || alert("실행됨");
true && alert("실행됨");
false && alert("실행안됨");
```

## 반복문

```javascript
	for(var i=0; i<반복횟수; i++){
		문장
	}

	for(var 변수(인덱스) in <배열 또는 객체>){
		문장
	}

	while(조건문){
		문장
	}

	do {
		문장
	} while(조건문)
```

break 키워드 - switch문이나 반복문을 벗어날 때 사용
continue 키워드 - 반복문에서 현재 반복 구간을 멈추고 다음 반복구간을 처음부터 시작함

## 배열

배열에 자료형 다 혼합시킬 수 있음

```javascript
var array = [273, '문자열', true, function(){}, {}, [178,70] ];
array.length // 배열의 길이 return
array.push(마지막 값) // 배열의 마지막 부분에 값 추가
```

## ECMAScript6에 추가된 것

기존의 for in 반복문은 반복 변수에 '요소'가 아니라 '인덱스'가 들어감

```javascript
var array = ["a", "b", "c"];
for (var i in array) {
  alert(i + "번째 값은" + array[i]);
}
```

하지만 새로운 for of 반복문은 반복 변수에 '요소'가 들어감

```javascript
for (const element of ["a", "b", "c"]) {
  alert("요소는 ${element}입니다.");
}
```

## 함수

- 익명함수
  - function () {};
- 선언적함수
  - function 함수() {};

### 익명함수 활용법

```javascript
var 함수 = function() {};
```

### 익명함수 간의 우선순위

```javascript
var 함수 = function (){ alert('AAA') };
var 함수 = function (){ alert('BBB') };
함수();
==> BBB출력됨
```

### 선언적함수와 익명함수 간의 우선순위

자바스크립트는 모든 코드를 읽기 전에 선언적 함수부터 읽는다

```javascript
var 함수 = function (){ alert('AAA') };
function 함수 () { alert('BBB') };
함수 ();
===> AAA출력됨
```

### 매개변수와 반환값

정해진 매개변수외에 추가로 입력된 매개변수는 무시됨
정해진 매개변수보다 적게 입력되었다면 그 자리는 undefined

```javascript
function 함수이름(매개변수, 매개변수, 매개변수) {
  return 반환값;
}
```

### Array() 함수

| 메서드                  | 기능                   |
| -------------------- | -------------------- |
| Array()              | 빈 배열을 만듬             |
| Array(number)        | number크기를 가지는 배열을 만듬 |
| Array(any, ..., any) | 입력된 매개변수로 배열을 만듬     |

### 가변 인자 함수

매개변수의 개수가 변할 수 있는 함수

```javascript
function sumAll() {}
=> 아무 내용이 없는 함수에 기본적으로 arguments 변수가 있다.
arguments는 입력받은 매개변수로 이루어진 배열이다.
```

ex) sumAll(1,2,3)일 경우에 arguments[0]=1이다

### 내부 함수

외부 함수의 내부에서만 작동하는 함수임

```javascript
function <외부 함수>(){
	function <내부 함수>(){
		<함수 코드>
	}
}
```

### 콜백 함수

매개변수로 전달되는 함수, 주로 익명함수로 선언한다.

```javascript
function 열번(매개) {
  for (var i = o; i < 10; i++) {
    매개();
  }
}
var 콜백 = function() {
  alert("출력");
};
열번(콜백);
```

매개변수(콜백함수)에 익명함수를 바로 입력할수도 있다.

```javascript
function 열번(
	function(){ alert('출력'); };
);
```

### 클로저

지역 변수를 살려내기 위해 쓰는 기법

```javascript
function test(name) {
  var output = "Hello" + name;
}
```

이 경우 output은 지역변수이다. 밖에서 사용할 수 없다.

```javascript
function test(name) {
  var output = "Hello" + name;
  return function() {
    alert(output);
  };
}
test("Kim");
```

output은 어디까지나 지역변수라서 변수 자체는 사용할 수 없고,
이렇게 함수를 리턴하는 방식으로, 간접적으로나마 살릴 수 있다.

```javascript
var test_1 = test(Kim);
var test_2 = test(Jung);
test_1();
test_2();
```

또한 이렇게 쓸 수도 있다.

### 내장 함수 - 타이머 함수

| 메서드                                | 기능                  |
| ---------------------------------- | ------------------- |
| setTimeout(function, millisecond)  | 일정 시간 후 함수를 한 번 실행  |
| setInterval(function, millisecond) | 일정 시간마다 함수를 반복해서 실행 |
| clearTimeout(id)                   | setTimeout 해제       |
| clearInterval(id)                  | setInterval 해제      |

setTimeout 설정과 동시에 id생성하기

```javascript
var id = setTimeout(function, millisecond);
```

### 내장 함수 - 인코딩과 디코딩 함수

| 메서드                              | 기능                           |
| -------------------------------- | ---------------------------- |
| escape()                         | 적절한 정도로 인코딩                  |
| unescape()                       | 적절한 정도로 디코딩                  |
| encodeURI(uri)                   | 최소한의 문자만 인코딩                 |
| decodeURI(encodedURI)            | 최소한의 문자만 디코딩                 |
| encodeURIComponent(uriComponent) | 문자 대부분을 모두 인코딩 (현재 가장 많이 쓰임) |
| decodeURIComponent(encodedURI)   | 문자 대부분을 모두 디코딩               |

### 내장 함수 - 코드 실행 함수

```javascript
eval(string) - string을 자바스크립트 코드로 실행합니다.
var willEval = "alert('KIM');";
eval(willEval);
```

### 내장 함수 - 숫자 확인 함수

```javascript
isFinite(number) - number가 무한한 값인지 확인
isNaN(number) - number가 NaN인지 확인
```

### 내장 함수 - 숫자 변환 함수

1000원 1.5\$를 변환

```javascript
parseInt(string)	string을 정수로 바꿈	1000, 1
parseFloat(string)	string을 유리수로 바꿈	1000, 1.5
Number(string)	string을 숫자로 바꿈	풀숫자가 아니면 바꿀수가 없음 NaN, NaN
```

### 자바스크립트의 실행 순서

```javascript
alert("A");
setTimeout(function() {
  alert("C");
}, 0);
alert("B");
```

A -> B -> C 순서로 출력
웹브라우저에 처리를 부탁하는 함수( ex : 타이머함수, 웹 요청 관련 함수)는 모든 코드의 실행이 끝나야 실행됨

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    alert(i);
  }, 0);
}
```

코드가 끝나고(for문이 다 돌고) setTimeout함수가 실행되므로, 3 3 3출력됨
0 1 2를 출력하고 싶으면 변수를 따로 복사해두어야함

```javascript
for (var i = 0; i < 3; i++) {
  (function(closed_i) {
    setTimeout(function() {
      alert(closed_i);
    }, 0);
  })(i);
}
```

이렇게 반복문을 실행하는 동안 클로저가 생성되어 변수 closed_i에 값을 저장할 수 있음

```javascript
[0, 1, 2].forEach(function(i) {
  setTimeout(function() {
    alert(i);
  }, 0);
});
```

### 기본 매개변수

매개변수를 입력하지 않았을 때 강제로 초기화하는 것을 기본 매개변수라고 함
= 매개변수가 undefined 자료형이면 값을 넣겠다.

```javascript
function test(a, b, c) {
  if (!b) {
    b = 2;
  }
  if (!c) {
    c = 3;
  }
  alert(a + "//'" + b + "//" + c);
}
test(1, 40);
```

변수가 입력되면 앞에서부터 들어감 1 // 40 // 3 출력!
더 간결한 방법도 있음

```javascript
function test(a, b, c) {
  b = b || 2;
  c = c || 3;
  alert(a + "//'" + b + "//" + c);
}
test(1, 40);
```

## 객체

객체 = 배열을 기반으로 만들어짐

```javascript
var product = {
  제품명: "건조 망고",
  유형: "당절임",
  성분: "망고, 설탕",
  원산지: "필리핀"
};
```

표현방법 -> 2가지
product['제품명'] = '건조 망고'
product.제품명 = '건조 망고'

배열 내부에 있는 값 하나하나는 요소(element)
<-> 객체 내부에 있는 값 하나하나는 속성(property)

객체의 속성들 중 자료형이 함수인 속성 = 메소드(method)

```javascript
var person = {
	name : 김용훈
	go : function (city) { alert(city); };
}
person.go(서울); // go 메소드를 호출하였다.
```

같은 객체 내의 속성을 호출할 때 = this 키워드

```javascript
var person = {
	name : 김용훈
	go : function(city){
	alert(this.name + city + '갔다');
	}
}
person.go(서울); // 김용훈서울갔다
```

### for in 반복문

객체의 모든 속성+속성값을 하나씩 출력

```javascript
for (var key in product) {
  alert(key + ":" + product[key]);
}
```

### with 키워드

```javascript
var product = {
  제품명: "건조 망고",
  유형: "당절임",
  성분: "망고, 설탕",
  원산지: "필리핀"
};
var output = "";
output += "제품명=" + product.제품명 + "\n";
output += "유형=" + product.유형 + "\n";
output += "성분" + product.성분 + "\n";
output += "원산지" + product.원산지 + "\n";
alert(output);
```

이렇게 product.어쩌구로 쓰면 코드가 복잡하므로 with 키워드를 사용

```javascript
with (product) {
	output += "제품명=" + 제품명 + "\n";
	output += ~~~~~~~~;
	output += ~~~~~~~~;
	output += ~~~~~~~~;
}
```

### with 키워드 사용 시 변수 이름 충돌

경우 : 객체의 속성 이름과 전역 변수의 이름이 같다

```javascript
var product = {
	~~~~
	output = "이미 있지롱";
}
var output = "";
with(product){
	output += ~~~~~; // 그냥 output이면 객체의 속성
	window.output += ~~~~~; // window.output이면 전역변수
}
```

### 객체의 속성 추가

```javascript
var student = {};
//객체에 속성 추가
student.이름 = "김용훈";
student.나이 = "24";
//객체에 메서드 추가
student.toString = function() {
  var output = "";
  for (var key in this) {
    //방금 만든 toString은 포함하지 않음
    if (key != "toString") {
      output += key + this[key] + "\n";
    }
  }
  return output;
};
```

### 객체의 속성 제거

delete 키워드 사용

```javascript
delete student.나이;
```

객체를 생성(반환)하는 함수

```javascript
function makeStudent(name, k, m, e) {
  var willReturn = {
    이름: name,
    국어: k,
    수학: m,
    영어: e
  };
  return willReturn;
}
```

### 객체들로 배열 구성하기

```javascript
function makeStudent(name, k, m, e) {
  생략;
}
var students = [];
//push로 students배열의 왼쪽부터 채워넣음
students.push(makeStudent("김용훈", 100, 100, 100));
students.push(makeStudent("김유림", 100, 100, 100));
```

## 생성자

### 생성자 함수 선언

생성자 함수의 이름은 대문자로 시작하는 것이 관례

```javascript
function <생성자 함수 이름>(){
	this.<속성이름>
	this.<속성이름>
	this.<메서드이름>
}
```

### 객체 생성

```javascript
new <생성자 함수 이름>()
```

### 예제

```javascript
function Student(name, k, m, e) {
  this.이름 = name;
  this.국어 = k;
  this.수학 = m;
  this.영어 = e;

  this.getsum = function() {
    return this.국어 + this.수학;
  };
}
var student = new Student("김용훈", 100, 100, 100);
```

### prototype을 사용한 생성자 함수 선언

```javascript
function <생성자 함수 이름>(){
	this.<속성이름>
	this.<속성이름>
}
<생성자 함수 이름>.prototype.<메서드이름>
```

1. 프로토타입을 안 쓸 경우
   생성자 함수 -> 속성 + 메서드 메모리 차지
   객체1 -> 속성 + 메서드 메모리 차지
   객체2 -> 속성 + 메서드 메모리 차지 ,,,

2. 프로토타입을 쓸 경우
   생성자 함수 -> 속성 메모리 차지
   객체1 -> 속성 메모리 차지
   객체2 -> 속성 메모리 차지 ,,,
   프로토타입 공간 -> 메서드 메모리 차지

### 캡슐화

실행엔 별 문제가 안된다 하더라도 개발자의 의도와 다르게 사용되는 경우가 있다.
속성과 메서드에 대한 접근에 제한을 둠으로써 그걸 방지하는 기법

```javascript
function Rectangle(w, h) {
  this.width = w;
  this.height = h;
}
Rectangle.prototype.getArea = function() {
  return this.width * this.height;
};
```

이렇게 사각형 생성자 함수를 짜놨는데

```javascript
var rectangle_1 = new Rectangle(5, -7);
```

변수에 "음수"가 들어가는건 물리적으로 말이 안된다!
다음과 같이 코드를 짜면 오류메세지를 출력하면서 그런 경우를 방지할 수 있다.

```javascript
function Rectangle (w,h){
	//this가 아닌 지역변수로 선언했기 때문에, 객체의 속성으로써는 접근이 불가함
	var width;
	var height;
	//통상적으로 set어쩌구 함수로 접근함
	this.setWidth(){
	if (w<0) {
		throw '길이는 음수일 수 없습니다.';
	} else {
		width = w;
	}
	};
	this.setHeight(){
	if (h<0){
		throw '길이는 음수일 수 없습니다.';
	} else {
		height = h;
	}
	};
	//통상적으로 get어쩌구 함수로 반환함
	this.getWidth = function(){ return width; };
	this.getHeight = function(){ return height; };
}
Rectangle.prototype.getArea = function(){
	return getWidth() * getHeight();
};
```

### 상속
위의 "사각형 생성자 함수"와 많이 유사한 "정사각형 생성자 함수"를 만들고 싶다.
```javascript
function Square(length){
	this.width = length;
    this.height = length;
}
Square.prototype.getArea = function(){
	return this.width*this.height;
};
```
캡슐화 하기 전의 코드면 이렇게 복붙+수정으로 끝날 수도 있지만
캡슐화까지 마친 코드라면 복붙+수정할 경우 줄이 길어지고 비효율적이므로
다음과 같이 상속 기법을 활용하자

```javascript
function Square(length){
	this.base = Rectangle; // base라는 속성에 생성자함수 넣어줌
	this.base(length, length); // 함수가 된 base속성을 실행
}
Square.prototype = Rectangle.prototype; // 프로토타입 복사
```
여기에서 Square.prototype.constructor() 메서드를 출력하면, 생성자함수 Square가 아니라 생성자함수 Rectangle을 가리킨다. 그대로 따왔기 때문이다.
그래서 Square.prototype의 생성자 함수를 Square(자기자신)으로 재정의해줘야 한다.

```javascript
Square.prototype.constructor = Square; // 프로토타입 복사 후 재정의
var square = new Square(5);
alert(square instanceof Rectangle);
```
만약 모든 상속과정이 잘 이루어 졌다면 true를 출력할것이다. 
이는 객체 square가 생성자 함수 Rectangle로부터 만들어졌음을 의미하고, 생성자 함수 Square가 Rectangle의 상속을 받았음을 의미한다.

## 기본 내장 객체

### 기본 자료형과 객체의 차이점
기본 자료형 - 자바스크립트의 6가지 자료형 중 숫자, 문자열, 불
1. 기본자료형으로 선언
var primitiveNumber = 273;
기본자료형이어서 속성이나 메서드가 없지만,
사용하려고하면 자동으로 객체로 변환이 되어 사용가능해짐
객체 자체는 아니기 때문에 속성과 메서드는 추가할 수 없음
2. 생성자함수를 사용하여 객체로 선언
var objectNumber = new Number(273);
속성과 메서드를 프로토타입으로 추가할 수 있음

### Object 객체
- 자바스크립트의 최상위 객체이자, Object 생성자 함수로 만든 인스턴스
- 자바스크립트의 모든 내장 객체는 Object 객체를 기본으로 만들어짐
- Object객체의 속성,메서드는 모든 객체에서 사용 가능하고,
- Object객체에 속성,메서드를 새로 추가하면 마찬가지로 모든 객체에서 사용 가능하다.
| 메서드                        | 기능                         |
| -------------------------- | -------------------------- |
| constructor()              | 객체의 생성자 함수를 나타냄            |
| hasOwnProperty(name)       | 객체가 name 속성이 있는지 확인        |
| isPrototypeof(object)      | 객체가 object의 프로토타입인지 검사     |
| propertyIsEnumerable(name) | 반복문으로 열거할 수 있는지 확인         |
| toLocaleString()           | 객체를 호스트 환경에 맞는 언어의 문자열로 바꿈 |
| toString()                 | 객체를 문자열로 바꿈                |
| valueOf()                  | 객체의 값을 나타냄                 |
    	
typeof 와 constructor() 자료형 구분

```javascript
var A = 273;
var B = new Number(273);
alert(typeof(A)); // number 출력
alert(typeof(B)); // object 출력
alert(A.constructor); // Number 출력
alert(B.constructor); // Number 출력
```
### Number 객체
Object객체의 7가지 메서드에, 3가지 메서드를 추가로 가짐

| 메서드             | 기능                                         |
| --------------- | ------------------------------------------ |
| toExponential() | 숫자를 지수 표시로 나타낸 문자열을 리턴                     |
| toFixed()       | 숫자를 고정 소수점 표시로 나타낸 문자열을 리턴                 |
| toPrecision()   | 숫자를 길이에 따라 지수 표시 또는 고정 소수점 표시로 나타낸 문자열을 리턴 |
    	
| 속성                | 기능                         |
| ----------------- | -------------------------- |
| MAX_VALUE         | 자바스크립트의 숫자가 나타낼 수 있는 최대 숫자 |
| MIN_VALUE         | 자바스크립트의 숫자가 나타낼 수 있는 최소 숫자 |
| NaN               | 자바스크립트의 숫자로 나타낼 수 없는 숫자    |
| POSITIVE_INFINITY | 양의 무한대 숫자                  |
| NEGATIVE_INFINITY | 음의 무한대 숫자                  |
    	
```javascript
var a = 123.12345;
alert(a.toFixed(2)); // 123.12출력
```

### String 객체
| 속성     | 기능         |
| ------ | ---------- |
| length | 문자열의 길이 반환 |

| 메서드                                 | 기능                             |
| ----------------------------------- | ------------------------------ |
| charAt(position)                    | position에 위치하는 문자를 리턴          |
| charCodeAt(position)                | position에 위치하는 문자의 유니코드 번호를 리턴 |
| concat(args)                        | 매개변수로 입력한 문자열을 이어서 리턴          |
| indexOf(searchString, position)     | 앞에서부터 일치하는 문자열의 위치를 리턴         |
| lastIndexOf(searchString, position) | 뒤에서부터 일치하는 문자열의 위치를 리턴         |
| match(regExp)                       | 문자열 안에 regExp가 있는지 확인          |
| replace(regExp, replacement)        | regEXP를 replacement로 바꾼 뒤 리턴   |
| search(regExp)                      | regExp와 일치하는 문자열의 위치를 리턴       |
| slice(start, end)                   | 특정 위치의 문자열을 추출해 리턴             |
| split(separator, limit)             | separator로 문자열을 잘라서 배열을 리턴     |
| substr(start, count)                | start부터 count만큼 문자열을 잘라서 리턴    |
| substring(start, end)               | start부터 end까지 문자열을 잘라서 리턴      |
| toLowerCase()                       | 문자열을 소문자로 바꾸어 리턴               |
| toUpperCase()                       | 문자열을 대문자로 바꾸어 리턴               |
    	
| HTML 관련 메서드            | 기능                                |
| ---------------------- | --------------------------------- |
| anchor()               | a 태그로 문자열을 감싸 리턴                  |
| big()                  | big 태그로 문자열을 감싸 리턴                |
| blink()                | blink 태그로 문자열을 감싸 리턴              |
| bold()                 | b 태그로 문자열을 감싸 리턴                  |
| fixed()                | tt 태그로 문자열을 감싸 리턴                 |
| fontcolor(colorString) | font 태그로 문자열을 감싸고 color 속성을 주어 리턴 |
| fontsize(fontSize)     | font 태그로 문자열을 감싸고 size 속성을 주어 리턴  |
| italics()              | i 태그로 문자열을 감싸 리턴                  |
| link(linkRef)          | a태그에 href 속성을 지정해 리턴              |
| small()                | small 태그로 문자열을 감싸 리턴              |
| strike()               | strike 태그로 문자열을 감싸 리턴             |
| sub()                  | sub 태그로 문자열을 감싸 리턴                |
| sup()                  | sup 태그로 문자열을 감싸 리턴                |

기본적으로 String 객체의 메서드는 자기 자신을 변화시키지 않고 리턴한다.
그래서 "메서드 체이닝"이 가능하다
string으로 return된 값은 string의 메서드를 다 가져다 쓸 수 있고,
만약 number로 return 된다면 number의 메서드를 다 가져다 쓸 수 있을것이다.
```javascript
var output = 'Hello';
output = output.toLowerCase().substring(0,10).anchor('name');
```
이런식으로 메서드 3개를 연속으로 사용할 수 있다.

### Array 객체

| 만드는 방법                | 상세 기능                  |
| --------------------- | ---------------------- |
| Array                 | 생성자 함수                 |
| Array()               | 빈 배열을 만듬               |
| Array(number)         | 매개변수만큼의 크기를 가지는 배열을 만듬 |
| Array(any, ... , any) | 매개변수로 배열을 만듬           |

그래서 배열은 총 4가지 방법으로 만들 수 있음
```javascript
var array1 = ['김', '용', '훈']
var array2 = new Array();
var array3 = new Array(10);
var array4 = new Array('김', '용', '훈');
```

| 속성     | 기능             |
| ------ | -------------- |
| length | 배열의 요소의 개수를 리턴 |
    	
| 메서드       | 기능                                 |
| --------- | ---------------------------------- |
| concat()  | 매개변수로 입력한 배열의 요소를 모두 합쳐 배열로 만들어 리턴 |
| join()    | 배열안의 모든 요소를 문자열로 만들어 리턴            |
| pop()     | 배열의 마지막 요소를 제거하고 리턴                |
| push()    | 배열의 마지막 부분에 새로운 요소를 추가             |
| reverse() | 배열의 요소 순서를 뒤집음                     |
| slice()   | 요소의 지정한 부분을 리턴                     |
| sort()    | 배열의 요소를 정렬                         |
| splice()  | 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴        |

- sort() 메서드 사용법
	기본적으로 "매개변수 두개를 받는 함수"가 매개변수로 들어간다.
	```javascript
	var array = [52, 273, 103, 32];
	array.sort( function(left, right){} );
	```

    매개변수로 입력한 함수가 리턴하는 숫자의 부호에 따라 정렬방식이 결정된다.
    ```javascript
	//오름차순 정렬
    array.sort( function(left, right){
    	return left - right;
    });
    //내림차순 정렬
    array.sort( function(left, right){
    	return right - left;
	});
	```
    객체로 이루어진 배열일때 이런식으로 활용가능 (= 총점을 정렬하기)
    ```javascript
    students = (student_A, student_B, student_C);
    students.sort(function(left, right){
    	return right.getSum() - left.getSum();
    });
	```
### Date 객체
생성자 함수에 매개변수를 입력하지 않으면 현재 시각으로 초기화
```javascript
var date = new Date();
alert(date); // 현재 시간 출력
```
매개변수를 입력하여 객체 생성
```javascript
1. 문자열을 사용
	var date = new Date('December 9, 1991');
	var date = new Date('December 9, 1991 02:24:23');
2. 숫자를 사용 = 연, 월-1, 일, 시, 분, 초, 밀리 초 순서로 입력하고 싶은데 까지 입력
	var date = new Date(1991, 11, 9);
	var date = new Date(1991, 11, 9, 2, 24, 23);
3. Unix time을 사용
	var date = new Date(2732741033257);
```

메서드
1. get~으로 시작하는 메서드 20가지정도
2. set~으로 시작하는 메서드 20가지정도
3. to~~String인 메서드 20가지정도

날짜 간격 구하기
```javascript
var now = new Date();
var before = new Date('January 22, 1994');
var interval = now.getTime() - before.getTime();
interval = Math.floor(interval / (1000*60*60*24) ); // = 9120(일)
```
날짜 간격 구하는 메서드를 프로토타입으로 추가하기
```javascript
Date.prototype.getInterval = ~~~~~~
```

### Math 객체
| 속성  |     |
| --- | --- |
+ E					2.718281828459045
+ LN2				0.6931471805599453
+ LN10			2.302585092994046
    	+ LOG2E		1.4426950408889633
    	+ LOG10E		0.4342944819032518
    	+ PI					3.141592653589793
    	+ SQRT1_2	0.7071067811865476
    	+ SQRT2		1.4142135623730951
    	++++++++++
    	+++메서드+++
    	+ random()			0부터 1까지의 임의의 수를 리턴
    	+ max(a,b,c,...,z)	가장 큰 값 리턴
    	+ min(a,b,c,...,z)	가장 작은 값 리턴
    	+ pow(x,y)			x의 y제곱
    	+ sqrt(x)				x의 제곱근을 리턴
    	+ abs(x)				x의 절댓값을 리턴
    	+ round(x)			x를 반올림하여 리턴
    	+ floor(x)				x보다 작거나 같은 가장 큰 정수를 리턴
    	+ celi(x)				x보다 크거나 같은 가장 작은 정수를 리턴
    	+ exp(x)				자연로그의 x 제곱을 리턴
    	+ log(x)				x의 로그값을 리턴
    	+ sin(x)				x의 사인 값을 리턴
    	+ asin(x)				x의 아크 사인 값을 리턴
    	+ cos(x)				x의 코사인 값을 리턴
    	+ acos(x)			x의 아크 코사인 값을 리턴
    	+ tan(x)				x의 탄젠트 값을 리턴
    	+ atan(x)				x의 아크 탄젠트 값을 리턴
    	+ atan2(y,x)		x와 y의 비율로 아크 탄젠트 값을 구해 리턴
    	++++++++++

    ECMAScript5 Array 객체
    	+++메서드+++
    	+ isArray()			매개변수가 배열인지 확인
    	+ indexOf()		매개변수를 배열의 앞쪽부터 검색, 위치를 리턴(없으면 -1 리턴)
    	+ lastIndexOf()	매개변수를 배열의 뒤쪽부터 검색, 위치를 리턴(없으면 -1 리턴)
    	+ forEach()		배열 각각의 요소를 사용해 특정 함수를 for in 반복문처럼 실행
    	+ map()			기존의 배열에 특정 규칙을 적용해 새로운 배열을 만듬
    	+ filter()			특정 조건을 만족하는 요소를 추출해 새로운 배열을 만듬
    	+ every()			배열의 요소가 특정 조건을 모두 만족하는지 확인
    	+ some()			배열의 요소가 특정 조건을 적어도 하나 만족하는지 확인
    	+ reduce()		배열의 요소가 하나가 될 때까지 요소를 왼쪽부터 두 개씩 묶는 함수를 실행
    	+ reduceRight()	배열의 요소가 하나가 될 때까지 요소를 오른쪽부터 두 개씩 묶는 함수를 실행
    	++++++++++
    	indexOf() 메서드 예시
    		var array = {1,2,3,4,5,5,4,3,2,1};
    		var output1 = array.indexOf(4); // = 4
    		var output2 = array.indexOf(10); // = -1
    		var output3 = array.lastIndexOf(4); // = 6
    		var output4 = array.lastIndexOf(10); // = -1
    	forEach() 메서드 예시 // 매개변수로 함수가 들어감
    		var array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    		var sum = 0;
    		var output = '';
    		array.forEach( function(element, index, array){
    			sum += element;
    			output += index + ': ' + element + ' -> ' + sum + '\n';
    		});
    	map() 메서드 예시 // 매개변수로 함수가 들어감
    		var array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    		var output = array.map(function (element) {
    			return element * element;
    		}); // 배열이 제곱수로 바뀜 1,4,9, ...
    	filter() 메서드 예시 // 매개변수로 함수가 들어감
    		var array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    		array = array.filter(function(element, index, array){
    			return element <= 5; // 불 자료형으로 리턴함
    		}); // 트루로 리턴된것만 골라 배열 형성
    	every() 메서드와 some() 메서드 예시 // 매개변수로 함수가 들어감
    		var array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    		function lessThanFive(element, index, array){
    			return element < 5; // 불 자료형으로 리턴함
    		}
    		var output1 = array.every(lessThanFive); // false반환
    		var output2 = array.some(lessThanFive); // true반환
    	reduce() 메서드와 reduceRight() 메서드 예시 // 매개변수로 함수가 들어감
    		var array = {1,2,3,4,5};
    		var output = "";
    		array.reduce(function(previousValue, currentValue, index, array){
    			output += previousValue + ":" +currentValue + ":" + index + \n;
    		});
    			reduce()메서드 결과(묶인 건 자료형을 알 수 없으니 undefined)
    			1	:	2	:	1
    			undefined	:	3	:	2
    			undefined	:	4	:	3
    			undefined	:	5	:	4
    			나머지 다 같고 reduce()대신 reduceRight()로 돌린 결과
    			5	:	4	:	3
    			undefined	:	3	:	2
    			undefined	:	2	:	1
    			undefined	:	1	:	0
    	reduce() 메서드 활용
    		var array = {1,2,3,4,5};
    		var resulut = array.reduce(function(previousValue, currentValue){
    			return previousValue + currentValue;
    		}); // 15출력

    ECMAScript5 String 객체
    	+++메서드+++
    	+ trim()	문자열 양쪽 끝의 공백을 제거
    	++++++++++

    JSON객체
    	JSON이란 자바스크립트 객체 형태를 갖는 문자열
    	+++메서드+++
    	+ JSON.stringify()	자바스크립트 객체를 JSON 문자열로 변환
    	+ JSON.parse()	JSON 문자열을 자바스크립트 객체로 변환
    	++++++++++
    	객체의 속성을 출력하려면 for in 반복문을 사용하거나 JSON.stringify()메서드를 사용
    		var person = {
    			name : "김용훈",
    			age : "20"
    		};
    		alert(JSON.stringify(person)); // {"name":"김용훈", "age":"20"} 출력
    	JSON.stringify() 사용시 객체 안에 toJSON() 메서드가 없다면 객체 전체를 JSON으로 변환
    	toJSON() 메서드가 있다면 toJSON()의 리턴값만을 JSON으로 변환
    		var person ={
    			name : "김용훈",
    			age : "20",
    			toJSON : function(){
    				return {
    					fact : "이것만변환됨"
    				};
    			}
    		}
    		alert(JSON.stringify(person)); // {"fact":"이것만변환됨"} 출력

    underscore 라이브러리
    	배열에서 정렬과 같은 기본적인 유틸리티 기능을 모아놓음
    	자세한 사용법은 공식 홈페이지 참조
    		sort : 정렬
    		trim : 문자열 양 옆의 글자를 자름
    		shuffle : 배열 내용을 랜덤으로 섞음
    		sample : 요소를 랜덤으로 몇 개 뽑아줌
    		등등

#####

브라우저 객체 모델

#####

    Browser Object Model = BOM = 웹 브라우저와 관련된 객체 집합 = 브라우저(플랫폼)에서 제공하는 기능
    window 객체
    	>location 객체
    		= 주소와 관련된 객체
    	>navigator 객체
    		= 웹 브라우저와 관련된 객체
    	>history 객체
    		= 기록과 관련된 객체
    	>screen 객체
    		= 화면 전체와 관련된 객체
    	>document 객체
    		DOM = Document Object Model = HTML문서와 관련된 객체
    여기서 DOM을 제외한 5가지 객체의 집합을 BOM이라고 한다.

    window 객체
    	브라우저 기반 최상위 객체
    	alert(), prompt() 함수 모두 window 객체의 메서드임 (이래서 JS에서 함수나 메서드 구분은 의미가 없음)
    	var 선언한 일반 변수는 모두 window 객체의 속성이 됨
    		예시 : var test = 123; alert(window.test); //123출력
    	새로운 윈도우 객체를 생성하는 메서드 : open()메서드
    		기본 형태 : open(URL, name, features, replace);
    		open()메서드의 모든 매개변수는 옵션임 (입력해도 되고 안해도 됨)
    			모든 옵션 다 사용하면 : window.open("http://hanbit.co.kr", "child", "width=600, height=300", true);
    			2번째 매개변수 : 윈도우 간 통신하는 데 사용하는 윈도우 이름
    			3번째 매개변수에 사용되는 옵션 : 옵션 // 설명 // 입력할 수 있는 값
    				height // 새 윈도우의 높이 // 픽셀 값
    				width // 새 윈도우의 너비 // 픽셀 값
    				location // 주소 입력창의 유무 // yes, no, 1, 0
    				menubar // 메뉴의 유무 // yes, no, 1, 0
    				resizable // 화면 크기 조절 가능 여부 // yes, no, 1, 0
    				status // 상태 표시줄의 유무 // yes, no, 1, 0
    				toolbar // 상태 표시줄의 유무 // yes, no, 1, 0
    		open()메서드는 단지 팝업창을 여는 것 뿐아니라 윈도우 객체를 리턴
    			var child = window.open("", "", "width = 300, height = 200");
    			child.document.write("<h1>생성된 객체에 이 문장이 들어감</h1>");
    		팝업 차단 검사
    			var child = window.open("", "", "width = 300, height = 200");
    			if (child) {
    				child.document.write("<h1>생성된 객체에 이 문장이 들어감</h1>");
    			} else{
    				alert("팝업차단을 해제하세요");
    			}
    	+++메서드+++
    	+ moveBy(x,y)	윈도우의 위치를 상대적으로 이동
    	+ moveTo(x,y)	윈도우의 위치를 절대적으로 이동
    	+ resizeBy(x,y)	윈도우의 크기를 상대적으로 지정
    	+ resizeTo(x,y) 윈도우의 크기를 절대적으로 지정
    	+ scrollBy(x,y) 윈도우 스크롤의 위치를 상대적으로 이동
    	+ scrollTo(x,y)	윈도우 스크롤의 위치를 절대적으로 이동
    	+ focus()	윈도우에 초점을 맞춤
    	+ blur()	윈도우에 맞춘 초점을 제거
    	+ close()	윈도우를 닫음
    	++++++++++
    		움직이는 팝업창 (1초마다 왼쪽으로 10, 아래로 10 이동)
    			var child = window.open("", "", "width=300, height=200");
    			child.moveTo(0,0);
    			setInterval(function(){
    				child.moveBy(10, 10);
    			}, 1000);
    	window 객체의 onload 이벤트 속성
    		on으로 시작하기 때문에 그냥 속성이 아닌 이벤트 속성임
    		window.onload = function(){}
    			HTML페이지에 존재하는 모든 태그가 화면에 올라가는 순간
    			(= 로드가 완료되는 순간)
    			-> 함수 실행
    location 객체
    	+++속성+++
    	+ href	문서의 URL 주소
    	+ host	호스트 이름과 포트 번호 // localhost:30763
    	+ hostname	호스트 이름 // localhost
    	+ port	포트 번호 // 30763
    	+ pathname	디렉토리 경로 // /Projects/Location.htm
    	+ hash	앵커 이름(#~) // #beta
    	+ search	요청 매개변수 // ?param = 10
    	++++++++++
    	+++메서드+++
    	+ assign(link)	현재 위치를 이동
    	+ reload()	새로고침
    	+ replace(link)	현재 위치를 이동
    	++++++++++
    		location 객체로 페이지를 이동하는 4가지 방법
    			location = "http://hanbit.co.kr";
    			location.href = "http://hanbit.co.kr";
    			location.assign("http://hanbit.co.kr");
    			location.replace("http://hanbit.co.kr"); // assign과는 다르게 뒤로가기 불가
    		location 객체로 페이지를 새로고침 하는 5가지 방법
    			location = location;
    			location.href = location.href;
    			location.assign(location);
    			location.replace(location);
    			location.reload();
    navigator 객체
    	+++속성+++
    	+ appCodeName	브라우저의 코드 이름
    	+ appName	브라우저의 이름
    	+ appVersion	브라우저의 버전
    	+ platform	사용 중인 운영체제의 시스템 환경
    	+ userAgent	웹 브라우저의 전체 정보
    	++++++++++
    screen 객체
    	+++속성+++
    	+ width	화면의 너비
    	+ height	화면의 높이
    	+ availWidth	실제 화면에서 사용 가능한 너비
    	+ availHeight	실제 화면에서 사용 가능한 높이
    	+ colorDepth	사용 가능한 색상 수
    	+ pixelDepth	한 픽셀당 비트 수
    	++++++++++
    	화면의 크기에 브라우저를 일치시키는 방법
    		var child = window.open("", "", "width=300, height=200");
    		var width = screen.width;
    		var height = screen.height;
    		child.moveTo(0,0);
    		child.resizeTo(width, height);
    Audio 객체
    	+++속성+++
    	+ src	음악 파일의 경로
    	+ volume	소리 크기
    	+ currentTime	현재 위치(초 단위)
    	++++++++++
    	+++메서드+++
    	+ play()	재생
    	+ pause()	일시 정지
    	++++++++++
    	객체 생성
    		var audio = new Audio("music/kalimba.mp3");
    		아니면 생성자 함수에서 src를 지정 안하고 별도로 지정해도 됨
    		var audio = new Audio();
    		audio.src = "music/kalimba.mp3";
    	간단한 재생 프로그램
    		<script>
    			var audio = new Audio("music/kalimba.mp3");
    		</script>
    		<body>
    			<button onclick="audio.play()">재생</button>
    			<button onclick="audio.pause()">일시정지</button>
    			<input type="number" onchange="audio.currentTime=this.value"/> //재생 위치
    			<input type="number" onchange="audio.volume=this.value"/> //볼륨
    		</body>
    모바일 장치 구분
    	2가지 방법이 있음 : 서버에서 확인 or 클라이언트에서 확인
    	-> 2가지 방법 모두 userAgent이용
    		var userAgent = navigator.userAgent;
    		alert(userAgent);
    	userAgent속성에 브라우저를 구분할 수 있는 고유한 문자열이 있음
    		iPhone, iPod, iPad, Android, WebOS 등등
    	또 카톡, 페북에서 링크를 클릭하면 KAKAOTALK등의 문자열이 있음
    	스마트폰 구분 코드
    		var smartPhones = ["iphone", "ipod", "android"];
    		for (var i in smartPhones) {
    			if(navigator.userAgent.toLowerCase().match(new RegExp(smartPhones[i]))){
    				alert("모바일 페이지로 전환합니다");
    				location = "http://m.hanbit.co.kr";
    			}
    		}
    모바일 장치의 방향
    	<script>
    		if(window.orientation==0||window.orientation==180){
    			alert("세로 방향입니다");
    		}else if(window.orientation==90||window.orientation==-90){
    			alert("가로 방향입니다");
    		}
    	</script>

#####

문서 객체 모델

#####

    노드, 문서객체, 문서객체모델 용어 정리
    	<!DOCTYPE html>
    		<html>
    		<head>
    			<title>index</title>
    			<script></script>
    		</head>
    		<body>
    			<h1 id = "header">HEADER</h1>
    		</body>
    	</html>
    	==>트리 구조로 나타내면 다음과 같음
    		+++++트리 그림+++++
    		+	html	->head	->title	->"index"
    		+					->script
    		+			->body	->h1	->"HEADER"
    		++++++++++
    		==> 이 트리 그림을 문서객체 모델이라고 함
    		==> 각각은 노드라고 함, ""는 텍스트 노드, 나머지는 요소 노드

    	<script>
    		window.onload = function(){
    			var header = document.getElementById("header");
    		};
    	</script>
    	==> 객체 header를 문서객체라고 함(정적으로 생성된 문서 객체)

    정적으로 문서 객체 생성
    	HTML페이지에 적혀있는 태그를 읽으며 생성
    동적으로 문서 객체 생성
    	자바스크립트로 원래 HTML페이지에 없던 문서객체를 생성
    	+++document 객체의 (노드 생성)메서드+++
    	+ createElement(tagName)	요소노드를 생성
    	+ createTextNode(text)	텍스트 노드를 생성
    	++++++++++
    	+++문서 객체의 (노드 연결)메서드+++
    	+ appendChild(node)	객체에 노드를 연결
    	++++++++++
    	<script>
    		window.onload = function(){
    			var header = document.createElement("h1"); //<h1>태그 생성
    			var textNode = document.createTextNode("Hello DOM"); //"Hello DOM"문자열 생성

    			//노드를 연결(후손부터 오름차순으로)
    			header.appendChild(textNode);
    			document.body.appendChild(header);
    		};
    	</script>

    텍스트 노드를 갖지 않고, 속성을 가지는 노드 생성
    	<script>
    		window.onload = function(){
    			var img = document.createElement("img");
    			img.src = 'img/flower.jpg';
    			img.width = 500px;
    			img.height = 300px;

    			document.body.appendChild(img);
    		};
    	</script>
    	이 방법이 안되는 경우(웹표준에서 정의X, 웹브라우저가 지원X)엔 메서드를 사용해야 한다.
    		+++문서 객체의 (속성 관련)메서드+++
    		+ setAttribute(name, value)	객체의 속성을 지정
    		+ getAttribute(name)	객체의 속성을 가져옴
    		++++++++++
    		<script>
    			var img = document.createElement('img');
    			setAttribute('user-property' 200); //웹표준에 없는 속성
    			setAttribute('src', 'myImage.jpg'); //웹표준에 있는 속성도 사용가능
    		</script>

    노드 생성과 연결
    	+++문서 객체의 (노드 생성+연결) 속성+++
    	+ innerHTML	객체 하위에 (태그를 고려하여) 노드 생성 및 연결
    	+ textContent	객체 하위에 (태그를 고려하지 않고) 텍스트 노드 생성 및 연결
    	++++++++++
    	어디까지나 속성이므로 "문서객체.속성 = 속성값" 형태로 사용한다
    		<script>
    		var output = "<h1>1째줄</h1><br>";
    		output += "<h1>2째줄</h1>";
    		document.body.innerHTML = output;
    		document.body.textContent = output; //태그도 문자처럼 그대로 출력
    		</script>

    문서 객체 가져오기
    	+++문서 객체 선택 메서드+++
    	+ document.getElementById('아이디') - 아이디를 사용해 문서 객체 선택
    	+ document.getElementsByName('이름') - name속성으로 여러 개의 문서 객체 선택
    	+ document.getElementsByClassName('클래스') - class속성으로 여러 개의 문서 객체 선택
    	+ document.getElementsByTagName('이름') - tagName 매개변수와 일치하는 문서 객체 선택
    	+ document.querySelector('선택자') - 선택자를 사용해 가장 처음 선택된 문서 객체 선택
    	+ document.querySelectorAll('선택자') - 선택자로 여러 개의 문서 객체 선택
    	++++++++++
    	여러개의 문서객체가 선택되는 메서드에서는
    		var divs = document.~~으로 선택하고 divs[0], divs[1], ... 로 불러온다.
    		for in 반복문은 쓸 수 없다. divs[0], divs[1]까지 2개 있다고 하면
    			for (var i n divs) {
    				output += i +'\n' ;
    			}
    			alert(output);
    			-> 0 1 length item nameditem 등등 문서객체이외의 속성에도 접근한다.
    		그래서 단순 for 반복문만 써야 한다.

    문서 객체의 스타일 조작
    	문서 객체의 style속성으로 스타일을 조작할 수 있다.
    		<script>
    		var 객체 = document.getElementById("객체");
    		객체.style.border = "2px solid black";
    		객체.style.color = "orange";
    		객체.style.fontFamily = "helvetica";
    		객체.style.backgroundColor= "red";
    		</script>
    	스타일시트에 사용하던 스타일 속성 이름을 그대로 사용하면 안됨
    	(자바스크립트는 -를 식별자에 사용할 수 없으므로 -다음 첫 글자를 대문자로)
    		font-family background-color: X
    		fontFamily backgroundColor: O
    	대신 문자열로 스타일 속성에 접근할 때는 두가지 방법 모두 가능
    		객체.style['font-family'] = 'red';
    		객체.style['fontFamily'] = 'red';

    문서 객체 제거
    	+++메서드+++
    	+ removeChild(child)	문서 객체의 자식 노드를 제거
    	++++++++++
    	<script>
    		var parent = document.getElementById("parent");
    		var child = document.getElementById("child");
    		parent.removeChild(child); //이런식으로 사용
    	</script>

#####

이벤트

#####

    ex) onscroll, onclick, onkeydown, onkeypress, onkeyup, onchange, ...
    ex) window.onload = function(){}
    	이벤트를 연결한다 : window객체의 onload속성에 함수자료형을 할당하는 것
    	load : 이벤트 이름 or 이벤트 타입
    	onload : 이벤트 속성(실제로 on으로 시작하는 모든 html의 속성은 이벤트 속성)
    	이벤트 속성에 할당된 함수 : 이벤트 리스너 or 이벤트 핸들러

    이벤트를 연결하는 방법 = 이벤트 모델
    	DOM Level 0
    		인라인 이벤트 모델
    		기본(고전) 이벤트 모델
    	DOM Level 2
    		마이크로소프트 인터넷 익스플로러 이벤트 모델
    		표준 이벤트 모델
    	level0은 방법이 쉽지만 이벤트를 중복해서 연결 불가
    	level2는 이벤트를 중복해서 연결할 수 있지만 브라우저 종류에 따라 방법이 다름
    	==> 이 단점들은 jquery를 통해 모두 커버 가능!

    DOM LEVEL0 - 기본(고전) 이벤트 모델
    	<script>
    		var image = document.getElementById('image');
    		image.width = 100;
    		image.height = 100;
    	</script>
    	HTML 표준에 속한 태그의 속성은 모두 이렇게 사용할 수 있다.
    	이벤트 속성도 속성의 일종이므로 역시 마찬가지다.
    	대신에 이벤트 속성에는 함수를 지정하는 것이다.
    	이때 지정됨 함수 = 이벤트 핸들러 = 이벤트 리스너
    	단, 이벤트 하나에 이벤트 리스너 하나만 연결할 수 있음
    		<script>
    			window.onload = function(){
    				var header = document.getElementById('kyh');
    				header.onclick = function(){
    					alert("클릭됨");
    				}
    			};
    		</script>
    		<body>
    			<h1 id="kyh">Click</h1>
    		</body>
    	이벤트를 일회성으로 하고 싶다면 이벤트 리스너를 null로 바꾸면 됨
    	다음 코드에서 함수는 한번 실행되고 소실됨
    		<script>
    			window.onload = function(){
    				var header = document.getElementById('kyh');
    				header.onclick = function(){
    					alert("클릭됨");
    					header.onclick = null;
    				};
    			};
    		</script>

    이벤트 발생 객체(<->이벤트 객체)
    	이벤트를 누가 발생시켰는지, 그 객체를 의미함
    	이벤트 리스너 안에서 this 키워드를 사용해서 확인
    		<script>
    			window.onload = function(){
    				document.getElementById('kyh').onclick = function(){
    					alert(this);
    				};
    			};
    		</script>
    		<body>
    			<h1 id="kyh">Click</h1>
    		</body>
    			==> object HTMLHeadingElement 출력(이벤트가 발생한 문서 객체 kyh)
    	그래서 이벤트 리스너 안에서 this키워드의 스타일을 바꾸는 것은 이벤트가 발생한 객체의 스타일을 바꾸는 것
    		<script>
    			window.onload = function(){
    				document.getElementById('kyh').onclick = function(){
    					this.style.color = 'orange';
    					this.style.backgroundColor = 'red';
    				};
    			};
    		</script>
    			==>h1의 글씨와 배경이 주황+빨강으로 바뀜

    이벤트 객체
    	이벤트의 '누가'와 관련된 정보외의 다른 정보가 있음
    		<script>
    			window.onload = function(){
    				document.getElementById('header').onclick = function(e){
    					//IE8 이하는 인터넷 익스플로러 이벤트 모델이라는 독자적인 이벤트 모델 사용하기 때문에 이벤트 객체를 window.event속성으로 사용
    					//나머지 브라우저는 이벤트 객체로 이벤트 리스너의 매개변수로 사용
    					//IE9 이상은 이벤트 객체로 둘 다 사용 가능
    					var event = e || window.event;

    					document.body.innerHTML = "";
    					for (var key in event) {
    						document.body.innerHTML += '<p>' + key + ':' + event[key] + '</p>';
    					}
    				};
    			};
    		</script>
    			==>이벤트에 관한 정보들이 다 출력됨

    이벤트 강제 실행(많이 안 씀)
    	header.onclick = function(){}; 이벤트 속성에 이벤트 리스너가 정의되어 있으면
    	header.onclick(); 이벤트 속성을 메서드처럼 호출해버리면 이벤트가 강제 실행됨

    DOM LEVEL0 - 인라인 이벤트 모델
    	태그에 이벤트 속성을 부여, 이벤트 속성에 JS 코드를 적어줌
    	이벤트 발생 시 JS 코드 실행
    		<body>
    			<h1 onclick="alert(클릭);">Click</h1>
    		</body>
    	여러 줄을 한번에 적을 수도 있음
    		<body>
    			<h1 onclick="var ten=10; alert(ten);">Click</h1>
    		</body>
    	하지만 이러면 지저분하니 script에 다 적어두고 호출하는 방식 사용
    		<script>
    			var waitTen = function(e){
    				var ten = 10;
    				alert(ten);
    			}
    		</script>
    		<body>
    			<h1 onclick = "waitTen(event);">Click</h1>
    		<body>

    디폴트 이벤트 제거
    	일부 HTML태그는 이미 이벤트 리스너가 있음.
    		ex)onclick을 이벤트 속성으로 가지는 태그들.. <a>, <submit>, ...
    	평범한 <form>태그
    		<body>
    			<form id = "my-form">
    				<label for = "name">이름</label><br/>
    				<input type="text" name="name" id="name" /><br/>
    				<label for = "pass">비밀번호</label><br/>
    				<input type="password" name="pass" id="pass" /><br/>
    				<label for = "pass-check">비밀번호-확인</label><br/>
    				<input type="password" name="pass-check" id="pass-check" /><br/>
    				<input type="submit" value="제출" />
    			</form>
    		</body>
    	디폴트 이벤트 제거
    		<script>
    			window.onload = function(){
    				document.getElementById('my-form').onsubmit = function(){
    					return false;
    				}
    			}
    		</script>
    		-> 디폴트 이벤트가 제거됐으므로 submit을 눌러도 제출이 안됨
    	유효성 검사(= 특정 조건에서만 디폴트 이벤트를 제거)
    		<script>
    			window.onload = function(){
    				document.getElementById('my-form').onsubmit = function(){
    					var pass = document.getElementById('pass').value;
    					var pass_check = document.getElementById('pass_check').value;

    					if (pass==pass_check){
    						alert("비밀번호가 일치합니다");
    					}
    					else if{
    						alert("비밀번호가 불일치합니다");
    						return false;
    					}
    				}
    			}
    		</script>
    	인라인 이벤트 모델의 유효성 검사
    		고전 이벤트 모델은 return false를 입력했다면
    		인라인 이벤트 모델은 form 태그의 onsubmit 속성에 "return 함수()" 형태로 입력
    		<script>
    			function whenSubmit(){
    				//(유효성 검사)
    				return false;
    			}
    		</script>
    		<form onsubmit = "return whenSubmit()"> ~~ </form>

    이벤트 전달
    	다수의 이벤트가 동시에 발생할 경우, 이벤트 전달을 2가지 방식으로 한다.
    		이벤트 버블링 : 자식노드에서 부모노드 순으로 이벤트 실행
    		이벤트 캡쳐링(안씀) : 부모노드에서 자식노드 순으로 이벤트 실행
    		<head>
    			<style>
    				*{ border : 3px solid black; }
    			</style>
    		</head>
    		<body>
    			<div onclick="alert('outer-div')">
    				<div onclick="alert('inner-div')">
    					<h1 onclick="alert('header')">
    						<p onclick="alert('paragraph')">Paragraph</p>
    					</h1>
    				</div>
    			</div>
    		</body>
    		-> p태그를 클릭하면 4개의 태그가 동시에 클릭되고, 4개의 이벤트가 동시에 발생
    	이벤트 전달 막기
    		이벤트 버블링 예시
    			<script>
    				window.onload = function(){
    					document.getElementById('header').onclick = function(){
    						alert('header');
    					};
    					document.getElementById('paragraph').onclick = function(){
    						alert('paragraph');
    					};
    				};
    			</script>
    			<body>
    				<h1 id ="head">
    					<p id="paragraph">Paragraph</p>
    				</h1>
    			</body>
    			-> 이벤트 버블링에 의하여 paragraph -> header 순으로 경고창 출력
    		이벤트 버블링 막기
    			인터넷 브라우저 : 이벤트 객체의 cancelBubble속성을 true로 변경
    			타 브라우저 : 이벤트 객체의 stopPropagation()메서드 사용
    				<script>
    					document.getElementById('paragraph').onclick = function(e){
    						//이벤트 객체 처리
    						var event = e || window.event;
    						//이벤트 발생 알림
    						alert('paragraph');
    						//이벤트 전달을 제거
    						event.cancelBubble = true;
    						if(event.stopPropagation){
    							event.stopPropagation();
    						}
    					};
    				</script>
    				-> 인터넷 익스플로러는 이벤트 객체에 stopPropagation() 메서드가 없어서 조건문으로 에러 방지
    				그 외 브라우저도 cancleBubble속성에 값만 넣는 거라 가능할 뿐 속성을 사용하려면 문제가 생길 수 있음

    DOM LEVEL2 - 인터넷 익스플로러 이벤트 모델
    	attachEvent(eventProperty, eventListener);
    	detachEvent(eventProperty, eventListener);
    	window 객체에 load 이벤트를 연결한다면
    		window.attachEvent('onload', function(){
    		});
    	DOM LEVEL2 이벤트 모델이 DOM LEVEL0 이벤트 모델보다 나은 점은 여러번 이벤트를 추가할 수 있다는 점
    		<script>
    			var header = document.getElementById("my-header");
    			header.attachEvent('onclick', function(){alert('1');});
    			header.attachEvent('onclick', function(){alert('2');});
    			header.attachEvent('onclick', function(){alert('3');});
    		</script>
    		-> 3, 2, 1 순으로 출력
    	이벤트를 제거할 때 사용하는 detachEvent에서 eventListener는 익명함수를 사용할 수 없다.
    	어떤 이벤트 리스너를 제거할지 명시해야한다.(같은 모양의 익명함수를 넣어도 안된다)
    		<script>
    			var header = document.getElementById("my-header");
    			var handler = function(){alert("클릭");};
    			header.attachEvent("onclick", handler);
    			header.detachEvent("onclick", handler); //연결하자마자 제거됨
    		</script>
    	이벤트 리스너의 this 키워드는 이벤트 발생 객체를 의미하지 않고, window객체를 의미한다.
    	이벤트 발생 객체를 사용하려면 이벤트 객체의 srcElement 속성을 사용해야함
    	IE에서만 실행가능하므로 다음과 같이 쓴다
    		<script>
    			window.onload = function(){
    				var header = document.getElementById("my-header");
    				if(header.attachEvent){
    					var handler = function(){
    						window.event.srcElement.style.color = "red";
    						window.event.srcElement.detachEvent("onclick", handler);
    					};
    					header.attachEvent("onclick", handler);
    				}
    			};
    		</script>

    DOM LEVEL2 - 표준 이벤트 모델
    	웹 표준 단체 W3C에서 공식적으로 지정함
    	IE모델과 마찬가지로 이벤트 하나에 여러 가지 이벤트 리스너 추가
    	IE모델과 달리 이벤트 캡쳐링을 지원(잘 안씀)
    	인터넷 익스플로러는 9버전부터 지원(8버전 이하에서 사용 불가)
    	+++메서드+++
    	+ addEventListener(eventName, handler, userCapture)
    	+ removeEventListener(eventName, handler)
    	++++++++++
    		eventName에는 단순 이벤트 이름이 들어감
    		userCapture는 입력하지 않으면 자동으로 false를 입력함
    		표준 이벤트 모델은 IE 이벤트 모델과 달리 this키워드가 이벤트 발생 객체를 의미함
    		<script>
    			var header = document.getElementById("my-header");
    			addEventListener("click", function(){
    				this.innerHTML += "+";
    			);
    		</script>
    	removeEventListener() 메서드는 표준 이벤트 모델의 detachEvent() 메서드와 사용법이 똑같음

    DOM LEVEL2 이벤트 모델의 통합적 사용
    	<script>
    		var header = document.getElementById("my-header");
    		if(heaaer.attachEvent){
    			var handler = function(){
    				window.event.srcElement.style.color = "red";
    				window.event.srcElement.detachEvent("onclick", handler);
    			};
    			header.attachEvent("onclick", handler);
    		} else{
    			var handler = function(){
    				this.syle.color = "red":
    				this.removeEventListener("click", handler);
    			};
    			header.addEventListener("click", handler);
    		}
    	</script>

#####

예외 처리

#####

    기본 예외 처리
    	예외가 발생하지 않게 사전에 해결하는 것(if문으로 경우의 수 고려)

    고급 예외 처리
    	try {
    	} catch (exception){
    	} finally {
    	}
    고급 예외 처리 예시
    	try {
    		alert("이 부분은 일단 실행됨");
    		notExist.noExist(); // 없는 객체의 없는 메서드 실행 = 에러 -> catch로 점프
    		alert("이 부분은 점프 되서 실행 안됨");
    	} catch (exception){
    		alert("에러가 잡혔을 경우 이 부분 실행");
    	} finally {
    		alert("어찌 되었든 이 부분은 결국 실행됨");
    	}

    예외 객체
    	catch의 괄호안에 입력하는 식별자 (exception, e로 쓰임)
    	타 언어에 비해 활용하는 경우가 적음
    	+++속성+++
    	+ message	예외 메시지
    	+ description	예외 설명
    	+ name	예외 이름
    	++++++++++
    		<script>
    			try {
    				var array = new Array(999999999999); //배열의 크기는 한정되어 있으므로 예외 발생시킴
    			} catch (exception) {
    				var output = "";
    				for (var i in exception){
    					output += i + ":" + exception[i] + "\n";
    				}
    				alert(output);
    			}
    		</script>
    		+++출력+++
    		description : 배열의 길이는 유한한 정수이어야 합니다.
    		number : -2146823259
    		stack : RangeError : 배열의 길이는 유한한 양의 정수이어야 합니다.
    			at Global code (http://localhost:56926/HTMLPage1.html:1:26)
    		++++++++++

    에러와 예외
    	예외 : try-catch 구문으로 해결할 수 있음
    	에러 : try-catch 구문으로 해결할 수 없음(문법 오류 같은 것)
    	에러의 예시
    		<script>
    			try{
    				error+-error+++; //없는 syntax여서 컴파일 안됨
    			}catch(exception){
    				alert("EXCEPTION!"); //예외처리가 제대로 안됬으므로 경고창 출력X
    			}
    		</script>

    예외 강제 발생
    	throw 키워드
    		<script>
    			throw "CUSTOM EXCEPTION OCCUR"; //오류 창 출력
    		</script>
    		오류메시지에 입력한 문자열 출력
    		사용자에게 주의 및 예외와 관련된 처리를 부탁할 수 있음
    	강제로 발생시킨 예외 처리1
    		<script>
    			try{
    				throw "DivideByZeroException"; //예외 발생함 -> catch실행
    			}catch(exception){
    				if(exception=="DivideByZeroException"){
    					alert("ㅇㅁㅇ");
    				}
    			}
    		</script>
    		문자열 "DivideByZeroException"으로 예외를 발생시켰으므로
    		이를 사용해 예외의 종류를 구분할 수 있음
    	강제로 발생시킨 예외 처리2(자주 사용하는 방식)
    		자바스크립트에서는 0으로 나눈다고 문제가 되진 않지만
    		개발자가 그런 상황을 막고 싶을 경우
    		<script>
    			function divide(alpha, beta){
    				if(beta==0){
    					throw "DivideByZeroException";
    				}else{
    					return alpha/beta;
    				}
    			}
    			try{
    				divide(10,0); //예외발생함
    			}catch(exception){
    				alert("CATCH"); //실행
    			}
    		</script>

    try catch finally 구문에서 finally 를 쓰는 이유
    	finally 가 없는 경우
    		<script>
    			function test(){
    				try{
    					alert("A"); //출력됨
    				}catch(exception){
    					alert("B"); //출력됨
    					return; //함수 종료
    				}
    				alert("C"); //종료되서 출력X
    			}
    			test();
    		</script>
    	finally 가 있는 경우
    		<script>
    			function test(){
    				try{
    					alert("A"); //출력됨
    				}catch(exception){
    					alert("B"); //출력됨
    					return; //함수 종료이지만
    				}finally{
    					alert("C"); //구문 특성상 출력됨
    				}
    			}
    			test();
    		</script>
    	이처럼 return, break, continue 키워드 등은 try catch 문에서 사용할 경우 코드가 꼬이게 된다.
    	그래서 일부 프로그래밍 언어는 catch 구문에서 return 키워드 등을 금지하고 finally 구문의 기능을 하는 것이 없는 경우도 있다.

```
> 윤인성 선생님의 Javascript 저서를 참고했습니다.
```
