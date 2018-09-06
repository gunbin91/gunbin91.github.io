--- 
layout: page
title : Network
permalink: /network/
subtitle: "네트워크 주소 체계" 
feature-img: "assets/img/pexels/old-phone.jpeg"
category : network
date : 2018-09-06
tags: [tcp/ip, network, router, port ]
order: 4
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ Network ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>