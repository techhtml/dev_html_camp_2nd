# CSS Transform
**transform** - 무언가를 변형

## 속성값
1. 이동 (translate)
2. 크기 조정 (scale)
3. 회전 (rotate)
4. 비틀기 (skew)

### translate
```
.box {
  transform:translate(-100%, 0);
}
/*
 * translate(x, y)
 * 자기 자신을 기준으로 움직임
 * percentage 단위를 쓸 경우,
 * 자기 자신이 보이는 지점을 기준
 */
.box {
  transform:translate(100px, 0);
}
```
**GPU 가속** 하면서 움직이는 CSS 속성

### rotate
```
/*
 * 회전을 이용할 때는 deg라는 단위
 * rotateX나 rotateY를 이용해 3D를 효과를 낼수도 있음
 */
.box {
  transform:rotate(1080deg);
}
```

### scale
```
.box {
  transform:scale(2);
}
```

### skew
```
.box {
  transform:skew(30deg)
}
```

## CSS animation
1. 트리거 기반 애니메이션 (transition)
2. 그냥 애니메이션 (animation, @keyframes)

### transition
```
/*
 * 유저가 a요소에 마우스를 올렸을 때 색상이 변경됨
 * a에서 b로 가는 과정을 내가 제어하지 못할 때
 */
a {
  color:#ccc;
  transition:0.3s all ease;
}
a:hover {
  color:#2ac1bc;
  background:gray;
}
/*
 * transition
 * transition-duration (시간)
 * transition-property (어떤 속성에)
 * transition-timing-function (가속도를 어떻게 넣을 건 지)
   * bezier-curve
 */
```
[cubic-bezier.com](http://cubic-bezier.com/)

### animation
내가 어느정도 제어 가능한 단계에서 애니메이션을 부여
트랜지션은 A에서 B까지의 변화를 지정, 애니메이션은 키프레임으로 그걸 지정

애니메이션 명세
최초 : [  박스   ]
마지막 :                                                  [  박스   ]
```
.box {
  width:150px;
  height:150px;
  background:crimson;
  /*
   * animation-duration
   * animation-(keyframe)name
   * animation-timing-function
   */
  animation:1s move-box ease;
  /*
   * animation-fill-mode
   */
  animation-fill-mode: forwards;
  /*
   * animation-iteration-count
   * 무한반복 : infinite
   */
  animation-iteration-count: 10;
  /*
   * animation-delay
   * 몇초 후에 애니메이션 되어라
   */
  animation-delay:3s;
}

@keyframes move-box {
  0% {
    transform:translate(0, 0);
    background:red;
  }
  100% {
    transform:translate(100%, 0);
    background:green;
  }
}
@keyframes move-box {
  from {}
  to {}
}
```

## 브라우저의 해석법
### HTML
1. HTML 코드 읽어들임 (parsing)
2. 토큰화 (tokenize)
3. DOM 객체 생성
4. DOM Tree 생성
5. Style Tree와 매칭
6. 요소를 배치 (layout, reflow)
7. 화면에 보여줌

### CSS
1. CSS 코드 읽어들임
2. 토큰화 (tokenize)
3. Style Tree (DOM TREE와 비슷한 형태)

### 렌더링 엔진
1. webkit (Safari)
2. blink (Opera, Chrome)
3. trident (MS Edge, IE)
4. gecko (Firefox)

### 자원 (Resource)
해석할 때 (Parse, Tokenize, DOM TREE)는 CPU
그릴 때 GPU 사용

CPU = 연산왕
GPU = 그림왕

CPU가 해석하고 GPU에 보내서, GPU가 화면에 그림
**CPU를 거치는 과정을 줄일수록 렌더링 속도 빠름**
=> Layout 과정을 최대한 줄인다.

CPU가 계산하는 것들?
[CSS Triggers](https://csstriggers.com/)
