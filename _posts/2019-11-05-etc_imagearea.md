---
layout: post
title: "이미지 좌표에 링크 쉽게 걸기"
tags: [ etc, image map ]
date: 2019-11-05
categories: [ etc ]
---

<p align="center">
   이미지안의 링크로 간단하게 페이지를 구성할 때 각각의 좌표에 쉽게 링크를 걸 수 있는 방법에 대해 알아보자. 
</p><br/>

## ◆ 이미지 좌표에 쉽게 링크넣기
이미지에 통으로 링크를 연결시키는 것은 간단한 작업이나, 이미지의 일부 좌표에만 링크를 연결하는 것은 매우 번거로운 작업이다.<br/>
하지만 이를 쉽게 구현할 수 있도록 이미지에서 좌표를 클릭하여 링크를 연결시켜주는 코드를 반환해 주는 사이트가 있다.

### ▶ 이미지 링크 코드 반환
- 1 https://www.image-map.net/ 접속
: <a href="https://www.image-map.net/" target="_blank">https://www.image-map.net/</a> 해당 사이트에서 이미지의 좌표에 링크를 걸 수 있는 코드를 반환해 주는 서비스를 제공한다.

- 2 이미지로드
: Select Image from My PC 클릭하여 이미지 파일을 선택하면 사이트내부로 이미지가 로드된다.

- 3 하단에 링크 모양을 선택하고 이미지에서 좌표와 크기를 선택
: shape로 링크를 걸 수 있는 모양을 선택하고 이미지에서 좌표를 클릭하여 선택한다.

- 4 Show me the code! 버튼을 누르면 아래와 같은 코드를 반환해준다.
: 아래 코드를 상황에 따라 적절히 스크립트로도 사용할 수 있다.<br/>
( 단, 이미지의 크기를 변경할 경우 작동하지 않는다. )

<br/>

{% highlight ruby %}
<img src="/images/test.jpg" usemap="#image-map">
<map name="image-map">
	<area class="mapArea" target="_blank" alt="" title="" href="http://www.naver.com" coords="0,0,221,155" shape="rect">
	<area class="mapArea" target="_blank" alt="" title="" href="http://www.google.com" coords="0,34218,642,34576" shape="rect">

	<area class="mapArea" alt="" title="" href="javascript:workPop('work', 1);" coords="166,25688,465,25931" shape="rect">
	<area class="mapArea" alt="" title="" href="javascript:workPop('work', 2);" coords="495,25689,784,25936" shape="rect">
</map>
{% endhighlight %}

<br/>

<img src="/assets/img/portfolio/ttt.png" usemap="#image-map" style="padding:0;">
<map name="image-map">
    <area target="" alt="" title="" href="http://www.naver.com" coords="519,156,622,259" shape="rect">
    <area target="" alt="" title="" href="javascript:alert('안녕하세요');" coords="340,215,51" shape="circle">
    <area target="" alt="" title="" href="javascript:alert('이미지 링크입니다.');" coords="561,438,46" shape="circle">
</map>




<br/>
<hr/>