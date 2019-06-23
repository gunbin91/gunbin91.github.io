--- 
layout: page
title : JSP
permalink: /jsp/
subtitle: "Web development with JSP" 
feature-img: "assets/img/pexels/jsp_img.jpg"
category : jsp
date : 2019-05-08
tags: [jsp, web]
order: 10
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ JSP ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>