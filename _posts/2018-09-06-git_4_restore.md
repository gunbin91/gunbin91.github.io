---
layout: post
title: "4. 복원/복구"
tags: [ git, sourcetree, gitrevert ]
date: 2018-09-06
categories: [ git ]
---

<p align="center">
    프로젝트 진행중에 이전 버전으로 되돌리고 싶을경우 사용하는 여러 방법에 대해 알아보자.
</p><br/>

# Discard ( commit취소 )
파일수정 후 <font color="deeppink">commit하기 전 수정 사항을 취소</font>할 수 있는 기능으로
파일 수정 후 commit하기 전에 다시 수정한 것을 취소하려면 <font color="orange">Discard버튼을 누른 후 해당 파일 선택 후 Discard Change버튼</font>을 누르면 해당 수정사항이 사라지고 처음 상태로 돌아간다.
<br/>
(단, commit한 상태를 Discard할 순 없다. )

<br/>

# Reset ( 버전 되돌리기 )
Log/History탭에서 돌아가고자 하는 버전을 오른쪽 클릭한 후 <font color="orange">Reset current branch to this commit"</font>을 클릭하고 <font color="orange">Using mode를 Hard</font>로 선택한 후 ok를 누르게 되면 <font color="deeppink">해당 버전으로 돌아가고 그 이후 commit되었던 버전들은 모두 삭제된다.</font> 따라서, <font color="red">조심하게 사용해야 할 기능</font>이다.

#### Using mode
- <font color="orange">Hard</font>
<br/>모든 사항을 선택한 지점으로 되돌린다. 
- <font color="orange">Mixed</font>
<br/>현재 working copy의 상태는 commit되지 않은 상태로 유지 되면서
해당 버전 이후의 버전들은 모두 삭제된다. 또한, 추가한 파일이 있는 버전이 있는 경우 해당 파일 또한 working copy(Unstaged files)의 목록으로 들어오게 된다.

<br/>

# Revert ( 버전 변경 )
<font color="deeppink">최신의 버전상태를 삭제하지 않고, 그 이전 상태의 버전으로 돌아가고 싶을 때 사용하는 기능</font>으로, 돌아가고자 하는 버전을 오른쪽 클릭 후 <font color="orange">'reverse commit'</font>를 클릭하면 된다.<br/>

이렇게 하면 가장 최신의 버전이 Revert라는 문구를 앞에 붙인 상태로
해당 버전이 최신버전이 되는데, 이렇게 원래 있던 버전을 계속 commit하여
최신버전으로 쌓아가는 것이기 때문에 순서에 주의해야한다. 


<br/>
