--- 
layout: page
title : Python
permalink: /python/
subtitle: "파이썬" 
feature-img: "assets/img/pexels/yb.jpg"
category : python
date : 2018-09-10
tags: [python, flask]
order: 5
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Python ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>