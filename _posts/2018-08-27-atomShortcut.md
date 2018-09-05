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

<div id="clipBoardCopyBtnWrap" class="btn_clipboard_copy">
<button id="clipBoardCopyBtn" class="btn_clipboard_copy" type="button">소스복사</button>
</div>
<div id="clipBoardCopy">복사할 컨텐츠의 내용들</div>

<script type="text/javascript">
var urlCopy = "test";               //  URL 셋팅
if (window.clipboardData) {
	$(".btn_clipboard_copy").on("click",function(){
		window.clipboardData.setData('Text',urlCopy);
	})
} else {
	var clip = new ZeroClipboard($(".btn_clipboard_copy"), {
		moviePath: "assets/js/ZeroClipboard.swf";
	});
	clip.addEventListener('mousedown',function() {
		clip.setText(urlCopy+"제로클립보드 작동");
	});
}
</script>


<div id="contents_area" onCopy="javascript:copy_play();">
여기를 마우스로 드래그 해서 복사한 다음 다른 곳에 붙여넣기를 해보세요.
</div>


<br/>
<hr/>