---
layout: post
title: "3. Staged files/Unstaged files"
tags: [ git, sourcetree, stagedfile, unstagedfile ]
date: 2018-09-05
categories: [ git ]
---

<p align="center">
    수정사항이 있는 파일들의 목록인 Staged files와 Unstaged files에 대해 알아보자.
</p><br/>

# 소스트리에서 파일아이콘의 의미
File Status탭에 있는 Unstaged files목록에 있는 수정된 파일들에 대한 목록에서 파일명 왼쪽 아이콘이 있는것을 확인할 수 있다. 해당 아이콘의 의미를 살펴보자.<br/>

- <font color="orange">...</font> : 이미 깃에 의해 관리되고 있는 파일이 수정되었을 때
- <font color="orange">?</font> : 깃에 의해 관리되고 있지 않은 파일이 추가/수정 되었을 때
- <font color="orange">{%raw%}+{%endraw%}</font> : 깃 관리에 더해진 파일임을 의미한다.<br/>
( +모양의 추가되어 깃에 관리를 받게되는 파일은 다음 커밋 시 ...아이콘으로 표시된다. )

<br/>

# commit시 버전을 따로 나눌 수 있다.
unstaged files 탭에는 수정되거나 추가된 모든 파일목록들이 나오게 되기 때문에
모두 staged상태로 올려 commit할 경우 모든 변경된 상태를 하나의 버전으로 관리하지만,
수정했던 파일들을 나눠서 버전관리를 하고 싶을 경우, 하나의 버전 commit 시 해당
파일들만 staged상태로 올려서 commit하면 된다.

# git용어
- <font color="orange">working copy</font>
<br/>unstaged files 상태를 의미
- <font color="orange">index, staging area</font>
<br/>staged할 상태의 파일들을 의미
- <font color="orange">add</font>
<br/>unstaged files들을 staged files상태로 올리는 행위 (commit전)

> 하나의 파일이 staged와 unstaged 목록에 동시에 올라가 있을 수 있다.<br/>
수정한 파일을 staged files로 올린 상태에서 해당 파일을 다시 수정할 시 
unstaged files목록에 또 다시 생기기 때문에 동시에 존재할 수 있으며, <font color="deeppink">staged files목록에 있는 상태만을 commit시킨다.</font>


<br/>