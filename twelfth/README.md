# UI 개발 환경에 대해 이해해보자
## 목표
오늘 수업은 개발 환경에 대해 이해하고 이를 어떻게 구성하는 지 소개합니다. 오늘의 수업은 실무에서 중요하게 사용하는 것들에 대해 이해하여 더 나은 환경을 구축하는 걸 목표로 삼는다.

이 수업은 약 2시간가량 소요될 예정이며, 환경 설정이 완료된 후 CSS 셀렉터 레벨 3를 진행할 예정이고, 중간중간 실습을 함께 진행해보자.

## 목차
1. git을 사용한 버전관리
2. 빌드 환경 (gulp)
3. sass (scss), less, postCSS (권장)

## git을 사용한 버전관리
[git](https://git-scm.com/) 은 버전관리 시스템의 일종으로 현재 전세계에서 가장 활발히 사용한다. 버전관리 시스템은 실제 시스템을 작업해나가는 과정에서, 작업 이력을 남기고 어떤 사람이 어떤 목적으로 작업했는 지 파악하기 위해 사용하고, 코드에 에러가 있어 장애가 발생했을 때 이전 코드로 되돌아가기 위한 (이를 롤백이라 부른다) 목적으로도 사용한다.

Windows 유저라면 홈페이지에 들어가서 git을 설치하고, 맥 유저는 *xcode* 가 설치되어 있다면 자동으로 git이 설치되어있을 거다. GUI 도구로는 [SourceTree](https://www.sourcetreeapp.com/) 란 게 존재한다. (무료다)

```
$ git —version
git version 2.10.1
```

현재 내 맥북에 설치되어있는 git의 버전은 2.10.1이란 의미이며, 이 문구가 제대로 출력된다면 git을 제대로 설치한 것이다. 지금은 터미널(CLI) 화면이 익숙하지 않을 수 있지만 점차 익숙해지고 나중에는 터미널을 자유자재로 사용할 수 있을 것이다.

### 버전관리 시작하기
우선 간단한 UNIX 기본 명령어부터 살펴보자. Windows 유저더라도 git을 설치할 때 UNIX 명령어로 기본 설정되기 때문에 크게 문제 없이 진행할 수 있을 거라 생각한다.

```
$ mkdir myfolder
$ ls
myfolder

$ cd myfolder
```

`mkdir` 은 폴더를 만드는 UNIX 명령어로 뒤에 생성할 폴더 이름을 정의한다. 즉 위에서 작성한 `mkdir myfolder` 라는 명령어는 myfolder라는 폴더를 생성한다.  

`ls` 는 현재 경로에 있는 아이템들을 목록으로 나타낸다. 여기서는 myfolder만 나오지만 실제로는 더 많은 것들이 출력된다.  `cd` 는 해당 경로로 이동하겠다는 걸 의미한다. 위 코드에서는 myfolder 내부로 이동한다.

그리고 나서 git 저장소를 생성한다.

```
$ git init
Initialized empty Git repository in /choeun/myfolder/.git/

$ git status
On branch master
Initial commit
nothing to commit
```

위 문구까지 제대로 출력되었다면 비어있는 git 저장소를 성공적으로 생성했음을 의미한다. git 저장소는 로컬(즉, 여러분들이 지금 가진 컴퓨터 내부에 있다)에서 관리되며, 추후에 다른 사람과 협업을 하거나 컴퓨터를 변경하면서 작업하는 등 다양한 환경을 고려하기 위해 서버(많이 사용하는 게 [GitHub](github.com/) )에 올리게 된다.

이제 실제로 버전관리를 시작해보자. 먼저 git에서 버전관리를 하는 흐름은 아래와 같이 나눌 수 있다. 

### 로컬 저장소 버전관리
1. (최초 1회만) 유저 정보를 정의한다.
```
$ git config user.name "techhtml"
$ git config user.email "apes0123@gmail.com"
$ git config --list
user.name=techhtml
user.email=apes0123@gmail.com
```
2. 어느정도 의미 있는 작업을 완료하였을 때 버전관리를 진행한다.
3. 이번 버전에 포함시킬 파일을 추가한다. (`git add 파일들`)
4. 이번 버전이 어떤 작업을 포함하고 있는 지 내용을 내포하는 메시지와 함께 기록을 남긴다. (`git commit -m “메시지”`)

최초로 1회를 하고 난 이후부터는 1번 작업을 거치지 않더라도 `commit`이 가능하다. 그리고서 서버에 올릴 준비를 해야하는데, 이 작업을 위해서 서버가 필요하기 때문에 GitHub 계정을 생성하고, 저장소를 생성해보자.

### 계정 생성 및 리모트 저장소 생성
1. Github.com에 접속한다.
2. [image:CF0C02FD-2416-4F32-A197-57FD8E55A421-45733-00003DBAA2AF40CF/57EE3DD1-2E06-45BE-899A-1A2292D56C69.png] 위 내용에 맞는 내용을 각각 채워넣고 *Sign up* 버튼을 클릭한다.
3. 로그인을 하고 난 후, 화면의 우측에 존재하는 *new repository* 버튼을 클릭한다.
4. [image:D39E2AB2-5D53-4B8F-8306-F7CF2BEEFF89-45733-00003DD7CCC2470B/1C1AA4F5-CACE-4146-904C-595E6BFB088E.png]위 화면에서 *Repository name*을 *영문*으로 작성한 후 *Create repository* 버튼을 클릭한다.
5. 저장소가 생성되었다면, 화면 상단에 있는 `https://github.com/techhtml/test.git` 같은 저장소 주소를 반드시 복사한 후 다시 터미널 창으로 복귀한다.

여기까지 진행했다면 세가지 파트가 정상적으로 동작하는 지 체크해보자.
- git 설치가 제대로 되었는가
- 로컬 저장소에서 제대로 버전관리를 진행했는가
- 원격 저장소(GitHub) 계정을 생성하고 저장소 생성을 마쳤는가

위 세가지가 문제없이 잘 동작한다면 이제 실제로 GitHub 서버에 올리는 작업을 진행해보자.

```
$ git log --oneline
1631979 test

$ git remote add origin https://github.com/techhtml/test.git
$ git remote
origin

$ git push origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 204 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/techhtml/test.git
 * [new branch]      master -> master

$ open https://github.com/techhtml/test.git
```

위 과정을 통해 버전관리에 대해 간략하게 알아보았다. 물론 git을 이용한 버전관리는 이게 끝이 아니라 더 많은 사용법이 존재하며 그 사용법들에 대해 이해하고 사용하여야 한다.

하지만 이번 과정은 git을 학습하는 게 목표가 아니기 때문에 여기서 마치도록 한다.

## 빌드 환경
빌드(Build)는 최종 버전(배포용)의 코드를 만들기 위한 일련의 작업. UI개발에서 빌드가 의미하는 바는 코드를 최적화하고, SCSS나 LESS같은 프리 프로세서를 이용한 개발 코드를 CSS로 변경해주는 등의 작업을 해준다.

*gulp*는 빌드 시스템의 일종으로 CSS를 압축하거나, SCSS를 CSS로 변환해주거나, 이미지를 압축하는 등 다양한 일을 수행하기 위한 빌드 시스템.

### 준비물
[node.js](https://nodejs.org/en/) * 설치

```
$ node --version
v7.0.0
```

gulpjs 설치
```
$ sudo npm install gulp-cli --global
/usr/local/lib
└── gulp-cli@1.2.2 

$ gulp --version
[10:48:28] CLI version 1.2.2
[10:48:28] Local version 3.9.1

```

### gulp로 SASS 개발환경 구축하기

#### 전제조건
1. sass로 개발을 한다.
2. sass로 개발을 한 결과물은 압축된 상태(minify)로 보이게 한다.

#### 구축
1. `guflfile.js`를 생성
2. 사용할 도구(gulp-sass, gulp-css-minify)의 가이드를 참고하여 `gulpfile.js`을 채워넣음
3. `npm init` => *node.js*로 이루어진 어플리케이션임을 정의
```
$ npm install gulp gulp-sass --save-dev
$ gulp sass
```

*gulp* 외에도 *grunt*나 *webpack*같은 빌드 도구가 존재. UI 개발 단계에서는 gulp가 가장 효율적이기 때문에 이 수업에서는 gulp를 사용합니다.

## SASS와 LESS, postCSS
### CSS의 문제점
자식관계를 나타내려면 부모이름을 계속 써줘야함
```
.product {}
.product dt {}
.product dd {}
```

중복되는(약간만 바뀌는) 코드가 있더라도 여러번 작성해줘야 함
```
.product-white {
  font-size:15px;
  line-height:1.2;
  background:white;
}
.product-red {
  font-size:16px;
  line-height:1.2;
  background:red;
}
```

변수가 없음. (var를 이용한 변수는 존재하나, 하위호환성이 낮음)
```
.product-title {
  color: #2ac1bc;
}
.product-button {
  background:#2ac1bc;
}
```

SASS나 LESS가 하는 일은 반복되는 작업을 줄여주고, 효율적으로 CSS를 관리할 수 있도록 하게 함.

### SASS와 LESS
SASS(LESS)는 기존의 CSS가 불편했기 때문에 개발자들이 더 효율적으로 CSS를 관리할 수 있게 만든 언어.

자식관계를 나타내려면 부모이름을 계속 써줘야함
```
.product {
  position:relative;
  font-size:12px;
  dt {}
  dd {}
}
```

중복되는(약간만 바뀌는) 코드가 있더라도 여러번 작성해줘야 함
```
@mixin box($font-size, $bg-color) {
  font-size:$font-size;
  line-height:1.2;
  background:$bg-color;
}
.product-white {
  @include box(14px, white)
}
.product-red {
  @include box(16px, red)
}
```

변수가 없음. (var를 이용한 변수는 존재하나, 하위호환성이 낮음)
```
$primary: #2ac1bc;

.product-title {
  color: $primary;
}
.product-button {
  background: $primary;
}
```

SASS와 LESS는 차이는 아주 미미하게 있어요. SASS는 Ruby라는 언어를 기반으로 만들어진 언어, LESS는 nodeJS를 기반으로 만들어진 언어.

### postCSS
CSS를 CSS로 변환. 미래 버전의 CSS를 현재 사용가능하게 해주는 역할
1. CSS 변수를 사용했다면, 하위호환성을 고려해서 변경
2. CSS 계산식을 사용했다면, 하위호환성을 고려해서 변경
3. 자동으로 vendor prefix를 붙여줌

```
/* before */
$primary: #2ac1bc;

.box {
  background:$primary;
}

/* after */
.box {
  background:#2ac1bc;
}
```

