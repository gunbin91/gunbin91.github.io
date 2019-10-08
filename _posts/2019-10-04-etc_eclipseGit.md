---
layout: post
title: "Eclipse에서 Git사용하기"
tags: [ etc, eclipse Git ]
date: 2019-10-04
categories: [ etc ]
---

<p align="center">
   Eclipse(또는 STS)에서도 git을 사용할 수 있도록 제공하고 있다.<br/>
    Git에대한 자세한 내용은 <a href="/git">Source Tree사용법</a>에서 확인!
</p><br/>

## ◆ Git
프로젝트를 진행하면서, 중간 중간 백업할 지점을 만들어 둘 수 있는 저장소의 개념으로, 여러 사람과 연동되어 협업에도 이용된다.<br/>
Eclipse에서 git의 사용은 <font color="orange">window – show view – git repository를 열면 git</font>을 설정할 수 있는 탭이 나온다.

<br/>

### ▶ Git 저장소 만들기

#### 1. 프로젝트를 만들기 전 <font color="orange">create new local git repository</font>를 이용해 git저장소를 만든다. ( 프로젝트 당 하나 )

#### 2. 프로젝트를 만들 때  project location -> use default location 해제 후 Location을 만들어둔 git repository경로로 설정하게 되면 깃을통해 관리될 수 있다.

<br/>

### ▶ Git의 감지대상 제외(git ignore)
특정 파일이나 디렉터리를 git이 무시하도록 설정할 수 있다. 보통 target폴더 내의 파일들이 Git의 감지대상이 되면, 프로젝트가 꼬이게 될 수 있으므로 target폴더는 git의 감시대상에서 제외해준다.<br/>
- 감시대상 제외
: <font color="orange">target폴더(무시할대상) 우 클릭 -> team -> ignore</font><br/>
( 잘못 등록했을 시 Git Repositories -> Working Tree -> WebContent -> .gitignore 파일에서 추가, 삭제 할 수 있다. )

<br/>

### ▶ Git version 등록
백업할 지점을 등록할 때 하나하나의 백업 지점을 version이라고 한다. 버전을 등록하는 방법은<br/> <font color="orange">프로젝트 우 클릭 -> team -> commit</font>을 클릭하여 커밋창을 띄우고<br/> Unstaged Changes(마지막 버전 이후 추가 또는 수정된 파일들)에서 target경로가 있다면 빼주고,버전에 등록할 파일들을 모두 밑에 Staged Changes로 이동 오른쪽 Commit mesage에 버전 이름을 작성 후 commit

> commit은 로컬에서 저장하는 상태로, push하기 전 까지는 깃을 공유하는 사람들과 공유할 수 없는 상태이다.

<br/>

### ▶ Git 백업 지점으로 돌아가기
프로젝트 우 클릭 -> <font color="orange">team -> Show in History</font>을 통해 백업한 version내역을 볼 수 있다.<br/>
해당 내역 중 원하는 백업 지점 <font color="orange">버전 우 클릭 -> reset -> Hard</font> 으로 등록한 버전으로 돌아갈 수 있다.

<br/>

### ▶ Branch 만들기
Branch는 테스트용이나 추 후 합치기 위하여 나뭇가지 개념으로 나눠서 작업하는 노드이며 master와 합병작업을 통해 합칠 수 있다.<br/>
프로젝트 우 클릭 -> <font color="orange">team -> switch to -> new branch</font><br/>
=> 중간 작업 완료 후 똑같이 commit 하면 됨

<br/>

### ▶ 브런치 합병
- 작업 노드를 master로 변경
: 프로젝트 우 클릭 -> <font color="orange">team -> switch to -> master</font><br/>

- branch와 합병
: 프로젝트 우 클릭 -> <font color="orange">team -> Marge -> brach선택 후 Marge</font><br/>
( 브런치 끼리도 합병이 가능하다. )

<br/>

### ▶ 브런치 지점 이동
프로젝트 우 클릭 -> team -> switch to 에서 만들어놓은 브런치 또는 마스터에 등록되어있는 버전으로 이동이 가능하다.

<br/>

## ◆ GitHub
로컬에 있는 <font color="orange">깃 저장소를 원격서버에 백업</font> 해둘 수 있는 서비스를 제공하는 곳 중 하나가 gitHub이다.<br/> 
gitHub 홈 => 가입 => 이메일인증 => gitHub 이름 설정하고 만들기

<br/>

### ▶ git push
만들어둔 프로젝트를 <font color="orange">gitHub에 올리는 (동기화)</font>작업,
gitHub홈페이지에서 만들어둔 깃 저장소에 들어간 후 깃의 주소를 복사한다. ( 초록색 버튼을 누르면 나온다. ) -> 이클립스로 돌아와서 프로젝트 우 클릭 -> team -> <font color="orange">push Branch'master'</font><br/>
=> 아이디비번 입력( git의 소유주거나 초대받은 아이디만 가능 )

<br/>

### ▶ git불러오기
등록한 git을 새로운 프로젝트로 옮기는 작업

- 1) git repository가져오기
: Git Repository메뉴를 열어서 <font color="orange">clone a git repository</font> 클릭 => 찾아서 등록

- 2) import
: 후 프로젝트를 가져오기 위해서 import -> Git -> Project form git -> Existing local repository -> repository선택<br/>
( 단, 서버는 따로 만들어야 함 )

<br/>

### ▶ git pull
gitHub에서 등록된 버전을 현재 로컬과 동기화<br/>






<br/>
<hr/>