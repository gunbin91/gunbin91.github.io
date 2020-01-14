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
    {% capture thecycle %}{% cycle 'odd', 'even' %}{% endcapture %}
  {% if thecycle == 'odd' %}
   <div style="width:50%; float:left;">
    {% else %}
    <div style="width:50%; float:right;">
    {% endif %}
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h4 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Etc ] {{ post.title }}
        </a>
    </h4>
    </div>
<!--    <hr/>-->
{% endfor %}
</div>

<br/>