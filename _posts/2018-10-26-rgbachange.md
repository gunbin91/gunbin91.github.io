---
layout: post
title: "이미지 rgb값 추출 및 변경"
tags: [ etc, script, rgb ]
date: 2018-10-26
categories: [ etc ]
---

<p align="center">
    이미지의 특정 위치나 특정 rgba값을 가진 픽셀에 대하여 해당 픽셀의 rgba값을 바꿀 수 있다. 
</p><br/>

# &lt;canvas>를 이용한 이미지 복제
&lt;canvas>태그를 이용하면 img태그에서 불러온 이미지를 해당 태그안으로 복제할 수 있다.<br/>
script를 이용하여 <font color="orange">canvas.getContext("2d")</font>를 통해 객체를 생성하고, 해당 객체의 <font color="orange">drawImage(img객체, 0, 0)</font>를 이용하면 이미지가 canvas태그로 복제된다.<br/>
Ex )
{% highlight ruby %}
var canvas = getElementById("myCanvas");
var ctx = canvas.getConetext("2d");
ctx.drawImage(getElementById("myImage"), 0, 0);
{% endhighlight %}

> drawImage(img, 0, 0)의 2,3번째 인자는 window의 좌표값이다.

<br/><br/>

# 이미지의 픽셀정보 가져오기
위에서 getContext("2d")로 생성된 ctx객체의 <font color="orange">getImageData(0,0, width, height)</font>를 이용하면 4칸당 하나의 픽셀정보(rgba)를 가지고 있는 배열을 반환하게 된다. 인자는 해당 이미지의 x, y, width, height값을 입력한다. <br/>
Ex )
{% highlight ruby %}
var id = ctx.getImageData(0, 0, canvas.width, canvas.height);
{% endhighlight %}

<br/><br/>

# 픽셀 순회 ( rgba 값 바꾸기 )
위에서 getImageData()를 이용하여 가져온 픽셀배열 데이터는 [r],[g],[b],[a]를 반복하는 배열이다.<br/>따라서 4칸씩 순회하면 하나의 픽셀마다 순회가 가능해진다.<br/>
Ex )
{% highlight ruby %}
var id= ctx.getImageData(0, 0, canvas.width, canvas.height);
for (var i = 0; i < id.data.length; i += 4) {
    id.data[i] = 255;       # r
    id.data[i+1] = 0;       # g
    id.data[i+2] = 0;       # b
    id.data[i+3] = 255;     # a
}
{% endhighlight %}

<br/><br/>

# rgb변경 예제
{% highlight ruby %}
function canvas_view(imageObj){
    var canvas = imageObj.nextSibling.nextSibling;
    
    # canvas의 크기를 이미지와 동일하게 설정
    canvas.height = imageObj.height;
    canvas.width = imageObj.width;
    
    # canvas에 이미지 복제
    var ctx= canvas.getContext("2d");
    ctx.drawImage(imageObj, 0, 0);
    
    # 복제된 이미지에 대한 픽셀정보를 가져옴
    var id= ctx.getImageData(0, 0, canvas.width, canvas.height);
    # 픽셀순회
    for (var i = 0; i < id.data.length; i += 4) {
        # 픽셀값이 (0, 0, 0)일 경우에만 변경
        if ( id.data[i] + id.data[i+1] + id.data[i+2] == 0 ){
            id.data[i] = 255;
            id.data[i+1] = 165;
            id.data[i+2] = 0;
            id.data[i+3] = 255;
        }
        
    }
        
    // canvas에 바꾼 rgba정보로 재배치
    ctx.putImageData(id, 0, 0);
}
{% endhighlight %}


<br/>