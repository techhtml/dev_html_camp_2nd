# UI 개발 환경에 대해 이해해보자
## 목표
오늘 수업은 개발 환경에 대해 이해하고 이를 어떻게 구성하는 지 소개합니다. 오늘의 수업은 실무에서 중요하게 사용하는 것들에 대해 이해하여 더 나은 환경을 구축하는 걸 목표로 삼는다.

이 수업은 약 2시간가량 소요될 예정이며, 환경 설정이 완료된 후 CSS 셀렉터 레벨 3를 진행할 예정이고, 중간중간 실습을 함께 진행해보자.

## 목차
1. git을 사용한 버전관리
2. 빌드환경 (gulp)
3. sass (scss), less, postCSS (권장)
4. 테스트 서버 구축

## git을 사용한 버전관리
[git](https://git-scm.com/) 은 버전관리 시스템의 일종으로 현재 전세계에서 가장 활발히 사용한다. 버전관리 시스템은 실제 시스템을 작업해나가는 과정에서, 작업 이력을 남기고 어떤 사람이 어떤 목적으로 작업했는 지 파악하기 위해 사용하고, 코드에 에러가 있어 장애가 발생했을 때 이전 코드로 되돌아가기 위한 (이를 롤백이라 부른다) 목적으로도 사용한다

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

## 빌드환경
(작성 중)

## SASS와 LESS, postCSS
(작성 중)

## 테스트 서버 구축
(작성 중)