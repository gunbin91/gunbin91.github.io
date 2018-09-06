---
layout: post
title: "2. Git저장소 만들기"
tags: [ git, sourcetree, gitrepository ]
date: 2018-09-05
categories: [ git ]
---

<p align="center">
    Git을 통해 프로젝트를 관리할 수 있도록 연동하여 생성하는 방법을 알아보자.
</p><br/>

# git저장소 생성
Git을 통해 프로젝트를 관리할 수 있도록 하려면 Git저장소를 만들어야한다.
1. 자신의 로컬 컴퓨터에 프로젝트를 진행할 적당한 경로에 디렉터리를 만든다.
2. SourceTree를 실행하여 Create를 클릭하고 만들어놓은 디렉터리를 선택하고 이름을 지정한다.
> 해당 디렉토리에 자동으로 .git이라는 숨김폴더가 생성된다. <font color="deeppink">Git으로 프로젝트를 관리하기 위해서는 프로젝트 내부에 이렇게 만들어진 '.git'숨김폴더가 있어야 한다.</font> 

<br/>

# 버전 만들기 ( commit )
버전이란 하나의 저장된 지점을 의미하는데 <font color="deeppink">git의 버전을 저장(등록)하는것을 'commit'이라고 한다.</font><br/>
프로젝트에 새로운 파일이 생성 또는 삭제되거나 내용이 수정되었을 경우 즉, <font color="deeppink">현재 git에 저장되어 있는 최신 버전과 현재의 상태가 다를경우</font> Git이 알아서 이를 인식하여 'Uncommitted changes'라는 메시지를 띄워놓게 된다.
<br/><br/>
왼쪽 탭에서 'File Status'라는 탭을 보면 'Unstaged files'와 'Staged files'라는 두개의 파트가 있는데, Unstaged files는 commit하지 않을 파일들의 목록을 의미하고, Staged files는 commit하고자 하는 파일들의 목록을 의미한다.
<br/><br/>
즉, 수정된 모든 파일들이 Unstaged files의 목록으로 나타나게 되고, 수정사항을 commit하고자 하는 파일들을 선택하여 'Stage Selected'또는 'Stage All'버튼을 통해 <font color="deeppink">Staged files로 옮긴 후 commit</font>하면 해당 수정사항에 대한 버전이 하나 만들어 지는것이다.

> 또한 버전 클릭시 오른쪽 하단에 수정된 코드의 내용이 보이게 되는데 새롭게 추가된 코드부분은 녹색, 삭제된 코드부분은 적색으로 표시된다.


<br/>