--- 
layout: page
title : GithubPage
permalink: /githubPage/
subtitle: "깃허브 페이지 사용법" 
feature-img: "assets/img/pexels/triangular.jpeg"
category : githubpage
date : 2018-08-25
tags: [github, githubpage, jekyll, hexo, blog ]
order: 3
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
   <p class="meta" align="left" style="line-height:0px;">
              {{ post.date | date: "%B %-d, %Y" }}
        </p>
    <h3 align="left">
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        [ GitHubPage ] {{ post.title }}
        </a>
    </h3>
    </div>
    <hr/>
{% endfor %}
</div>

<br/>