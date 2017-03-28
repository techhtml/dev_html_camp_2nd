# 접근성 & 복습
웹접근성
## KWCAG 2.1 (리뷰)
TIME : 1시간 30분 ~ 2시간

### 준수의무
1. 기본적 측면
2. 법적 측면

### 원칙
* 인식의 용이성
* 운용의 용이성
* 이해의 용이성
* 견고성

### 인식의 용이성
####  *텍스트 아닌 콘텐츠*는 그 의미나 용도를 인식할 수 있
도록 대체 텍스트를 제공해야 한다.

대표주자 : 이미지, 동영상, 오디오

```
// 가장 기초적인 대체 텍스트
<img src='이미지의 경로' alt='교촌 간장치킨'>
<!-- alt (alternative text, 대체 텍스트) -->

// 배경 이미지에 대체텍스트를 넣는 경우
<div class='bg'>
  <span class='blind'>배경 이미지를 위한 설명 텍스트</span>
</div>

.bg {
  // IR (Image Replacement) 기법
  text-indent:-9999px;
}

.blind {
  // 얘가 더 좋은 방식
  position:absolute;
  left:-9999px;
}

// 긴 설명문을 달아야 하는 경우
<img src='차트' alt='전국민 드립 배틀 배민 신춘문예 1년치 치킨에 도전하세요.' longdesc='desc.html'>

// desc.html
<body>
	<h1> 전국민 드립 배틀 배민 신춘문예 1년치 치킨에 도전하세요.</h1>
	<dl>
		<dt>응모자격</dt>
		<dd>넘치는 드립력과 새벽 3시의 감성을 두루 갖춘자</dd>
	</dl>
</body>

// 긴 설명문을 달아야하는 배경이미지
<div class='bg'>
	<h1 class='blind'> 전국민 드립 배틀 배민 신춘문예 1년치 치킨에 도전하세요.</h1>
	<dl class='blind'>
		<dt>응모자격</dt>
		<dd>넘치는 드립력과 새벽 3시의 감성을 두루 갖춘자</dd>
	</dl>
</div>

```

#### 멀티미디어 콘텐츠의 대체 수단 (자막, 수화, 대본)
#### 명조대비
* 전경색(폰트색상, 콘텐츠색상)과 배경색이 4.5 : 1을 준수해야한다.
* 만약 폰트사이즈가 14px 이상에 bold인 경우, 혹은 18px 이상인 경우는 3:1도 가능
* 확대가 가능한 경우 3:1
* 콘텐츠 사이에 구분이 가능해야한다. (구분선, 배경색을 달리, 폰트사이즈를 달리)

```
// skip navigation

<a href='#main' class='skip-nav'>메인 콘텐츠로 바로가기</a>

<div id='main'>
  // 콘텐츠
</div>
.skip-nav {
  position:absolute;
  top:0;
  left:-9999px;
}
.skip-nav:foucs {
  left:0;
}

```

### 운용의 용이성

[웹 접근성, 나눔 : 널리](http://nuli.navercorp.com/sharing/a11y)

## 복습 (INDEX)
### 좋은 개발자?
HTML, CSS (UI, UX) 개발을 배움. 어떻게 해야 *좋은 개발자*가 될 수 있을까요?
*좋은 개발자*란?

*5%의 뛰어난 사람들* 때문에 *95%의 덜 뛰어난 사람*이 고통받는 구조

### 뭘 해야 좋은 개발자?
* 생각을 그대로 구현해낼 수 있으면 좋은 개발자
* 오픈소스에 기여하면 좋은 개발자
* 성능을 잘 내면 좋은 개발자
* 개발을 빨리 하면 좋은 개발자

### Font
* font-family (폰트의 집합)
* font-size (폰트의 크기)
* line-height (행간)
* font-weight (폰트의 굵기)
* letter-spacing (자간)
* color (색상)

### Text
* text-align (정렬)
* text-indent (들여쓰기)
* text-decoration (밑줄, 밑줄 제거)

### Box-model (박스가 어떻게 생겨먹었는 지)
* width
* height
* padding
* border
* margin
* box-sizing

### Layout
* float
* display model (block, inline)
* flex

### flexbox (부모)
* display: flex
* justify-content
* align-items
* flex-wrap

### flexbox (자식)
* flex 속성
* min-width

### Position
* position 속성
	* absolute
	* relative
	* fixed
	* static (기본값)
* left, top, right, bottom
* z-index (숫자가 높을수록 z축이 위로)

### Animation
* animation 속성 (내가 시점 제어가 가능한)
* transition 속성 (내가 시점 제어가 불가능한)
* transform 속성
	* 이동 (translate)
	* 크기 (scale)
	* 회전 (rotate)
	* 꺾기 (skew)

### Units
* px (pixel)
* % (부모 요소에 비례해서 변하는 값)
	* padding-top: 100%; (부모요소의 width === 100%, 320px === 320px)
	* width: 100%; (부모요소의 width === 100%, 320px === 320px)
	* font-size: 100%; (부모요소의 폰트 크기)
	* line-height:100%; (부모요소의 폰트 크기)
* em (자기 자신의 폰트 사이즈에 비례해서 변함)
	* font-size: 14px;
	* padding:1em;  (=== padding:14px)
	* 계산이 어렵다.
* rem (root em, `<html>` 요소의 폰트 사이즈에 비례해서 변함)
	* `html { font-size: 16px }`
	* `p { font-size: 18px } `
	* `p { padding: 1rem } ` (===  padding: 16px)
* vw, vh (viewport width, viewport height)  http://caniuse.com/#feat=viewport-units
	* 브라우저 지원율 낮음
	* 뷰포트를 기준으로 변하는 값
	* 100vw = 뷰포트의 가로 사이즈 아이폰 5s의 가로사이즈 = 320px = 100 vw = 320px
	* 100vh = 뷰포트의 세로 사이즈 아이폰 5s의 세로사이즈 = 480px = 100 vh = 480px

### 고려해야하는 것들
#### 공통
* 어느 버전까지 지원할 것인가?
* 반응형 웹 디자인인가?
* 입력 장치 어떤 거 쓰는 지? (터치, 마우스, 키보드)

#### Desktop
* 디스플레이 사이즈 (화면 크기)
* 전체를 다 이용할건 지, 부분만 이용할 건 지 980px 고정하고 margin auto로 센터정렬 할 건지,
페이지 전체 다 쓸 건 지

#### Mobile
* 화면 크기
* 센서 어느정도 쓸건 지
* 터치 영역 체크
