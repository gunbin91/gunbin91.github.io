--- 
layout: page
title : GithubPage
permalink: /githubPage/
subtitle: "깃허브 페이지 사용법" 
feature-img: "assets/img/pexels/computer.jpeg"
category : githubpage
tags: [github, githubpage, jekyll, hexo, blog ]
---

<div align="center">
{% for post in site.categories[page.category] %}
   <div style="width:75%;">
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