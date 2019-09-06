--- 
layout: page
title : Spring
permalink: /spring/
subtitle: "Web development with SPRING" 
feature-img: "assets/img/pexels/jsp_img.jpg"
category : spring
date : 2019-09-06
tags: [spring, web]
order: 11
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ SPRING ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>