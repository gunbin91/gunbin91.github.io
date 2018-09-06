---
layout: post
title: "git Ignore"
tags: [ git, sourcetree, git tag  ]
date: 2018-09-06
categories: [ git ]
---

<p align="center">
    원격저장소를 이용해 git을 사용하는 경우 대부분 노출되기 때문에, 보안상의 문제등으로 git이 관리하지 못하도록 하고싶은 파일을 지정하는 방법을 알아보자.
</p><br/>

# Ignore
무시한다라는 뜻으로 버전관리에서 굳이 같이 관리를 할 필요가 없는 파일들을
없는것 처럼 무시하도록 설정하는것.

#### ▶ Ignore파일 등록
unstaged목록에 무시하고자 하는 파일이 나오게 되면 해당 파일을 <font color="orange">오른쪽 클릭 후
ignore</font>를 클릭하게 되면 아래와 같은 선택사항을 클릭하여 등록한다.
<br/>
- <font color="orange">Ignore exact filenames</font> : 해당 파일명을 무시한다.
- <font color="orange">Ignore all files with this extension</font> : 해당 확장자 명을 가진 파일을 무시한다.
- <font color="orange">Ignore custom pattern</font> : 파일명의 패턴으로 무시

> ignore파일을 등록하게 되면 .gitignore라는 환경설정 파일이 만들어지는데 이파일에는 무시할 파일등의 환경설정등이 저장되어 있으므로 이 파일또한 같이 commit하도록 한다.

# 환경파일관리
웹 어플리케이션의 경우 데이터베이스 인증등의 id/pwd 등의 정보가 코드상에 노출될 수 있는 
위험이 있기 때문에 해당 파일에 변수로 설정하여 id/pwd등의 정보는 따로 다른 파일로 생성하여
관리하게 되는 경우가 있는데 이 때 해당 파일을 Ignore시켜서 네트워크상에 노출되지 않도록 한다.


<br/>