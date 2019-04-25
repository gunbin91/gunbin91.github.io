--- 
layout: page
title : Java
permalink: /java/
subtitle: "자바" 
feature-img: "assets/img/pexels/javacap.jpg"
category : java
date : 2019-04-25
tags: [java, web]
order: 7
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Java ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>