--- 
layout: page
title : Git
permalink: /git/
subtitle: "SourceTree를 이용한 Git사용법" 
feature-img: "assets/img/pexels/motherboard.jpg"
category : git
date : 2018-09-06
tags: [github, git, sourcetree ]
order: 2
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Git ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>