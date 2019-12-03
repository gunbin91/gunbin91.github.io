---
layout: post
title: "Toad 데이터 수정 명령어 - edit"
tags: [ etc, toad, edit ]
date: 2019-12-03
categories: [ etc ]
---

<p align="center">
    데이터베이스 관리툴인 Toad에서는 데이터를 좀 더 간편하게 수정할 수 있는 명령어를 제공한다.
</p><br/>

## ◆ Edit
Toad에서 제공하는 데이터 수정 명령어이다.<br/>
데이터를 수정/추가/삭제 할 때는 UPDATE등의 명령어를 사용해야 하지만, <font color="orange">Toad에서는 edit명령어를 사용함으로서 인터페이스를 통해 손 쉽게 데이터를 수정할 수 있다.</font>

ex) <b>edit member_table</b>

또한 select문처럼 where절을 이용한 일부 데이터를 추출하여 수정하는 것도 가능하다.

ex) <b>edit member_table where age=10</b>

- 데이터를 수정하고 난 후에는 <font color="orange">commit을 해야 적용</font>된다. 상단의 commit버튼이나 아래 이미지의 v버튼을 클릭하게 되면 실제 데이터베이스에 적용이 된다.

<img src="/assets/post_img/toad_edit.PNG">

<br/>
<hr/>