--- 
layout: page
title : Etc.
permalink: /etc/
subtitle: "기타" 
feature-img: "assets/img/pexels/wall_e.jpeg"
category : etc
date : 2018-08-25
tags: [etc]
order: 100
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:50%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Etc ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>