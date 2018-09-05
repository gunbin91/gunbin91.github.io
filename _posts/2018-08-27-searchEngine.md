---
layout: post
title: "구글 검색엔진 최적화"
tags: [ etc, searchEnginOptimization ]
date: 2018-08-27
categories: [ etc ]
---

<p align="center">
    검색엔진(google, naver)에서 수집(크롤링)하는 사이트중에서 해당 사이트를 최대한 많이 표출해줄 수 있도록 하는 권장사항들을 모아놓은것. 대표적으로 구글에서 정의해 놓은 최적화 사항들을 살펴보자.
</p><br/>

## &lt;title>을 통하여 제목설정
<br/>페이지마다 고유한 타이틀을 명확하게 작성하여야 한다.

## &lt;meta>를 사용하여 description을 설명
<font color="orange">&lt;meta name="description" content="설명"></font>

## 이해하기 쉬운 URL사용
의미 없는 숫자형식등의 열거형식이 아닌 경로에도 의미를 부여하여 설정 하는것이 좋다.

## 같은 컨텐츠를 가진 여러개의 URL이 있을때 
컨텐츠는 비슷하지만 데이터등이 다른 여러개의 URL이 있을때 나머지페이지의 헤더에<br/>
대표 페이지를 설정해 주도록한다.
<font color="orange">&lt;link rel="canonical" href="노출될 대표페이지주소"></font>

## 사이트 이동
사이트의 이동은 스크립트가 아닌 <font color="deeppink">하이퍼텍스트</font>를 통하여 하는것이<br/>크롤링할 때 데이터 수집이 수월하게 될 수 있다.<br/>
단, 리다이렉션으로 구현할 수 있을경우 <font color="deeppink">리다이렉션</font>이 더 좋은 방법이다.

## 앵커텍스트( &lt;a> ) 사용
앵커텍스트(title속성과 같이)를 적절히 사용하는것이 좋다.<br/>
이미지의 경우 alt 또한 적절히 사용 ( 구글 이미지 검색에서 사용 )

## 제목태그 사용
제목태그(h1, h2 ...)를 사용하여 제목을 명확히 표기해주는 것이 좋다.

## url/robots.txt 차단하지 않기
사이트의 <font color="deeppink">robots.txt </font>라는 텍스트파일을 이용해 해당사이트에 대한 접근 권한을<br/> 가능/불가능 으로 설정할 수 있다. 해당 파일은 검색엔진에서 해당 사이트를 크롤링할때 유용하게 쓰일 수 있는 파일이다.<br/>

#### ▶ robots.txt
- User-agent: * <br/>권한을 설정할 유저를 설정
- Disallow : / <br/>접근권한을 거부 할 경로
- allow : / <br/>접근권한을 허가 할 경로
- Sitemap: ~~.xml <br/>웹 크롤링을 좀 더 잘 할 수 있도록 기계가 이해하기 쉬운
xml파일을 이용해<br/> 해당 페이지에 대한 보충을 설명한 xml파일을 등록

#### ▶ xml파일 작성방법
{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8"?>
<urlset
xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
	<url>
		<loc> 해당 사이트 주소 </loc>
	</url>
	....
{% endhighlight %}

## 페이지 랭크?
검색의 품질을 높이기 위해 먼저 표출할 사이트를 솎아내는 알고리즘
<br/>즉, 페이지랭크가 높을수록 검색엔진에 표출될 확률이 높다.

#### ▶ 페이지랭크를 높이는법
- 해당 사이트의 링크가 다른 사이트에 많이 참고되어 있을수록
- 페이지랭크가 높은 사이트가 해당 사이트에 대한 링크를 참고하고 있을경우


<br/>
<hr/>