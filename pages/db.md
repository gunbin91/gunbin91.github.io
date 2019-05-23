--- 
layout: page
title : DataBase
permalink: /db/
subtitle: "Database basic" 
feature-img: "assets/img/pexels/db.jpg"
category : db
date : 2019-05-08
tags: [db]
order: 9
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ DB ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>