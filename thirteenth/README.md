# JavaScript에 대해 이해해보자
## 목표
오늘 수업은 JavaScript에 대해 이해하고 어떻게 사용하는 지 살펴본다.
1. 자바스크립트의 역사에 대해서 살펴본다.
2. 자바스크립트 기초 문법을 살펴본다.
3. 문서 객체 모델 (DOM)에 대해 이해하고 이를 활용해본다
4. babel을 이용해 하위 호환성을 보장한다.

## JavaScript 역사
1996년, Firefox(Netscape Navigator)에 막 입사한 브랜든 아이크(Branden Eich)라는 사람에게 미션이 있었어요. Scheme이라 불리우는 프로그래밍 언어를 네비게이터 브라우저에서 동작하게 하라. 10일동안, Scheme (함수형 언어)에 C++에 Perl을 섞음.
=== JavaScript.

처음의 목적, 정적인 HTML 페이지에 동작을 부여한다. 처음에는, Mocha라는 이름, 넷스케이프의 이사가 정한 이름. LiveScript라 이름을 변경했다가, 마케팅 이슈로 당시 가장 유행하던 JAVA라는 언어의 라이센스를 따서 JavaScript라 명명함.

JavaScript라는 언어가 특정 회사(Netscape)의 개발자가 만들었으니, 이를 표준화하여 전세계에 배포해야한다. 유럽의 표준기구인 ECMA (ECMA International)와 함께 JavaScript의 표준화를 진행하고, 표준화된 JavaScript를 ECMA-262 문서로 관리한다.

ECMAScript, ECMA-262, ECMA-2015, ECMA6은 JavaScript의 표준버전을 가리키는 표현. ECMA 3.1(2008년)에서 ECMA 6(2015년)까지 걸린 시간은 7년.

발전이 너무 더디다보니 만들어진 게 TypeScript, CoffeeScript같은 번외작이 나오기 시작하고, 사람들이 많이 사용함. ECMA-262의 7번째 Edition을 기준으로 학습. 기본적인 개념은 5.1을 참고.

IE는…….. JScript라는 별도의 자바스크립트 문법을 가지고 있고, IE8까지 해당 문법이 존재함. IE 호환성은 100%, `jQuery`라는 라이브러리를 이용해서 구현

## JavaScript 기초 문법
### 변수 (Variables)
변수(variables)는 특정한 값(value)을 담기 위한 공간으로 활용된다. 예를 들어, 3초에 한번씩 `hello world`를 출력하는 프로그램이 있다고 생각해보자.

```
setInterval(function() {
  console.log('hello world');
}, 3000)
```

위 코드는 3초마다 한번씩 console에 `hello world`를 출력하는 프로그램이다. 위 코드에서 어떤 부분이 시간을 나타내는 부분인 지 파악할 수 있는가? JavaScript에 익숙하다면 당연히 이해할 수 있겠지만, 그렇지 못한 사람은 어떤 부분이 시간을 제어하는 지 이해하기 어렵다.

```
const REPEAT_TIME = 3000;

setInterval(function() {
  console.log('hello world');
}, REPEAT_TIME)
```

위 코드에서는 이전 코드에 `3000`이라고 써져있던 걸 `REPEAT_TIME`이라는 변수로 변경하고, 해당 변수에 값을 넣어주었다. 즉 변수는 값을 더 이해하기 쉽게 하고, 그 값을 제어하는 데에 있다.

변수를 선언하는 방법에는 `var`, `let`, `const`로 3가지 방법이 있다. 이 수업에서는 먼저 `var`에 대해서만 다루도록 한다.

`var`는 예로부터 사용되어온 전통적인 변수 선언 방식으로, 이 키워드를 이용해 변수를 선언할 수 있다.  자바스크립트에서는 모든 것을 값(Value)으로 생각하기 때문에 변수에 어떤 값이던 넣을 수 있다.

```
// 숫자 (Number)
var num = 3;
var pie = 3.14;

// 문자열 (String)
var name = "조 은";

// 따옴표를 써도 된다
var name = '조 은';

//두 문자열을 더할 수도 있다.
var first_name = '조';
var last_name = '은';
var name = first_name + last_name;
// name === '조은'

// 참, 거짓을 판별하는 값도 존재한다.
var isMoved = false;
var isCatch = true;

// 익명 함수를 넣었다
var move = function() {
  console.log('hello world');
}

// 키 : 값으로 이루어진 객체를 넣을 수도 있다.
var choeun = {
  name: '조은',
  age: 100
}

// 객체의 값을 가져올 때는 아래와 같이 사용한다.
console.log(choeun.name); // 조은
console.log(choeun.age); // 100

// 배열이 존재하기도 한다.
var student_list = ["조은","조금","조별","조실버","조동"];

// 배열에 접근할 때는 아래와 같이 사용한다.
student_list[0] === "조은";
student_list[1] === "조금";
student_list[2] === "조별";
student_list[3] === "조실버";
```

다른 프로그래밍 언어를 접했다면 낯선 개념일 수 있지만, 모든 것을 값으로 인식한다는 것에 주의하길 바란다.

### 객체 (Object)
우리 삶에 존재하는 모든 것을 객체라 부를 수 있다. 이 개념은 상당히 어려운 개념이지만, 반드시 알아야하는 개념이다. 현실 세계의 나무 의자를 객체로 생각해보자.

[image:AD704EED-C59E-48EB-80F8-5D9A3D66130B-71924-0000783A1C637C5F/thumb-17IaM7Lu312_500x500.jpg]
**Figure 1.** 현실세계의 나무 의자

먼저 **나무 의자**라는 객체가 어떻게 구성되어있는 지 살펴보자.
1. 다리 4개
	1. 다리 (객체)
	2. 재질: 나무
	3. 높이: 4cm
	4. 둘레: 2cm
2. 시트
3. 등받이

```
var wood_chair = {
  legs: [
    {material: 'wood', height: '4cm', width: '2cm'},
    {material: 'wood', height: '4cm', width: '2cm'},
    {material: 'wood', height: '4cm', width: '2cm'},
    {material: 'wood', height: '4cm', width: '2cm'}
  ],
  seat: {
    material: 'wood',
    height: '2cm',
    width: '15cm'
  },
  back: {
    panel: {
      material: 'wood',
      height:'15cm',
      width:'10cm'
    },
    legs: [
      {material: 'wood', height: '4cm', width: '2cm'},
      {material: 'wood', height: '4cm', width: '2cm'}
     ]
  },
  isSeat: false,
  onSeatIn: function() { },
  onSeatOut: function() { }
}
```

객체는 현실세계에 존재하는 것을 **모델링**하는 걸 의미.

### 추상화 (abstraction)
내용을 간추려내는 것.

```
var choeun = {
  name: '조은별',
  age: 100,
  getFirstName: function() {
    return this.name[0];
  },
  getLastName: function() {
    return this.name[1];
  },
  getName: function() {
    return this.name;
  }
}

// choeun.name === "조은"
// choeun.getFirstName() === "조"

```

### 객체 생성
```
var oakWood = {
  name: 'oak',
  origin: 'KR',
  getOrigin: function() {
    return this.origin;
  },
  setOrigin: function(origin) {
    this.origin = origin;
  }
}

var redPineWood = {
  name: 'korean red pine',
  origin: 'KR',
  getOrigin: function() {
    return this.origin;
  },
  setOrigin: function(origin) {
    this.origin = origin;
  }
}

var roxb = {
  name: 'Ficus elastica Roxb',
  origin: 'KR',
  getOrigin: function() {
    return this.origin;
  },
  setOrigin: function(origin) {
    this.origin = origin;
  }
}

var wood = {
  name: 'Green wood',
  origin: 'KR',
  getOrigin: function() {
    return this.origin;
  },
  setOrigin: function(origin) {
    this.origin = origin;
  }
}

oakWood.setOrigin('JP');
```

#### 이슈:
(1) 메모리 관리측면에서 불편하고,
(2) 객체의 복잡도가 높아질 수록 코드를 나열해야하는 수준이 길어짐

```
// 생성자 함수 (Constructor)
// 다른 언어 => (Class)

var Wood = function(name, origin) {
  this.name = name;
  this.origin = origin;
  this.getOrigin = function() {
   return this.origin;
  }
  this.setOrigin = function(origin) {
    this.origin = origin;
  }
}

// 인스턴스
var pineWood = new Wood('소나무', 'KR');
var oakWood = new Wood('참나무', 'KR');

```

### 상속 (Prototype)
Prototype 상속은 유전자 상속, 부모 객체로부터 형질을 물려받음.

```
var Wood = function(name, origin) {
  // var this = {};
  // this.__proto__ = Wood.prototype;
  this.name = name;
  this.origin = origin;
  // return this;
}

Wood.prototype = {
  getOrigin = function() {
   return this.origin;
  },
  setOrigin = function(origin) {
    this.origin = origin;
  }
}

var pineWood = new Wood('소나무', 'KR');
var oakWood = new Wood('참나무', 'KR');
```

## 문서 객체 모델 (DOM)
JavaScript를 이용하여 HTML이나 XML같은 마크업 언어의 요소를 제어 가능하게 하는 개발 API.

1. 요소 자체에 대한 접근
2. 이벤트 (event)

개발을 함에 있어 제일 중요한 것?
1. 스펙을 제대로 이해하는 것
2. 일정 준수 (실무)

스펙을 제대로 이해함에 있어서 필요한 과정
1. 기획자 & 디자이너와 충분한 면담 (괴롭힘)
2. 자기 자신의 역량 체크
3. 브라우저의 역량 체크
4. 스펙 명세서 작성

## 스펙명세서
1. 유저가 시(최대 20자)와 작가명(최대 10자)을 입력한다
2. 특정한 형태의 이미지를 만들고 배경을 선택할 수 있게 한다
3. 배경은 미리 정해진 이미지와 유저가 선택한 이미지를 선택할 수 있다
4. 이미지를 저장하여 페이스북 or 카카오톡 or 인스타그램에 공유한다

### 테스트 케이스
1. 시를 입력한다
	1. 만약 시가 20자 이내일경우
	2. 만약 시가 20자 이상일경우
2. 작가명을 입력한다
	1. 만약 작가명이 10자 이내일경우
	2. 만약 작가명이 10자 이상일경우
	3. 만약 시를 입력하지 않았는데 작가명 칸으로 넘어온경우

### 요소에 대한 접근
IF) 버튼을 클릭할 경우
IF) 요소를 클릭할 경우

{target}을 {event}할 경우

#### querySelector()
```
// Native
var div = document.querySelector('div');

// jQuery
var $div = $('div')
```

**document는 어디서 튀어나왔냐?**

#### DOM과 prototype
DOM (Document Object Model)은 HTML 요소 한개와 1:1로 매칭, 즉 하나의 `<div>`가 생기면 `HTMLDivElement`라는 문서 객체가 생성이 됨.

10000개의 HTML요소가 있을 때, 10000개의 문서 객체가 생성이 된다? 즉 메모리 관리가 **아주** 중요함.

DOM(Document Object Model, 문서 객체 모델)은 prototype를 잘 활용하여 메모리 활용도를 극대화한 모델.

HTML{요소명}Elment
HTMLElement
Element
Node (요소 탐색)
EventTarget (이벤트 관련 코드)
Object

`document`는 DOM(Document Object Model)의 최상위 객체, `document.querySelector()`라고 하면 문서 내에서 요소를 d 찾아라.

### 이벤트
이벤트는 크게 두종류
1. 유저가 행하는 것
2. 유저가 행하지 않는 것

#### 유저가 행하는 이벤트
1. 마우스 (mouse)
	1. mousedown (마우스를 누를 때)
	2. mouseup (마우스를 뗄 때)
	3. mousemove (마우스를 움직일 때)
	4. mouseover (마우스를 올렸을 때)
	5. mouseenter (마우스가 최초로 들어갔을 때)
	6. mouseleave (마우스가 나올 때)
	7. mouseout (요소 내 자식요소에 마우스를 올리는 것도 아웃으로 포함)
2. 키보드 (keyboard)
	1. keydown (키보드 눌렀을 때)
	2. keypress (키보드를 계속 누르고 있을 때)
	3. keyup (키보드에서 뗐을 때)
3. 터치 (touch)
	1. touchstart (터치를 시작했을 때)
	2. touchmove (터치한 채로 움직일 때)
	3. touchend (터치가 끝났을 때)
4. 추상적개념
	1. click
	2. dblclick

```
// Native
요소.addEventListener('이벤트이름', function(evt) {
  // 이벤트를 발생
  console.log(evt)
})

// jQuery
$('셀렉터').on('이벤트이름', function(evt) {
  // 이벤트를 발생
  console.log(evt);
})
```

### 실제로 이벤트를 부여
carousel 코드
터치 시작 => 무브 => 끝 이벤트를 넣고
touchstart => touchmove => touchend

#### 실습
1. carousel 코드에 Touch Event 부여하기
2. 어떤 값을 이용해서 carousel을 구현할 수 있을까?
