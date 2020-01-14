--- 
layout: page
title : AWS
permalink: /aws/
subtitle: "AmazonWebService" 
feature-img: "assets/img/pexels/triangular.jpeg"
category : aws
date : 2020-01-03
tags: [aws]
order: 13
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h4 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ AWS ] {{ post.title }}
        </a>
    </h4>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>