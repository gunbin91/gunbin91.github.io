--- 
layout: page
title : javascript(Jquery)
permalink: /javascript/
subtitle: "자바스크립트" 
feature-img: "assets/img/pexels/js.jpg"
category : javascript
date : 2019-05-24
tags: [javascriprt]
order: 8
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        {% if post.sub_title  %}
            [ {{ post.sub_title }} ]
        {% else %}
            [ JavaScript ]
        {% endif %} 
            {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>