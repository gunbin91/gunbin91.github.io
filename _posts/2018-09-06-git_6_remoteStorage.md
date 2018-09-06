---
layout: post
title: "6. 원격 저장소 ( RemoteStorage )"
tags: [ git, sourcetree, remote storage ]
date: 2018-09-06
categories: [ git ]
---

<p align="center">
    git은 보통 원격저장소라는 네트워크 저장소와 연동하여 사용한다. <br/>이는 협업에 있어 아주 중요한 혁신이다.
</p><br/>

# 원격저장소
자신의 로컬 하드디스크의 공간이 아닌 네트워크상에 저장할 수 있는 저장소를 의미<br/>
즉, 쉽게말해 인터넷상의 저장공간

# 원격저장소 종류
원격저장소의 종류로는 많이 알려져 있는 여러 네이버클라우드, 구글클라우드 등의 클라우드들이 있지만,<br/>
git을 통해 프로젝트를 전문적으로 관리하는 원격저장소는 따로있다.<br/>

#### ▶ git 원격 저장소
- github ( 오픈소스냐 아니냐의 따라 유료 )
- gitlab ( 신생 )
- yobi ( 국내 )

# 원격저장소와 소스트리 연결
현재 가장 널리 표준으로 사용되고 있는 github를 이용하여 로컬저장소와 연동해 보자.<br/>
SourceTree를 실행하여 <font color="orange">'Repository' - 'addRemote'</font>를 클릭하여 add클릭 후 <font color="orange">github에 생성한 Repository의 http주소를 복사하여 소스트리의 URL/Path에 붙여넣기</font><br/>
>처음 연결하는 경우에는 Default remote를 체크하여 연결한다.<br/>
왼쪽 Remotes목록에 생성한 remote네임이 생기게 된다.

# 원격저장소와 동기화
위의 연결만으로는 동기화되지 않는다. 이를 동기화 하기위해 <font color="orange">'push'</font>버튼을 누르게 되면,
현재 생성되어 있는 브랜치의 목록들이 나오게 되고, github에 올리고자 하는 브랜치만 
체크하여 ok버튼을 누른다.<br/><br/>

- 업로드 되는 과정에서 github의 로그인화면이 나오게 되고, 로그인 인증하면 동기화가 진행된다.<br/>
( 동기화 후에 github에서 저장소를 클릭하게 되면 업로드한 해당 프로젝트가 보이게 된다. )
<br/><br/>
- 동기화 까지 마치게 되면 소스트리 그래프에서 github도 브랜치처럼 표시되는데,
master등의 로컬 작업 후 commit하게 되면 <font color="deeppink">push버튼에 숫자</font>가 표시되는것을 확인할 수 있다.<br/>
이는 <font color="deeppink">github와 로컬작업의 버전차이</font>를 의미하며 github에 업로드하지 않았기 때문이다.<br/>
=> 따라서, 다시 github로 push해주게 되면 github에 업로드 됨과 동시에 push버튼의 숫자가 없어진다.



<br/>