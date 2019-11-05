---
layout: post
title: "이미지 좌표에 링크 쉽게 걸기"
tags: [ etc, image map ]
date: 2019-11-05
categories: [ etc ]
---

<p align="center">
    
</p><br/>

◆ 이미지 좌표에 쉽게 링크넣기
이미지에 통으로 링크를 연결시키는 것은 간단하나, 이미지의 일부 좌표에만 링크를 연결하는 것은 매우 번거로운 작업이다.
그래서 이를 쉽게 구현할 수 있도록 이미지에서 좌표를 클릭하여 링크를 연결시켜주는 코드를 반환해 주는 사이트가 있다.

1. https://www.image-map.net/ 접속
2. Select Image from My PC 클릭하여 이미지 로딩
3. 하단에 링크 모양을 선택하고 이미지에서 좌표와 크기를 선택
: 여러개를 추가할 수 있다.
4. Show me the code! 버튼을 누르면 아래와 같은 코드를 반환해준다.
상황에 따라 적절히 사용하면 된다.

> 단, 이미지의 크기를 변경할 경우 작동하지 않는다.

ex) 
<img src="/images/test.jpg" usemap="#image-map">
<map name="image-map">
	<area class="mapArea" target="_blank" alt="" title="" href="http://www.naver.com" coords="0,0,221,155" shape="rect">
	<area class="mapArea" target="_blank" alt="" title="" href="http://www.google.com" coords="0,34218,642,34576" shape="rect">

	<area class="mapArea" alt="" title="" href="javascript:workPop('work', 1);" coords="166,25688,465,25931" shape="rect">
	<area class="mapArea" alt="" title="" href="javascript:workPop('work', 2);" coords="495,25689,784,25936" shape="rect">
</map>
		






<br/>
<hr/>