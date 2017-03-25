# JavaScript에 대해 이해해보자 (Part 2)
오늘 수업에서는 JavaScript의 더 복잡한 개념에 대해 이해해봅시다.
1. statement & expression
2. scope
3. this

추가로 오늘은 컴포넌트들을 구현해봅시다.
1. Tab Menu
2. Scrollspy (**position:sticky**)
3. Carousel (do your self)

## Statement & Expression (문 & 식)
### Statement
값을 반환하지 않는 것
```
var age = 10;
```

#### if 문
**만약**, 조건이 맞다면 A를 실행시키고 아니라면 B를 실행시킨다.

Example
```
if(chicken === 'delicious') {
  order(chicken);
} else {
  order(pizza);
}
```

구성
```
if(조건문) {
  // 조건문이 true를 반환할 경우
} else {
  // 조건문이 false를 반환할 경우
}

if(조건문1) {
  // 조건문1이 true를 반환할 경우
} else if(조건문2) {
  // 조건문1이 false를 반환할 경우
  // 조건문2가 true를 반환할 경우
} else {
  // 조건문1이 false를 반환할 경우
  // 조건문2도 false를 반환할 경우
}
```

#### for 문
특정횟수만큼 특정 코드를 반복하여 실행시킬 때 사용하는 코드

Example
```
for(var i = 0; i < 10; i += 1) {
  console.log("hello member" + i);
}
```

구성
```
for(초기값; 조건문; 초기값에서 어떻게 변할것인지) {
  // 만약 조건문이 true라면 실행
  // 만약 조건문이 false라면 더 이상 실행 X
}

var i;
for(i = 10; i === 0; i -= 2) {
  // 최초 반복: i: 0;
  // i가 10보다 작으면 무한대로 동작
  console.log("hello member " + i);
  // 1회차, i = 10;
  // 2회차, i = 8;
  // 3회차, i = 6;
  // 4회차, i = 4;
  // 5회차, i = 2;
  // 6회차, i = 0;
}

```

비슷한걸로 `while`문, `do while`문

### Expression
값을 반환하는 것

#### 연산식
A에 B를 더하거나, A에 B를 곱하는 등 연산과 관련된 일을 수행.

```
3 + 5;
// 8

10.4 + 20.3;
// 30.7

20 - 10;
// 10

20 / 10;
// 2

20 * 10;
// 200

n % 2;
// n = 1; // 1
// n = 2; // 0
// 나누고 남은 값
```

#### 값 비교
```
var a = 10;
var b = '10';

// 같은가
a == b;
// 자바스크립트에서 ==은 타입은 신경 안쓰고 값만 같으면 OK
// true

a === b;
// 권장
// 자바스크립트에서 ===은 타입도 값도 동일해야함.
// false

a + b;
// '1010'
// 내가 원했던 값이 20이라면..

a = 10;
b = 30;

a > b;
// false

a >= b;
// false

a < b;
// true

a <= b;
// true

// 증감
a += 10;
// a = a + 10;
// a === 20

a -= 10;
// a = a - 10;
// a === 10;

a *= 10;
// a = a * 10;
// a === 100

a /= 10;
// a = a / 10;
// a === 10

```

## scope (유효범위)
특정한 변수의 생존주기

```
var a = 10;
// global variables
// 전역 변수

function sum() {
  var num = 20;
  // local variables
  // 지역 변수
  function minus() {
    console.log(num);
    // num의 값? (20);
  }
  return a + num;
}

var c = sum();
// num: 20

minus();
// num: 100

console.log(a);
// 10

console.log(num);
// 100

console.log(c);
// 30
```

Scope는 함수를 기준으로 특정한 범위를 지정하여 변수의 유효범위를 지정함. (ECMA-262 5.1까지의 기준)

let (var의 진화판)
```
let a = 10;

function sum() {
  a = 100;
  console.log(a);
}

console.log(a);
```

const (상수)
```
const a = 100;

a = 10;
```

#### babel
babel이라는 도구를 이용해서 ES2015 문법의 하위호환성 보장
호환성 : [ECMAScript 6 compatibility table](https://kangax.github.io/compat-table/es6)

## this

---
## 복습
1. CSS Transform
2. CSS Animation
3. High performance animation
