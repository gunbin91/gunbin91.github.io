---
layout: post
title: "Atom에디터 단축키"
tags: [ etc, atom, atom shortcut, editer ]
date: 2018-08-27
categories: [ etc ]
---

<p align="center">
    Atom은 Github에서 만든 에디터이다. 단축키를 살펴보자.
</p><br/>

- <font color="orange">Ctrl + /</font>
<br/> 주석을 토글형식으로 적용/해제
- <font color="orange">Ctrl + F</font>
<br/> 찾기/바꾸기
- <font color="orange">Ctrl + Shift + F</font>
<br/> 프로젝트 전체에서 찾기
- <font color="orange">Ctrl + E</font>
<br/> 선택 영역을 찾기/바꾸기
- <font color="orange">Ctrl + G</font>
<br/> 라인 번호로 커서 이동
- <font color="orange">Ctrl + R</font>
<br/> 키워드로 이동
- <font color="orange">Ctrl + M</font>
<br/> 블럭 매칭
- <font color="orange">Ctrl + J</font>
<br/> 라인 조인
- <font color="orange">Ctrl + L</font>
<br/> 라인 선택
- <font color="orange">Ctrl + D</font>
<br/> 현재 단어 선택 (이후 전체 범위에서 같은 단어 선택)
- <font color="orange">Ctrl + Backspace, Delete</font>
<br/> 단어 별 삭제
- <font color="orange">Ctrl + Shift + K</font>
<br/> 현재 라인 삭제
- <font color="orange">Ctrl + Shift + D</font>
<br/> 현재 라인 다음 라인으로 복사
- <font color="orange">Ctrl + [, ]</font>
<br/> 들여쓰기
- <font color="orange">Ctrl + Alt + [, ]</font>
<br/> 코드 폴딩 토글
- <font color="orange">Ctrl + Shift + Alt + [, </font>]
<br/> 전체 코드 폴딩 토글
- <font color="orange">Ctrl + ←, →</font>
<br/> 단어 별 이동
- <font color="orange">Ctrl + ↑, ↓</font>
<br/> 현재 라인 이동
- <font color="orange">Ctrl + Alt + ↑, ↓</font>
<br/> 다중 커서 삽입
- <font color="orange">Ctrl + Enter</font>
<br/> 현재 라인 밑으로 개행
- <font color="orange">Ctrl + Shift + Enter</font>
<br/> 현재 라인 위로 개행
- <font color="orange">Ctrl + Space</font>
<br/> 코드 힌트 보기
- <font color="orange">Shift + 방향키</font>
<br/> 텍스트 선택
- <font color="orange">Shift + Ctrl + ←, →</font>
<br/> 단어별 텍스트 선택

<script type="text/javascript" src="/assets/js/ZeroClipboard.js"></script>
<script type="text/javascript">
var clip = null;
function init() {
    clip = new ZeroClipboard.Client();
    ZeroClipboard.moviePath = '/assets/js/ZeroClipboard.swf';
    clip.setHandCursor( true );
    clip.setText('수정!!!!!') //이 부분을 자신한테 맞게 수정하면 된다.
    clip.glue( 'd_clip_button' );
}    
</script>

<body onLoad="init()">
<span id="d_clip_button" class="my_clip_button">복사하기</span>
</body>


<div id="contents_area" onCopy="javascript:copy_play();">
여기를 마우스로 드래그 해서 복사한 다음 다른 곳에 붙여넣기를 해보세요.
</div>


<br/>
<hr/>