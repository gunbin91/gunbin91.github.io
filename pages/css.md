--- 
layout: page
title : CSS
permalink: /css/
subtitle: "Style" 
feature-img: "assets/img/pexels/book-glass.jpeg"
category : css
date : 2018-10-29
tags: [css]
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
        [ Etc ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>