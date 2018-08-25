--- 
layout: page
title : Etc
permalink: /etc/
subtitle: "기타" 
feature-img: "assets/img/pexels/computer.jpeg"
category : etc
date : 2018-08-25
tags: [etc]
order: 100
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:50%;">
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