--- 
layout: page
title : GithubPage
permalink: /githubPage/
subtitle: "깃허브 페이지 사용법" 
feature-img: "assets/img/pexels/computer.jpeg"
category : githubpage
tags: [github, githubpage, jekyll, hexo ]
---

<div align="center">
{% for post in site.categories[page.category] %}
    <h2>
        <a href="{{ post.url | absolute_url }}" style="text-decoration:none;">
        {{ post.title }}
        </a>
    </h2>
    <hr/>
{% endfor %}
</div>
{% if paginator.total_pages > 1 %}
  <div class="pagination">
    {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}" class="button" >
      <i class="fa fa-chevron-left"></i>
      {{ site.theme_settings.str_previous_page }}
    </a>
    {% endif %}
    {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}" class="button" >
      {{ site.theme_settings.str_next_page }}
      <i class="fa fa-chevron-right"></i>
    </a>
    {% endif %}
  </div>
  {% endif %}